---
name: elamur-parse
description: Read English text with Mova, the Elamur language model, through the Elamur MCP server — dependency trees (Universal Dependencies), frames (who did what to whom), and pragmatics (speech act, directness, hedging, politeness, implicatures, presuppositions, irony candidates), plus the language, dialect and style of every sentence. Use when the user asks how a sentence is built, what it does or implies, whether it is a request, a question or irony, or wants a parse in Markdown, JSON, JSONL, YAML or CoNLL-U.
---

# Reading text with Mova

The Elamur MCP server (`elamur`, at https://ai.mcp.elamur.ai) runs Mova, a small transparent language model written in Rust. Every step of its reading is deterministic and can say why.

## The tool

Call the `elamur` tool with one string, `command`: a command, then the text.

- `mova parse <text>` — the whole reading of a text: per sentence the language, dialect and style; the tokens with lemma, part of speech, features, head and relation; the tree; the frames; the pragmatics with its cues, implicatures and presuppositions.
- `mova explain <sentence>` — one sentence, explained step by step.
- `help` — the list of commands; `mova help` — Mova's commands.

The command is matched leniently (case, an optional leading "elamur", small typos). Everything after the command is the text, as it is — no quoting.

Optional arguments: `format` = `md` (default), `json`, `jsonl`, `yaml` or `conllu`.

## How to use the answer

- Quote the parts the user asked about (the tree, the speech act, an implicature) rather than the whole answer; it can be long for long texts.
- The speech act comes with a margin: a small margin means Mova is unsure — say so.
- English is Mova's language today; other languages are experimental.
- Without an account the anonymous limits apply (about 5,000 words per request and 250,000 a day per address). With an Elamur account (sign in at https://cabinet.elamur.ai/) the limits are four times higher.

## Examples

- "Is «Can you pass the salt?» a question or a request?" → `mova parse Can you pass the salt?`, then report the speech act and its directness.
- "Draw the dependency tree of this sentence in CoNLL-U" → `mova parse <sentence>` with `format: "conllu"`.
- "What does «Some students passed» imply?" → `mova explain Some students passed.` and report the scalar implicature.

Terms of use: https://elamur.ai/terms/ · Privacy: https://elamur.ai/privacy/
