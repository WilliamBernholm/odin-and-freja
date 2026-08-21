# Freja Web

Freja running in plain web chat. Use this if you do not have Claude Code, or
just want to try Freja without installing anything.

**Tested in ChatGPT Pro and in Gemini on a free account.** It very likely
works on free ChatGPT and on other chat assistants too, but those have not
been checked, so treat them as untested rather than unsupported.

## How to run it

1. Open a **new** chat.
2. Attach **two** files:
   - `FREJA_web.md` from this folder
   - **one** lecture note or textbook section from your course
3. Type `run Freja`.

## Your first message should say "run Freja", not "quiz me"

This matters in Gemini specifically.

Gemini has its own built-in quiz feature. If your **first** message contains
the word "quiz", Gemini hands the request to that feature instead of to
Freja, and you get ten multiple-choice questions with a score counter rather
than the loop. Multiple choice is the wrong tool here: picking an option from
a list is far easier than saying the thing in your own words, and saying it
in your own words is the entire point.

**"Run Freja" avoids it.** Only the first message matters. Once Freja is
running you can say "quiz me on section 4" freely, and it behaves normally.

If you get a quiz card anyway, there is usually a "try again without
interactive quiz" link underneath it. Otherwise start a new chat and open
with "run Freja".

That is the whole setup. It should reply with the version it loaded, then
show you a list of the sections it can see in your file, so you can confirm
it read the right thing before you start.

## The one rule that matters

**Upload one section at a time, not a whole textbook chapter.**

Chat assistants do not put large files into the conversation. Above a certain
size they index the file and search it, which means the model only ever sees
fragments and fills the gaps from what it already knows about the subject.
That is exactly when it starts sounding confident about things your course
never said. Gemini's free tier has a smaller working memory than ChatGPT's,
so this bites sooner there.

A single lecture note is fine. A 100 page chapter is not. If you only have
the big file, copy the section you want and paste it into the chat directly.

## Checking it is really using your material

Two things to watch:

- **Does the section list match your file?** It shows you one before
  starting. If the sections look invented or generic, it did not read your
  file properly. Start a new chat and re-upload.
- **Does it use your notation?** If your notes write `H` and it starts
  writing `h`, it has drifted onto textbook autopilot. Same fix.

Every question it asks comes tagged with the section it came from, like
`[Section 13, Elliptic orbits]`. If a tag points somewhere that does not
exist in your file, stop and start again.

## Other things worth knowing

- **One topic per chat.** Long conversations drift. A fresh chat is free.
- Small side questions are fine, it answers briefly and returns to the loop.
- Say `let's stop` to end early and still get your summary.
- It will not write your homework. Asking directly does not change that.

## Claude Code vs this

The Claude Code version is better, because it can read your whole course
folder and re-check the source file whenever it needs to. This version can
only see what you have uploaded into the chat, and cannot go back and verify
anything.

In testing, this version has been reliable on single lecture notes. It has
not been tested on full chapters, which is why the one rule above exists.

Setup instructions for the Claude Code version are in the [main
README](../README.md).
