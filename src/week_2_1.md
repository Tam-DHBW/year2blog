# Semester 2 | Week 1

Hey everyone, it's been a while!
After diving deep into the practical side of things for months,
we're finally circling back to some theory,
and that means it's time to pick up where we left off with the Jailbreak project.

Quick refresher on what we're actually building here:
As large language models and AI agents keep weaving themselves deeper into everyday life at an insane pace,
the big players are racing to lock them down with all sorts of restrictions and safety layers (commonly known as guardrails).
These are the rules and filters that try to prevent misuse, harmful outputs, or just plain weird behavior.

In our view, the most effective way to really understand how those guardrails work (and where they fall short) isn't just reading papers or watching talks:
it's by rolling up your sleeves and trying to break them.
So that's exactly what we're doing: building a simple LLM setup and then jailbreaking it using different techniques, step by step.
Hands-on learning beats theory every time.

For the rest of the Software Engineering class, we've decided to stick with the original scope we set at the beginning.
The topic is still super relevant, and honestly, it's only gotten more interesting as new jailbreaking methods and stronger defenses keep popping up in the wild.
We're not planning any major rewrites to the core architecture or logic.
Why mess with something that's been rock-solid?
**Since we deployed it five months ago, we've had literally zero downtime and haven't needed to touch it for support**.
That's the kind of reliability you dream about!

Instead, our focus is on leveling up in a few key areas. We're expanding the test suite significantly to catch more edge cases.
The game design is already getting a full rebuild to make the experience more engaging and replay-able.
We're adding complete mobile support so people can play on the go without friction.
And perhaps most excitingly, we're planning to migrate to a smarter, higher-parameter model that should deliver a noticeably more lifelike and responsive feel.

On top of that, one of our big new goals is building out a progressive level tree.
Right now, once you've "completed" the game by breaking through certain guardrails,
there's not much incentive to come back. We want to change that: make replaying worthwhile with escalating challenges.
Plus, we've realized that ranking individual jailbreaking techniques in isolation isn't the most accurate approach anymore.
In practice, it's the clever combinations of techniques that really manage to slip past defenses, not any single trick standing alone.
So the level progression will reflect that layered reality.

One last fun side note: under our current (pretty low) usage, the AWS bill is basically zero.
None of the core services we've leaned on have even come close to exceeding the free tier limits.
It's a nice little reminder that you can run meaningful experiments without burning through cloud credits.

That's the plan moving forward. Excited to share more updates as we implement these changes, so stay tuned, and feel free to drop thoughts or suggestions in the comments.
We are always happy to chat about guardrails, jailbreaks, or why our AWS costs are still at $0 😄
