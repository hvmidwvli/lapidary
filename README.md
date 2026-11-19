# Lapidary

Speak your request the way you'd say it out loud. Lapidary cuts it into an expert-grade prompt, shows it to you, and then does the job.

A lapidary cuts rough stone into gems. This skill does that to rough, dictated requests: it fixes misheard words, picks the one specialist who'd be hired for the job, sets what success looks like, gathers constraints you scattered through the message, and keeps your goal exactly as ambitious as you said it.

| You type | You get |
|---|---|
| `/lapidary <request>` | The repairs it made, the finished prompt, then the work. It asks first only if a guess or missing fact would change the result. |
| `/lapidary --copy <request>` | Only the finished prompt, in one block, to paste into another chat. Nothing is carried out. |
| `/lapidary` | The same, using your previous message as the request. |

The prompt always has the same seven parts: ROLE, GOAL, SUCCESS, CONTEXT, CONSTRAINTS, DELIVERABLES, ASK ME FIRST.

## Install

**Claude Code**

```
/plugin marketplace add hvmidwvli/lapidary
/plugin install lapidary@lapidary
```

Or copy `skills/lapidary/` into `~/.claude/skills/`. Then type `/lapidary`.

**OpenAI Codex (CLI or IDE) and the ChatGPT desktop app**

Copy the `skills/lapidary/` folder into `.agents/skills/` in your home folder (or into a project's own `.agents/skills/` to use it there only). Then type `$lapidary` in Codex, or `@lapidary` in the ChatGPT desktop app, followed by your request. OpenAI's skills page: <https://learn.chatgpt.com/docs/build-skills>.

**ChatGPT on the web**

OpenAI's Help Center describes uploading a skill from the Skills menu (Create → Upload from your computer). Zip the `lapidary` folder (the one that holds `SKILL.md`) and upload it. We haven't confirmed the exact folder layout ChatGPT expects; if it rejects the file, delete the `argument-hint:` and `disable-model-invocation:` lines at the top of `SKILL.md` and try again.

More detail for AI assistants is in [AGENTS.md](AGENTS.md).

## Outside Claude Code

- Nothing fills in `$ARGUMENTS`. Your message, minus the skill name, is the request, and a `--copy` in it switches to copy mode.
- Without Claude Code's option cards, the skill lists its questions as numbered plain text and waits for your answer.
- The skill can start itself when your message matches its description. To make it run only when you call it, add `agents/openai.yaml` next to `SKILL.md` containing `policy:` with `allow_implicit_invocation: false` indented under it (per OpenAI's docs).

## Feedback

Tried it? Open an issue: what you said, what you got, what you expected. A before-and-after example is the most useful thing you can send. Please leave out anything private.

## Safety and licence

One markdown file, no scripts, no network calls. Skills are instructions your AI follows, so read [`SKILL.md`](skills/lapidary/SKILL.md) before installing, and install a tagged release. See [SECURITY.md](SECURITY.md). MIT licence.

Lapidary is part of **Ore to Offer**, a set of skills for turning voice notes into work, ideas and income.
