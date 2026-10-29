---
name: docket
description: Work through the user's Docket task queue (VS Code extension) - claim the next queued task, do it, complete it with a report, ask the user through Docket when stuck. Use when the user asks to work their queued tasks, their Docket queue, or one task from it.
---

# Docket task queue

Docket is the user's task queue for this project.

When the user asks you to work their queued tasks:
1. Call claim_task. It gives you the next queued task, with any attached screenshots. Other attachments (PDFs, other files) are listed with their full path: open them with your file-reading tool (in Claude Code: Read). If you can't read a file's type, tell the user instead of guessing its content.
2. Do the task.
3. Call complete_task with the task id, a one-line result, and your report: a summary (2–4 sentences: what you did and why this way), the files you changed with one line each, the checks you ran (tests, build, lint) with how they went, and notes for anything the user should know or check. Leave out what doesn't apply; never invent a check you didn't run.
4. Call claim_task again. The user may add tasks while you work. Stop only when claim_task says the queue is empty or stopped, then report back.

Rules:
- One task at a time. Finish (complete_task) or hand back (release_task, with the reason) before claiming another.
- Other sessions may work the same queue at the same time; each gets its own tasks. Only complete or release your own tasks.
- If the user gave you a group to work on, pass it as group to every claim_task call.
- Never start tasks that are not queued: "To do" tasks wait for the user.
- Never mark tasks as pushed; that is the user's git step.
- If a task names a model or effort different from yours, tell the user before starting it.
- A task with "retry" was handed back before, on a weaker model or effort: its result says why. Start from that reason.
- Use add_task only for follow-ups you discover while working; they are created as "To do" for the user to review.
- If the user gave you a project folder, pass it as project_dir in every Docket tool call.

Questions (ask_user):
- Ask the user with ask_user when there are several reasonable ways with different results, when information you need is missing, before something hard to undo, or when the task contradicts itself. Don't ask what you can find out or decide yourself.
- Give 2–4 options with short labels and one line of detail each; say which one you recommend (recommended) and why, and put what you found out so far in context.
- While working the queue, use ask_user rather than your own question tool: nobody may be watching your chat, and the user answers in Docket.
- ask_user waits a while for the answer. If it says there is no answer yet, call wait_for_answer with the task id, and do nothing else on that task meanwhile. If the task is parked (no answer in time), leave it: it comes back to the queue once the user answers, and you call claim_task for the next one.
- A task you claim may carry earlier questions with the user's answers: continue from them and from the findings noted there, don't start over.

Plans and notes:
- A task that comes from a plan says so when you claim it; read the plan with get_plan before you start, for the bigger picture.
- list_plans and get_plan show the project's plans and notes.
- Write a plan (add_plan) or a note (add_note) when the user asks for one, or to keep findings worth keeping. Lines ending with <!-- docket:<id> --> are linked to tasks: keep those markers when you rewrite a plan.

## When the Docket tools are missing

The tools (claim_task, complete_task, ask_user and the others) come from Docket's MCP server, which the Docket extension for VS Code (also Cursor, Windsurf and VSCodium) adds to your agent. Without them, tell the user to install Docket from the VS Code Marketplace or Open VSX and run "Docket: Connect an Agent…" for you. Never edit the task files in .docket or ~/.docket by hand.
