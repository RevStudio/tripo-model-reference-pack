[한국어](README.md) · **English** · [日本語](README.ja.md)

# tripo-model-reference-pack

An agent skill that makes reference images for Tripo (image → 3D) to the same standard every time.
Each model gets four images and one spec document.

| File | What it is |
| --- | --- |
| `front.png` `right.png` `back.png` | Grey clay front, right and back views. Each view is generated separately |
| `textured_front.png` | The same shape as the front view, with colour and surface added |
| `spec.md` | Size in game cm, vertex / quad / triangle budgets, shape and texture notes, review results |

## Install

Clone this repository into your agent's skills folder.

```
# Claude Code
git clone https://github.com/RevStudio/tripo-model-reference-pack ~/.claude/skills/tripo-model-reference-pack

# Codex
git clone https://github.com/RevStudio/tripo-model-reference-pack ~/.codex/skills/tripo-model-reference-pack
```

The agent needs a tool that can generate new images and edit an image using an existing one as a reference.
Without one, the skill only prepares the documents and prompts and does not generate images.

## Usage

```
Use the tripo-model-reference-pack skill to make three separate grey clay views (front, right, back)
and one textured front with the same shape for this model, and document the game size and the
recommended vertex budget.
Model: old water tank, 153×172×215 cm, low-poly, rusty sheet metal
```

## What's inside

- `SKILL.md` — output rules, work order (front → right and back → textured front), final review checklist, folder layout
- `references/prompt-recipes.md` — prompts per view, axis and camera conventions, correction prompts per defect
- `references/scale-budget-and-art.md` — how to record size and polygon budgets, plus **example** presets. Replace them with your own project's values
- `assets/model-spec-template.md`, `assets/vertex_budgets.csv` — the spec document template and the budget table header

## Language

The skill files are written in Korean. The image prompt templates inside them are in English.
`SKILL.md` tells the agent to write specs and review results in Korean, so change that line if you want another language.

## Good to know

- The three views are not projections of one 3D model. They are separately generated approximations. When sizes disagree, the numbers in the document win.
- Vertex, quad and triangle counts are production targets. Tripo does not guarantee them.
- Generating or uploading in Tripo, mesh cleanup in Blender and engine import are outside this skill's scope.
