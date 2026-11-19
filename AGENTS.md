# For an AI assistant that was handed this repository

Your user wants the Lapidary skill installed. It is one folder, `skills/lapidary/`, holding `SKILL.md`. Read that file first, then install it for the tool you are:

- **Claude Code:** `/plugin marketplace add hvmidwvli/lapidary`, then `/plugin install lapidary@lapidary`. Or copy the folder to `~/.claude/skills/lapidary/`.
- **Codex (CLI, IDE) or the ChatGPT desktop app:** copy the folder to `$HOME/.agents/skills/lapidary/` (user scope) or `<project>/.agents/skills/lapidary/` (one project). On Windows, `$HOME` is the user's profile folder (OpenAI's page gives the path without spelling out Windows; check it exists afterwards). The user then invokes it with `$lapidary` (Codex) or `@lapidary` (ChatGPT app).
- **A tool with no skills folder:** paste the body of `SKILL.md` (everything after the second `---`) into a new chat or custom instructions, then paste the request after it.

Confirm the skill is listed (in Codex, `/skills`) before telling the user it works. Don't claim it is installed if you could not check.

## How to run it when the tool is not Claude Code

`SKILL.md` was written for Claude Code. Read it with these translations:

- `$ARGUMENTS` is the user's message after the skill name. If the message contains `--copy`, use copy mode.
- If the user wrote nothing after the skill name, use their previous message as the request.
- Claude Code's `AskUserQuestion` option cards do not exist here. Use the file's own fallback: numbered plain-text questions below the prompt block, then stop and wait.
- Ignore the front-matter lines `argument-hint` and `disable-model-invocation`. If the user wants the skill to run only when called by name, add `agents/openai.yaml` beside `SKILL.md` with `policy:` and, indented under it, `allow_implicit_invocation: false` (OpenAI's documented setting).

Source for the Codex and ChatGPT facts above: <https://learn.chatgpt.com/docs/build-skills> and OpenAI's Help Center page on skills. Where those pages are silent, this file says so rather than guessing.

## Don't

- Don't edit `SKILL.md` unless the user asks. Report a problem instead of silently changing the skill.
- Don't send the user's requests anywhere. The skill itself makes no network calls.
