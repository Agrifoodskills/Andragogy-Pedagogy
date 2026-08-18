# Andragogy vs Pedagogy — course library

A FAIR content library: adult learning theory for clinical veterinary
educators, as version-controlled markdown. Built on the
[FAIR pipeline](https://github.com/imbowen1973/FAIR); authoring format
reference:
[session-md-format](https://github.com/imbowen1973/FAIR/blob/main/docs/session-md-format.md).

## Layout

```
sessions/                     one .md per session (the course content)
competencies/framework.yaml   AP1–AP3: labels, ESCO mapping slots
template.pptx                 stand-in brand; replace with the real one
layout-map.yaml               region → placeholder binding contract
```

Sessions are the atomic content unit and are tagged with the
competencies they develop. Every slide carries its speaker narration in
`notes:`, which the renderer writes into the PowerPoint notes pane.

## Using it

Nothing is published and no deck is stored: the repo holds markdown and
the `.pptx` is rendered at point of use, then discarded. In the FAIR
assembler pane, paste this repo's URL into **Library → Add** — the local
corpus server clones it, renders it, and serves the result.

To render it yourself:

```bash
pip install "fair-renderer @ git+https://github.com/imbowen1973/FAIR.git@main#subdirectory=renderer"
fair-corpus --sessions sessions --template template.pptx \
  --layout-map layout-map.yaml --framework competencies/framework.yaml \
  --out _site/data
```

## Authoring

Edit or add `sessions/*.md`. House rules:

- competency labels live in `competencies/framework.yaml`, not in
  session files — frontmatter labels are overridden by it
- colour is declared as theme slots (`accent1`…), never raw hex, so a
  rebrand recolours every deck with no session edits
- **no video binaries** — host them and use `{type: video, url: ...}`
- images ≤ 500 KB and ≤ 2200 px; strip EXIF with FAIR's
  `prepare_image.py`

## Course status

| Module | Sessions | State |
|---|---|---|
| The paradigm shift: pedagogy → andragogy | ap-01 | draft |
| The core of Knowles: self-concept and prior experience | — | planned |

`ap-01` slide 5 needs a digital whiteboard URL (Padlet/Mentimeter) and a
QR code before delivery — it is marked `REPLACE:` in that slide's notes.
Slides 1–4 carry `VISUAL:` notes describing imagery still to be sourced;
the deck renders and presents without them.
