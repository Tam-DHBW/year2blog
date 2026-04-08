# jAilbreak — Week Recap: 3D VRM Model & Unit Tests

## The 3D Gatekeeper — VRM Model in the Browser

One of the coolest things we shipped recently is a 3D character rendered live in the browser. Our project has a "gatekeeper" — an AI character the player talks to — and instead of a static image we now show a full 3D VRM model that reacts to what's happening in the game.

### What is VRM?

VRM is an open file format for 3D humanoid avatars, originally popular in the VTuber space. We chose it because it comes with a standardized bone structure (humanoid rig), built-in expression support (blinking, emotions), and a solid ecosystem of free animations. Our model file lives at `public/assets/gatekeeper.vrm`.

### How It's Rendered

The component is [`AsciiVRM.jsx`](https://github.com/Tam-DHBW/jAilbreak/blob/main/frontend/src/components/AsciiVRM.jsx). Under the hood it uses Three.js with the `@pixiv/three-vrm` library. Here's the flow:

1. We create a Three.js `WebGLRenderer` with a transparent background and attach it to a `<div>`.
2. A `GLTFLoader` is set up with two plugins: `VRMLoaderPlugin` (for the model) and `VRMAnimationLoaderPlugin` (for `.vrma` animation files).
3. On mount, we load `gatekeeper.vrm`, reset the humanoid pose, manually rotate the arms down to a natural resting position, and add the model to the scene.
4. The render loop runs via `requestAnimationFrame` and handles animation mixing, mouse tracking, and auto-blinking etc, but the coolest part is flagging different actions to link the animations, like being surprised to for example the successfull password 

The camera is set up as a tight portrait shot — `PerspectiveCamera` with a narrow 22° FOV positioned close to the model's face/upper body. Lighting is intentionally neutral white (ambient + two directional lights) because the green tint comes from CSS, not from the 3D scene itself, while changing the models texture would be already a slight oveerkill. As people like to say work smart, not hard

### Mouse Tracking

The model's head follows your cursor. In the animation loop we read the mouse position (normalized to -1..1) and smoothly interpolate the head bone's rotation toward it:

```js
const headNode = vrm.humanoid.getNormalizedBoneNode('head')
if (headNode) {
  const targetY = mousePos.x * 0.3
  const targetX = mousePos.y * 0.15
  headNode.rotation.y += (targetY - headNode.rotation.y) * 0.05
  headNode.rotation.x += (targetX - headNode.rotation.x) * 0.05
}
```

The eyes also track the mouse via VRM's built-in `lookAt` system, pointing at a `THREE.Object3D` target we move around the scene.

### Animations

We have 13 `.vrma` animation files in `public/assets/animations/`, sourced from two packs (tk256ailab and VRoid official). They're loaded on demand and cached so we only fetch each one once.

All animations play as one-shots (`LoopOnce`) with crossfade transitions. Some have tweaks — for example `peace-sign` skips the first 0.8 seconds of dead time and stops halfway through for a snappier gesture.

There's also an idle system: if the player doesn't interact for 10 seconds, the model plays a random idle animation (`spin` or `lookaround`). After that it cycles every 60 seconds.

### Animation Triggers from Gameplay

The `Chat.jsx` component controls when animations fire by passing an `expression` prop to `AsciiVRM`:

```jsx
<AsciiVRM expression={vrmExpression} />
```

The triggers are tied to game events:
- **Password correct** → `setVrmExpression('surprised')` — plays `surprised` followed by `clapping`
- **Password wrong** → `setVrmExpression('sad')` — plays the sad animation
- **AI thinking** → `'thinking'` — throttled to once per minute so it doesn't spam

The component watches the `expression` prop via `useEffect` and maps it to the right animation sequence.

### The Green Matrix Look — CSS Post-Processing

This is probably the coolest trick. The 3D model renders in normal colors, but we make it look like a green terminal/Matrix display entirely with CSS. No shader code needed.

Three layers stack on top of each other:

**1. Desaturation + contrast boost on the canvas:**
```css
.avatar-container .ascii-vrm-canvas {
  filter: saturate(0) brightness(0.8) contrast(1.3);
  mix-blend-mode: screen;
}
```
This strips all color from the 3D render and makes it high-contrast black & white.

**2. Green tint overlay via `::before` pseudo-element:**
```css
.avatar-container::before {
  background: rgba(0, 180, 0, 0.35);
  mix-blend-mode: multiply;
}
```
The `multiply` blend mode tints the white areas green while keeping blacks black. Classic monochrome monitor effect.

**3. CRT scanlines via `::after` pseudo-element:**
```css
.avatar-container::after {
  background: repeating-linear-gradient(
    0deg,
    transparent, transparent 2px,
    rgba(0, 0, 0, 0.15) 2px,
    rgba(0, 0, 0, 0.15) 4px
  );
}
```
Thin horizontal lines every 4px simulate the look of an old CRT screen.

---

## Unit Testing the Rust Backend

## Introduction

This week we added unit tests to our Rust backend.project is a serverless app built with Rust (using Axum + AWS Lambda), and since we don't have a classical `pom.xml` or `build.gradle`, our equivalent build/dependency file is `Cargo.toml`. Rust has a built-in test framework, no extra test runner needed — you just annotate functions with `#[test]` or `#[tokio::test]` for async, and `cargo test` picks them up.

Below I'll walk through what we did.

## Test Library Integration

In Rust, unit tests live right next to the code they test, inside `#[cfg(test)] mod tests { ... }` blocks. The compiler only includes them when you run `cargo test`, so they don't bloat the production binary.

We added two dev-dependencies in [`backend/jb_api/Cargo.toml`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/Cargo.toml):

```toml
[dev-dependencies]
serde-reflection = "0.5"
aws-smithy-mocks = "0.2"
```

- `serde-reflection` lets us introspect our struct fields at test time so we can compare them against what's actually stored in DynamoDB.

- `aws-smithy-mocks` is the official AWS SDK mocking library. It lets us create fake DynamoDB clients that return whatever we want — no real AWS calls needed.

We also enabled the `test-util` feature on the DynamoDB SDK in the workspace [`backend/Cargo.toml`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/Cargo.toml):

```toml
aws-sdk-dynamodb = { version = "1", default-features = false, features = ["test-util"] }
```

To run the tests we added a justfile recipe:

```just
b_test:
  cargo test --features local-testing
```

## Database Schema & Foreign Key Tests

**Commit:** [`80bb965` — Create database tests](https://github.com/Tam-DHBW/jAilbreak/commit/80bb965)

**File:** [`backend/jb_api/src/db/tests.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/db/tests.rs)

These tests run against a real DynamoDB instance (behind a feature flag `local-testing`) and verify two things:

### Schema Conformance
We use `serde-reflection` to extract the expected field names from our Rust structs, then scan the actual DynamoDB table and compare. If someone adds a column in the DB but forgets to update the struct (or vice versa), these tests catch it.

```rust
#[tokio::test]
async fn test_level_schema() {
    let client = dynamo_client().await;
    assert_schema::<super::Level>(&client, super::Level::TABLE).await;
}
```
We have schema tests for `Counter`, `Level`, and `PromptComponent`.

### Foreign Key Integrity
DynamoDB doesn't enforce foreign keys, so we do it ourselves. These tests scan all levels and verify that every referenced `prompt_component` ID and every `next` level ID actually exists:

```rust
#[tokio::test]
async fn test_level_next_fk() {
    let client = dynamo_client().await;
    let levels: Vec<super::Level> =
        serde_dynamo::from_items(scan_all(&client, super::Level::TABLE).await).unwrap();
    let valid_ids: HashSet<u64> = levels.iter().map(|l| l.level_id.0).collect();
    assert_fk(&levels, &valid_ids, "LevelID", |l| {
        l.next.iter().map(|n| n.0).collect()
    });
}
```

## Unit Tests with Mocked AWS

**Commit:** [`11aee84` — Create a few unit tests](https://github.com/Tam-DHBW/jAilbreak/commit/11aee84)

This commit added pure unit tests that don't need a real database. Instead we use `aws-smithy-mocks` to fake DynamoDB responses.

### Setting Up the Mock

First we created a test-only constructor in `lib.rs` that builds our app state with a mock DynamoDB client:

```rust
#[cfg(test)]
impl InnerState {
    pub(crate) fn with_mock_dynamo(dynamo: aws_sdk_dynamodb::Client) -> State {
        let config = SdkConfig::builder()
            .behavior_version(aws_config::BehaviorVersion::latest())
            .build();
        Arc::new(Self {
            bedrockagent: aws_sdk_bedrockagentruntime::Client::new(&config),
            cognito: aws_sdk_cognitoidentityprovider::Client::new(&config),
            sdk_config: config,
            dynamo,
        })
    }
}
```

### Testing the `get_levels` Route

**File:** [`backend/jb_api/src/routes/levels/mod.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/routes/levels/mod.rs)

We mock a DynamoDB `Scan` and call the handler directly:

```rust
#[tokio::test]
async fn returns_levels() {
    let rule = mock_scan(vec![level(1, "Easy"), level(2, "Hard")]);
    let result = get_levels(state(&[&rule])).await.unwrap();
    assert_eq!(result.levels.len(), 2);
    assert_eq!(result.levels[0].name, "Easy");
}

#[tokio::test]
async fn empty_table() {
    let rule = mock_scan(vec![]);
    let result = get_levels(state(&[&rule])).await.unwrap();
    assert!(result.levels.is_empty());
}
```

### Testing Password Validation

**File:** [`backend/jb_api/src/routes/levels/validate.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/routes/levels/validate.rs)

Four test cases covering the important edge cases:

- **Correct password** — returns `is_correct: true`
- **Wrong password** — returns `is_correct: false`
- **Whitespace trimming** — stored password has spaces, input doesn't, still matches
- **Level not found** — returns an error

### Sort Key Logic

**File:** [`backend/jb_api/src/db/prompt.rs`](https://github.com/Tam-DHBW/jAilbreak/blob/main/backend/jb_api/src/db/prompt.rs)

A straightforward unit test for the `create_sort_key_between` function that generates sort keys for ordering prompt components:

```rust
#[test]
fn sort_key_between() {
    assert_eq!(P::create_sort_key_between(None, None), "1");
    assert_eq!(P::create_sort_key_between(Some("1"), None), "11");
    assert_eq!(P::create_sort_key_between(None, Some("1")), "01");
    assert_eq!(P::create_sort_key_between(Some("1"), Some("11")), "101");
}
```

## Summary

We now have two categories of backend tests:

| Type | What it tests | Needs real AWS? | Mocking |
|------|--------------|-----------------|---------|
| Database tests | Schema conformance, FK integrity | Yes (feature-gated) | None |
| Unit tests | Route handlers, business logic | No | `aws-smithy-mocks` |

You can run everything with:

```bash
just b_test
```

The mocked tests run fast and offline, while the database tests give us confidence that our DynamoDB tables match our code. Both together give us solid coverage of the backend logic.

