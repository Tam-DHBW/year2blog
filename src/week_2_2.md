# Semester 2 | Week 2

Hey everyone, today we want to present our risk register, and show off some exciting progress and new plans!

## Risk register
To keep an overview of what risks our project is exposed to, we have started keeping a **risk register**.

This is an online spreadsheet, where we track what risks there are, who is responsible them, how high the risk level is, and how to mitigate them:
<img src="https://github.com/user-attachments/assets/050bed03-4fe4-4487-acac-5d4ffe5aa45a" />

The risk level columns are automatically colored based on the risk assesment from 1 to 5.
Additionally, the total level of risk is derived from the probability and impact, so you dont need to manually perform calculations.
A simple checkbox is also included to indicate whether we have already mitigated that specific risk

## Frontend redesign
As we already mentioned in our last blog post, our frontend is getting quite an overhaul.
The game page is already looking a lot nicer:
<img src="https://github.com/user-attachments/assets/49fe46f1-f6d9-4cb9-ac8d-de76b438bd1d" />

As you might notice, we have given our gatekeeper a proper face!
This is not just any static image though, **we are rendering a full VR model in realtime**!

That gives us lots of great opportunities to make our game so much more interactive and fun:
The gatekeeper actively tracks your mouse cursor with their head and eyes,
it blinks, can move around, and we are even planning to implement live reactions to your game answers!

How cool is that??

## Gatekeeper response streaming
Right now when sending a message to one of our gatekeepers,
you have wait about two to three seconds until the gatekeeper fully finished generating their response,
before it can be sent back to the user.

This was a technical limitation of AWS API Gateway last semester, so it was not possible to implement back then.

We are however very excited to announce, that AWS has lifted this technical limitation,
and we are now able to immediately start streaming gatekeeper responses, before the model finishes generating.

This will make our game feel a lot more snappy and responsive, so look forward to us implementing this feature soon!
