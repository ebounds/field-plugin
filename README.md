# Field

**The shape of thinking together.**

Field is a Claude skill that expresses the accumulated tone of a whole conversation as one wordless SVG artwork. Claude reads the available exchange, forms a brief composition score, and chooses drawing controls under a shared visual grammar. A fixed titanium capsule anchors the image; around it, a translucent field gathers, sweeps, folds, and rejoins.

Field offers an interpretation of the conversation and the assistant's way of engaging with it. It makes no claim to directly measure internal state or answer quality.

This repository packages Field 4.6.0 as a Claude Code plugin. The skill under `skills/field/` is the unmodified [v4.6.0 release](https://github.com/ebounds/field/releases/tag/v4.6.0) of [ebounds/field](https://github.com/ebounds/field), where Field is developed.

## Install

```bash
claude plugin marketplace add ebounds/field-plugin
claude plugin install field@ebounds
```

## Use

In a substantive conversation, ask Claude to show Field, or invoke the skill directly with `/field:field`. Claude follows `skills/field/SKILL.md`, reviews the conversation, and renders one SVG.

Two things are optional:

- **Listening.** Ask Claude to include Field's listening companion for a 24-second musical phrase made from the same interpretation and controls.
- **Companion.** Ask Claude to keep Field present, and it publishes updated expressions to a small local viewer as the conversation continues.

You can also try the visual instrument without installing anything, in the [browser playground](https://ebounds.github.io/field/).

## What the plugin runs

The plugin contains one skill and no hooks, MCP servers, agents, or commands. Nothing runs until the skill is invoked. Everything runs on your machine, and the plugin needs no account, API key, or third-party package.

- **Image renderer.** `scripts/render_field.py` uses the Python 3 standard library and writes one SVG file to the path Claude gives it.
- **Audio renderer (optional).** `scripts/render_audio.mjs` needs Node.js 18 or later and writes one stereo WAV file. The sound is synthesized locally, without samples.
- **Companion (optional).** `scripts/field.mjs serve` starts a web server bound to `127.0.0.1` only, on port 8767 by default, and serves the bundled viewer pages in `docs/`. It stores the expressions Claude publishes, and an optional phase index, in a local `.field` directory until you delete it. The `publish` and `read` commands talk only to that local server and refuse any other address. The server does not read transcripts or call a model.

The plugin sends no data to any external service and has no telemetry. The bundled viewer pages contain ordinary links to the Field website and its GitHub repository, which open only if you click them.

## Requirements

- Python 3 for the image.
- Node.js 18 or later for listening and the companion.

## More

- [Illustrated reading guide](https://ebounds.github.io/field/field-guide.pdf), also bundled at `skills/field/docs/field-guide.pdf`
- The visual grammar, synthesis procedure, and continuity protocol, in `skills/field/references/`
- Source and feedback: https://github.com/ebounds/field

Created by Edgar Bounds. MIT licensed; see `LICENSE`.
