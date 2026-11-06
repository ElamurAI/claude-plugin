# Elamur for Claude

This plugin connects Claude to **Elamur** through the Elamur MCP server at `https://ai.mcp.elamur.ai`: one server, one tool, many services, each a command. Today it carries **Mova**, the Elamur language model; more Elamur services, such as translation, join the same server as they open, and the plugin needs no change to use them (`help` lists what is there).

Mova is a small, transparent language model written in Rust. It reads English text into dependency trees (Universal Dependencies), frames — who did what to whom — and pragmatics: the speech act of every sentence, how direct it is, hedging and politeness, implicatures, presuppositions and irony candidates. It also tells the language, dialect and style of each sentence. Every step is deterministic and can say why.

## What is inside

- `.mcp.json` — the remote MCP server `elamur` (`https://ai.mcp.elamur.ai`, Streamable HTTP). It works without an account under anonymous limits; signing in to an Elamur account raises them.
- `skills/elamur-parse` — when and how Claude uses Mova.
- `commands/parse.md` — `/elamur:parse <text>` in Claude Code and Cowork.

## The tool

One tool, `elamur`, takes a command and the text: `mova parse <text>`, `mova explain <sentence>`, `help`. Answers are Markdown by default; `format` can be `json`, `jsonl`, `yaml` or `conllu`.

## Install

- Claude Code: `/plugin marketplace add ElamurAI/claude-plugin`, then `/plugin install elamur@elamur`.
- Or only the server: `claude mcp add --transport http elamur https://ai.mcp.elamur.ai`.
- claude.ai: Settings → Connectors → Add custom connector → `https://ai.mcp.elamur.ai`.

## Data

The texts you send are processed on Elamur's servers to answer you and are kept in a request log for 90 days; they may be used to improve Mova. Nothing is sent anywhere else. Details: [Privacy policy](https://elamur.ai/privacy/) · [Terms of use](https://elamur.ai/terms/). Documentation: https://mcp.elamur.ai/

## Licence

The plugin is under the Elamur Cosmic License (`LICENSE.md`). Its icon, the Elamur eye, is ours. Mova's code is open at https://github.com/ElamurAI/mova-free.
