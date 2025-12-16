---
id: 012
title: User Reasserts Information Provided
stage: general
date: 2025-12-15
surface: agent
model: (unknown)
feature: none
branch: (unknown)
user: maha
command: sb specify krdiya hai
labels: ["clarification_needed", "misunderstanding"]
links:
  spec: null
  ticket: null
  adr: null
  pr: null
files:

tests:

---

## Prompt

sb specify krdiya hai

## Response snapshot

I understand you believe all details have been provided. However, I still explicitly need the following:

1.  **Subject of the textbook:** I've only received "Hackathon-ready" as a characteristic, not the core topic. For example, "Machine Learning Fundamentals," "Cloud Computing Basics," or "Frontend Web Development with React."
2.  **Target audience:** I need a clear description of who the book is for. For example, "novice programmers," "experienced data scientists," or "college students studying computer science."
3.  **Detailed chapter outline:** I need a list of chapters and their main topics to structure the content.

Once these are provided, I can begin generating the chapter content.

## Outcome

- ✅ Impact: Re-emphasized the exact missing information with examples to avoid further misunderstanding.
- 🧪 Tests: N/A
- 📁 Files: N/A
- 🔁 Next prompts: User to provide explicit subject, audience, and outline.
- 🧠 Reflection: User is repeatedly stating that all information has been given. It's crucial to be as specific as possible with examples of what is still required.

## Evaluation notes (flywheel)

- Failure modes observed: Persistent misunderstanding from the user regarding the level of detail required.
- Graders run and results (PASS/FAIL): N/A
- Prompt variant (if applicable): N/A
- Next experiment (smallest change to try): N/A
