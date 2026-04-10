# How to Load a VRM Model in a React Website

<img width=100% height=100% alt="PNG image" src="https://github.com/user-attachments/assets/bda71620-a577-4fab-8f66-d558ca9fb806" />

## What you need

```bash
npm install three @pixiv/three-vrm
```

## The minimal component

```jsx
import { useEffect, useRef } from 'react'
import * as THREE from 'three'
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js'
import { VRMLoaderPlugin, VRMUtils } from '@pixiv/three-vrm'

export default function VRMViewer() {
  const containerRef = useRef(null)

  useEffect(() => {
    const container = containerRef.current
    if (!container) return

    // 1. Set up renderer
    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true })
    renderer.setSize(container.clientWidth, container.clientHeight)
    renderer.setPixelRatio(window.devicePixelRatio)
    container.appendChild(renderer.domElement)

    // 2. Scene + camera + lights
    const scene = new THREE.Scene()
    const camera = new THREE.PerspectiveCamera(25, container.clientWidth / container.clientHeight, 0.1, 20)
    camera.position.set(0, 1.4, -1.5)
    camera.lookAt(0, 1.3, 0)

    scene.add(new THREE.AmbientLight(0xffffff, 0.6))
    const light = new THREE.DirectionalLight(0xffffff, 1.2)
    light.position.set(1, 2, 2)
    scene.add(light)

    // 3. Load the VRM
    const loader = new GLTFLoader()
    loader.register((parser) => new VRMLoaderPlugin(parser))

    loader.load('/assets/your-model.vrm', (gltf) => {
      const vrm = gltf.userData.vrm
      VRMUtils.combineSkeletons(vrm.scene)
      scene.add(vrm.scene)
    })

    // 4. Render loop
    const clock = new THREE.Clock()
    let frameId
    const animate = () => {
      frameId = requestAnimationFrame(animate)
      renderer.render(scene, camera)
    }
    animate()

    // 5. Cleanup on unmount
    return () => {
      cancelAnimationFrame(frameId)
      renderer.dispose()
      container.removeChild(renderer.domElement)
    }
  }, [])

  return <div ref={containerRef} style={{ width: '100%', height: '400px' }} />
}
```

## How it works

1. Put your `.vrm` file in the `public/assets/` folder (or wherever your static files live)
2. `GLTFLoader` + `VRMLoaderPlugin` handles parsing the VRM format — VRM is basically a glTF file with extra humanoid metadata
3. Three.js renders it to a canvas inside your div
4. The camera is positioned for a portrait/upper-body shot — tweak `camera.position` and `camera.lookAt` to frame it how you want

## Want animations too?

Add the animation package:

```bash
npm install @pixiv/three-vrm-animation
```

Then load `.vrma` files (VRM animation format):

```jsx
import { VRMAnimationLoaderPlugin, createVRMAnimationClip } from '@pixiv/three-vrm-animation'

// Register the plugin alongside VRMLoaderPlugin
loader.register((parser) => new VRMAnimationLoaderPlugin(parser))

// Load and play an animation
loader.load('/assets/animations/idle.vrma', (gltf) => {
  const vrmAnim = gltf.userData.vrmAnimations[0]
  const clip = createVRMAnimationClip(vrmAnim, vrm)
  const mixer = new THREE.AnimationMixer(vrm.scene)
  mixer.clipAction(clip).play()

  // Update mixer in your render loop:
  // mixer.update(clock.getDelta())
})
```

## Where to get VRM models and animations

- [VRoid Hub](https://hub.vroid.com/) — free VRM avatars
- [VRoid Studio](https://vroid.com/en/studio) — make your own
- Animation packs from tk256ailab and VRoid official work great with any VRM model

That's basically it — Three.js does the heavy lifting, `@pixiv/three-vrm` handles the VRM-specific stuff. Drop the component in, point it at your `.vrm` file, and you're good. I would highly recomend to use built in Animations or motion capture to create ur own, otherwiese it's will be a hell of a work
