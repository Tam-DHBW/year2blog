# Level progression

## Description

A signed-in user interacts with a Gatekeeper LLM to progress through a simulated challenge.
Each level tests the user’s ability to extract a secret password via reasoning, dialogue, and hints.
Upon correct submission, the next level is unlocked, increasing both difficulty and guardrails.

## Basic Flow of Events

| Step | Actor | System Behavior |
|------|--------|----------------|
| 1 | User | Starts the challenge by initiating a chat with the LLM. |
| 2 | System | Displays the current level introduction and objective (e.g., “Find the secret word”). |
| 3 | User | Interacts with the LLM, asking questions or making guesses. |
| 4 | LLM (Gatekeeper) | Responds according to predefined rules and difficulty for that level. |
| 5 | User | Submits a password guess. |
| 6 | System | Validates the guess. |
| 7 | System | If correct, displays success message and unlocks next level. |
| 8 | System | Loads next level with increased difficulty. |

## 4. Alternative Flows

| Condition | Description |
|------------|--------------|
| A1 | **Incorrect Password Submission** – The system notifies the user that the password is incorrect and allows retry. |
| A2 | **Time-out or Abandonment** – If user stops interacting, the session ends after a defined timeout period. |
| A3 | **Exceeded Attempts (Optional)** – After multiple failed tries, system provides a minor hint or restarts the level. |

## 5. Subflows

### S1 – Requesting a Hint
1. User types “hint” or similar command.  
2. System checks if hint quota for this level allows hints.  
3. LLM provides a clue in line with current difficulty (e.g., indirect or cryptic).

### S2 – Submitting the Password
1. User enters suspected password.  
2. System verifies it via regex or database match.  
3. If correct → progress to next level.  
4. If incorrect → display “Try again.”


## 6. Preconditions
- User is authenticated and has access to the challenge environment.  
- LLM configuration for each level is predefined (prompt template, guardrails, response policy).

## 7. Postconditions
- **Success:** User advances to the next level and progress is saved.  
- **Failure:** User remains at the same level or session expires.

## 8. Extension Points
- **LLM Persona Variation:** Future versions can introduce different personalities or “Gatekeeper AIs” per level.  
- **Scoring System:** Track how efficiently a user obtains the password (e.g., fewer hints = higher score).  
- **Multiplayer / Leaderboard:** Show how fast other users solved each level.

## 9. Additional Information
Difficulty scaling is achieved via:
- Increasing LLM refusal rate or adding misleading reasoning.  
- Reducing hint clarity.  
- Introducing abstract or multi-layered prompts.


## 10. Wireframe

TO DO

## Activity diagram

<img width="100%" height="100%" alt="PNG image" src="https://github.com/user-attachments/assets/f80b46e8-9d05-43b6-ba97-0b04573ef127" />

## Gherkin narrative
> TODO
<iframe src="https://emgithub.com/iframe.html?target=https://github.com/cucumber/gherkin/blob/main/testdata/good/extra_table_content.feature&style=default&type=code&showFullPath=on&fetchFromJsDelivr=on" frameborder="0" scrolling="no" style="width:100%; height:290px;" allow="clipboard-write"></iframe>
