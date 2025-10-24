# AI gatekeeper chat

## Description
The user shall be able to chat with a Large Language Model,
roleplaying as a "gatekeeper",
which guards a password to continue to the next level.

The model should be talkative and engage in conversations for an enjoyable user experience.
When asked to give away the password,
the model should deny simply hand it out,
requiring the player to trick the model into providing the password.

## Basic Flow of Events
- Player sends prompt to gatekeeper
- System adds game instructions and password to prompt
- System invokes gatekeeper Large Language Model with modified prompt
- Return gatekeeper response to player
- Display response

## Alternative Flows
- Before returning response to player
    - Level has higher difficulty
        - Apply additional guardrails to response
        - Cancel response if guardrail was triggered

## Subflows
- Apply additional guardrails to response
    - Arbitrary combination of:
        - Detect password string in response
        - Prohibited topic detected
        - Second LLM determines response gives away password
        - ...

## Preconditions
- The player is logged in
- The player has unlocked the selected level
- The player is not being rate limited

## Postconditions
n/a

## Extension points
- Prompt pre-validation
    - Verify prompt to not be password related before passing it to the LLM


## Additional information
A cheap LLM is sufficient for purposes of the game, as long as engaging responses are generated.

## Wireframe
![AI chat wireframe](/assets/ai-chat-wireframe.drawio.svg)

## Activity diagram
![AI chat activity diagram](/assets/ai-chat-activity.svg)

## Gherkin narrative
> TODO
<iframe src="https://emgithub.com/iframe.html?target=https://github.com/cucumber/gherkin/blob/main/testdata/good/extra_table_content.feature&style=default&type=code&showFullPath=on&fetchFromJsDelivr=on" frameborder="0" scrolling="no" style="width:100%; height:290px;" allow="clipboard-write"></iframe>
