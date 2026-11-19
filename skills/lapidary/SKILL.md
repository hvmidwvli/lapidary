---
name: lapidary
description: Turns a dictated request into an expert prompt and runs it; --copy gives the prompt only. · Ore-to-Offer
argument-hint: "[--copy] [raw request — empty uses my previous message]"
disable-model-invocation: true
---

# Lapidary

Raw stone: $ARGUMENTS

The user dictates by voice. The requests carry real intent but arrive rough: misheard words, run-on sentences, the real goal buried mid-message, constraints scattered around. A specialist brief gets far better work out of a model than raw dictation does. Cut the rough stone into that brief without changing what it is.

## Mode

- `--copy` anywhere in the input → copy mode. Remove the flag; the rest is the request.
- Nothing left after removing flags → the request is the user's previous message in this conversation.

## 1. Repair

Fix misheard words and transcription errors from context: homophones, split or merged words, garbled names of tools, brands and places. List every such guess so a wrong one is easy to catch, e.g. `"delete once" → "delete the old ones"`. Mark a guess `(?)` when another reading would change the result. Plain grammar smoothing isn't a guess, so leave it out of the list.

## 2. Cut the prompt

Rebuild the request in this shape. Address the model as "you"; "I/me" is the user.

```
ROLE: You are a <seniority + specialty + domain>.
GOAL: <the outcome, one or two sentences>
SUCCESS: <how we'll know: numbers, deadlines, acceptance checks>
CONTEXT: <facts, files, links, accounts, prior work; label assumptions "Assumption:">
CONSTRAINTS: <every constraint, gathered from wherever it was said, plus legal/platform-terms limits that apply>
DELIVERABLES: <numbered, each with its format>
ASK ME FIRST: <only questions whose answer changes the result, or "Nothing — start.">
```

**Role.** Pick the one expert who would be hired for exactly this job, with years and a sub-domain: "social media marketing manager with 25 years of experience growing consumer brands on Instagram", not "marketing expert". If the user named a role, keep it and sharpen it. One role, not a committee; a blended role dilutes the voice.

**Fidelity.** The cut must stay the same stone:
- Keep the user's ambition. Targets stay exactly as stated; if one looks unrealistic, add a one-line baseline note in CONTEXT, never a lower goal.
- Add no scope. An extra that might help becomes a question in ASK ME FIRST, not a deliverable.
- Invent no facts. Unknowns become questions or labeled assumptions.

Keep it a brief, not an essay: usually 10–25 lines.

## 3. Show it

**Default mode** — show:

**Repairs:** the guesses on one line, or "none".
**Prompt:** the cut prompt in one fenced block.

Then decide:
- A `(?)` repair or a question in ASK ME FIRST → ask before starting, never only inside the block (questions there get missed). With a question tool (AskUserQuestion): one card per question or `(?)` repair, 2–4 options, your recommendation first and marked "(Recommended)", each readable on its own; then carry out the prompt with the answers. Without one: list them as numbered plain text below the block and stop.
- Otherwise write "Proceeding." and carry out the prompt in this chat, working as the role.

**Copy mode** — output only the prompt in one fenced block, nothing before or after. Put `(?)` guesses into its ASK ME FIRST so the chat that receives it asks the user. Don't carry it out.
