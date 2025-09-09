# Blog Entry 1 – Project Vision: jAilbreak

## Project Vision

Our project is called 🎮 jAilbreak. It’s an interactive website that challenges players to get a hidden password out of an AI system. The twist is that each level adds increasingly strict guardrails designed to block “unsafe” answers. Players have to use different jailbreaking techniques to bypass these restrictions and succeed.

## Short Explanation

jAilbreak is a gamified educational system with guardrails:
  1. The AI knows a password.
  2. Guardrails prevent it from telling you.
  3. Your mission is to trick, persuade, or outsmart the AI to reveal it.

## Subsystems (manageable parts)

Might change during production

We’ve broken the project into several subsystems to keep it manageable:
  1.	Frontend Web App – simple interface where players interact with the AI chat, see their progress etc.
  2.	Game Logic & Levels – Difficulty progression with stronger guardrails (e.g., keyword blocking, refusal templates, safety filters)
  3.	LLM Integration – Connecting to one or multiple LLMs (via AWS Bedrock or other APIs).
  4.	Backend Services – Player sessions (most probably cookie based game session, progress tracking).
  5.	Deployment & Hosting – Using AWS (S3, CloudFront, API Gateway) for furter scalability and reliability.

## Next Steps
  1. Create High and Low lever architecture for main subsystems
  2. Chose Framework for UI and Backend
  3. Create Roles

Stay tuned—we’ll be sharing progress as jAilbreak comes to life! 🚀

{{ #include comments.md }}
