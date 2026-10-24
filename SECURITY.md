# Security policy

## Reporting a problem

If you find a security problem in Docket, please report it privately. **Do not open a public issue or discussion**, since that would show the problem to everyone before it is fixed.

Use either:

- **GitHub:** the **Security** tab of this repository → **Report a vulnerability**. Only the Docket team can see the report.
- **Email:** docket@polestartechno.com, with "Security" in the subject.

Please include:

- the Docket version (Command Palette → **Docket: About**) and your editor and operating system;
- what an attacker could do, and what they would need first (for example, a project folder they control);
- the steps to reproduce it, or a small example.

## What happens next

- We confirm we received your report within **3 working days**.
- We tell you whether we can reproduce it, and how we plan to fix it, within **10 working days**.
- We fix confirmed problems in a new version as soon as we can, and name you in the release notes if you'd like.

Please give us a reasonable time to release the fix before you talk about the problem publicly.

## In scope

Problems in the Docket extension itself, for example:

- a task, plan or attachment that makes Docket run code or open files it shouldn't;
- a way around Restricted Mode (an untrusted folder changing settings or starting an agent);
- Docket exposing data from one project to another, or outside your computer.

Problems in the AI agents themselves (Claude Code, GitHub Copilot, Codex and others) belong to their makers. If you're unsure, report it here and we'll pass it on.

## Supported versions

Security fixes go into the latest version only. Keep Docket updated: VS Code and Cursor update extensions automatically unless you turned that off.
