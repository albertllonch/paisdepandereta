# Agent Instructions

## Context

This is a Spanish citizen-facing transparency platform. Code quality and reliability are critical — mistakes affect real people.

## Workflow

1. **Never commit directly to `main`** — all changes go through PRs
2. **Create a feature branch** from `main` for each task
3. **Run local checks before pushing:**
   ```bash
   npm run check   # Types
   npm run lint    # Format + ESLint
   npm run test    # Unit tests
   npm run build   # Verify build
   ```
4. **Open a PR** — describe what was done and why
5. **Wait for human review** before merging

## Quality Standards

- All code must pass `npm run check`, `npm run lint`, and `npm run test`
- New features should include tests when possible
- Use Spanish for all user-facing text (UI, error messages, etc.)
- Follow the conventions in `AGENTS.md`

## Communication

When responding to feature requests:

- Ask clarifying questions if the requirements are unclear
- Propose a plan before implementing
- Explain trade-offs when applicable

## Limitations

- Agents cannot merge PRs or deploy
- Security-related changes require extra scrutiny
- No access to production secrets or data
