# Retrospective 2 — Festival Retrospective

This was our second retrospective, and we used a "fun" Festival format this time around. The idea is that different areas of the festival map to different reflection categories. Here's how it went

## Main Stage — Highlights

These are the things that went well and that we really enjoyed this sprint:

- **Response streaming support** — we got the backend by Tamino to stream AI responses instead of waiting for the full reply. Way better UX (Which would be implemeted any time now)
- **Frontend UI overhaul** — the whole frontend got a fresh look. Feels a lot more polished and usefull now.
- **Live VRM model rendering** — we got a 3D avatar rendering live in the browser with animations and everything. Probably the coolest feature we shipped.

## Fortune Teller — Things We Wish We Knew at the Start

Compared to our first retro, we've learned a lot of things the hard way that would've saved us time if we knew them earlier:

- **3D VRM model is not as hard to use** — we were intimidated by the idea of putting a 3D model in a web app, but `@pixiv/three-vrm` made it surprisingly straightforward. Wish we'd started with it sooner.
- **How to do a proper frontend** — structuring a React app properly, managing state, keeping components clean. We figured it out along the way but it would've been nice to know best practices from day one.
- **We should have written the backend in Python** — hot take, but cmon, we all can agree Python >>> Rust

## First Aid Tent — Pain Points

Things that didn't go as well as we'd hoped:

- **Requirements** — we could've been clearer about what exactly we were building from the start. Some features were a bit vague.
- **Behaviour Driven Development** — getting Cucumber.js + Puppeteer to work properly was more painful than expected. The tooling didn't always cooperate.
- **Accurately entering stuff into YouTrack** — we weren't great at keeping our project management tool up to date. Tasks got done but weren't always tracked.
- **Unable to store user data in DynamoDB** — we ran into issues with storing user-specific data. DynamoDB's data model took some getting used to.

## Actions — What We'll Do Better Next Time

- **Proper YouTrack tracking** — actually keep the board updated so we know where things stand, or just not use it at all 
- **Better testing** — write tests earlier, not as an afterthought. We've started with unit tests now but wish we had them from the beginning.

## Takeaway

This retro showed that we've grown a lot as a team since the first one. The highlights are real — streaming, the UI overhaul, and the VRM model are features we're genuinely proud of. But we also know where we dropped the ball, especially around project tracking and testing discipline. The good news is we're already acting on it.
