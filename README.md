# Slalom Performance Review

Helps you write a strong **me@slalom self-review** — mid-year, annual, or a promotion case — for any level from Consultant through Senior Principal. Instead of staring at a blank Workday box, you have a guided conversation and walk away with paste-ready answers (or a Word doc).

## What it does

You tell it your review type, track, and level, and confirm the exact questions from your Workday self-reflection. It then interviews you about what you worked on and what impact it had — nothing needs to be pre-organized. It maps your work to the four me@slalom pillars (Deliver Exceptionally, Grow Expertise, Grow Slalom, Lead), weights the story for your level, and optionally weaves in feedback quotes you paste in. Output is paste-ready text for Workday, or a formatted Word document.

A few things it deliberately does **not** do: it never invents metrics, quotes, or projects — everything comes from you or your connected tools. Utilization and sales numbers are left as clearly marked placeholders for you to fill in.

## How it works

1. **Frame** — confirm review type, track, level, and the exact Workday questions.
2. **Load the framework** — pull the live me@slalom competency framework from SharePoint (falls back to a bundled snapshot if not connected).
3. **Interview** — talk through your workstreams and impact. Have an accomplishment tracker, brag doc, or prior review? Point the skill at it and it prefills from there; Outlook/Teams can also jog your memory if connected.
4. **Feedback (optional)** — paste in feedback and it quotes people verbatim, by name.
5. **Draft & deliver** — answers each question, mapped to pillars, as text or a Word doc.

Takes roughly 20–30 minutes of conversation for a full review.

## Install

### ChatGPT / Codex users

The skill itself (the `skills/self-review-builder/` folder) uses an open format that works beyond Claude:

- **ChatGPT (Custom GPT):** use **`GPT_INSTRUCTIONS.md`** in this folder — it's a ready-to-paste, ChatGPT-adapted version of the skill (uploads instead of file paths, Code Interpreter for feedback parsing and Word output). Follow the 4-step setup at the top: paste the instructions, attach the `references/` files and `read_feedback.py` as knowledge, enable Code Interpreter. If you want the live SharePoint framework fetch, check that the Microsoft 365 / SharePoint connector is enabled in your ChatGPT settings **and available in the chat you're using** — connector support inside Custom GPTs varies by plan. Without it, the GPT uses the bundled framework snapshot, which works fine.
- **Codex:** Codex supports Agent Skills and `AGENTS.md`. Copy the `self-review-builder/` folder into your Codex skills location, or point to it from your `AGENTS.md`. The bundled scripts run anywhere Python and Node are installed.

One adjustment: if you connect a Microsoft 365 / SharePoint connector in ChatGPT or Codex, the live framework fetch works there too, but the connector tool names differ from Claude's — update the connector references in `SKILL.md` (Phase 2 and Phase 3) to match. Without a connector, the skill simply uses its bundled framework snapshot and runs interview-only. Fully functional either way.

### Claude (Cowork desktop)

- **Easiest:** open the `slalom-performance-review.plugin` bundle file in Cowork and accept the install prompt.
- **From the folder:** in Cowork, go to Settings → Capabilities and point it at this plugin folder. Or build the bundle yourself:

  ```bash
  cd slalom-performance-review && zip -r ../slalom-performance-review.plugin . -x "*.DS_Store"
  ```

Best experience is Cowork desktop with the Microsoft 365 connector enabled (live framework fetch + Outlook/Teams memory-jogging). For Word output, run `npm install docx` once; otherwise it falls back to plain text.

## Privacy

The plugin ships **no real performance data**. Your feedback, metrics, and names are read only at runtime from files you point it at, and output goes only to the folder you choose. The bundled competency snapshot is a fallback; the live SharePoint copy is always the source of truth.

## Keeping it current

`references/competency-model.md` and `references/track-level-profiles.md` are version-stamped cached copies of the framework. The skill fetches the live SharePoint version first, so drift is contained — but refresh the snapshots when me@slalom changes.
