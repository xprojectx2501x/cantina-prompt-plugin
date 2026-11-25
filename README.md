# cantina-prompt-plugin

Easily check and enhance your prompts for cantina.com HQ Video generation to reduce
production time and increase accuracy of prompts.

A Claude skill that turns scene ideas, stories and screenplays into prompts for
[Cantina](https://cantina.com) AI videos.

## What it does

- **Writes scene prompts** with every character tagged, a concrete location, tone,
  and who faces whom on every line of dialogue.
- **Stays inside Cantina's limits** (6 tagged characters, 3 dialogue lines and 50
  dialogue words per scene) and splits long scenes for you.
- **Asks** for anything it needs instead of guessing (character names, location, tone).
- **Recreates a scene or line that came out wrong.** Point to it by scene number, by a
  line of dialogue, or by describing the moment, and say what went wrong:
  `/cantina-prompt recreate the dialog where he said hello. They face the camera, not each other.`
- **Full detail mode** writes each scene so it stands on its own: location, positions,
  actions and facing restated for every moment.
- **Social media post** for each new video: title options, description, short caption
  and tags.

## Install

### Claude Code

```
/plugin marketplace add xprojectx2501x/cantina-prompt-plugin
/plugin install cantina-prompt@cantina-prompt
```

### Claude app / claude.ai

Download `plugins/cantina-prompt/skills/cantina-prompt` as a zip and upload it in
**Settings → Capabilities → Skills**.

## Use

```
/cantina-prompt <your scene, story or screenplay>
```

| Switch | For one request | For good (Claude Code only) |
|---|---|---|
| Social post | add `no social` or `with social` | `/cantina-prompt social off` / `social on` |
| Detail level | add `full detail` | `/cantina-prompt detail full` / `detail standard` |

Recreated scenes always use full detail.

## Notes

The rules in `references/cantina-prompting-101.md` are written in this project's own
words, based on Cantina's
[Prompting 101](https://support.cantina.com/hc/en-us/articles/51897894449683-Prompting-101)
help article and on testing. This project is not affiliated with Cantina.
