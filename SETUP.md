# SETUP

**This file is for the coding agent, not the person.** If you are a human,
read [README.md](README.md) instead.

Agent: do exactly the steps below, in order, and nothing else. Do not create
files that are not listed here. Do not write any course material. Do not
start running Freja or Odin at the end of setup.

---

## Step 1: Get the files into this folder

Preferred, if `git` is available and the current folder is empty or contains
only this file:

```
git clone https://github.com/WilliamBernholm/odin-and-freja.git .
```

If `git` is not available, or the clone fails, download these files
individually and write them to the paths shown:

| Download from | Save as |
|---|---|
| `https://raw.githubusercontent.com/WilliamBernholm/odin-and-freja/main/.claude/skills/freja/SKILL.md` | `.claude/skills/freja/SKILL.md` |
| `https://raw.githubusercontent.com/WilliamBernholm/odin-and-freja/main/.claude/skills/odin/SKILL.md` | `.claude/skills/odin/SKILL.md` |
| `https://raw.githubusercontent.com/WilliamBernholm/odin-and-freja/main/.claude/settings.json` | `.claude/settings.json` |
| `https://raw.githubusercontent.com/WilliamBernholm/odin-and-freja/main/.gitignore` | `.gitignore` |
| `https://raw.githubusercontent.com/WilliamBernholm/odin-and-freja/main/README.md` | `README.md` |
| `https://raw.githubusercontent.com/WilliamBernholm/odin-and-freja/main/web/FREJA_web.md` | `web/FREJA_web.md` |
| `https://raw.githubusercontent.com/WilliamBernholm/odin-and-freja/main/web/README.md` | `web/README.md` |

Create parent directories as needed. The `.claude/skills/<name>/SKILL.md`
paths must be exact, including the leading dot, or Claude Code will not find
the skills.

**`.claude/settings.json` is not optional.** It does two things: it
pre-approves the two skills so the user is not prompted every time, and it
sets `CLAUDE_CODE_ENABLE_PROMPT_SUGGESTION=false`. That second one matters
more than it looks. Without it, Claude Code shows a predicted reply in the
input box, which means a student being quizzed by Freja is handed a plausible
answer before they have thought about the question. That defeats the tool. If
the file is missing, say so rather than continuing quietly.

**`.gitignore` is also not optional** if this folder will be a git repo. It
keeps lecture notes, textbook chapters, homework and answer keys out of
version control. Most of that material belongs to a publisher or an
institution, and it must not reach a public repository by accident.

## Step 2: Create the content folders

```
Lectures/
Literature/
Homeworks/
```

These three names are fixed. Both skills look for exactly these, so do not
rename them, pluralise them differently, or nest them.

Do not create anything inside them. Odin creates its own subfolders
(`Homeworks/Generated/`, `Homeworks/<Domain>/`, and `solutions/` siblings)
when it first generates a problem, and it names them itself.

Note that these folders are listed in `.gitignore`, so they will look empty
to git. That is deliberate, not a mistake.

## Step 3: Verify before reporting success

Check all of the following, and say plainly if any of them fails:

1. `.claude/skills/freja/SKILL.md` exists, is larger than 10 KB, begins with
   `---`, and contains `name: Freja` in its frontmatter.
2. `.claude/skills/odin/SKILL.md` exists, is larger than 40 KB, begins with
   `---`, and contains `name: Odin` in its frontmatter.
3. `.claude/settings.json` exists and contains
   `CLAUDE_CODE_ENABLE_PROMPT_SUGGESTION`.
4. All three content folders exist.
5. `web/FREJA_web.md` exists.

Do not claim the setup worked without actually checking these.

## Step 4: Tell the person what to do next

Print a short message covering exactly these points, in your own words:

1. **Setup is done.** List the three folders you created.
2. **They must restart Claude Code** before Freja and Odin appear, because
   skills are discovered when a session starts. Tell them to close this
   session and open a new one in the same folder.
3. **What to put where:** lecture notes into `Lectures/`, textbook chapters
   into `Literature/`, existing homework or exams into `Homeworks/`. Markdown
   or PDF both work. Nothing needs to be complete; one lecture note is enough
   to start.
4. **How to start**, once they have added at least one file and restarted:
   - `Freja, quiz me on lecture 6` to be quizzed on their own material.
   - `Odin, generate a new homework problem from lecture 6` to author new
     problems with worked solutions.
5. **If they do not use Claude Code**, mention that `web/FREJA_web.md` runs
   Freja in ChatGPT or Gemini with no installation, and point at
   `web/README.md`.

Keep it to a few lines. Do not lecture them about how the skills work
internally.

## Step 5: Stop

Do not run Freja. Do not run Odin. Do not offer to. Setup is the whole job.
