---
name: cantina-prompt
description: Turn a user's text, scene idea, or screenplay excerpt into a Cantina (cantina.com) AI scene-generation prompt that follows Cantina's "Prompting 101" rules — creating a new prompt, correcting/revising one the user already wrote, or recreating a scene or line of dialogue that came out wrong (found by scene number, quoted dialogue, or description, with the user's description of the problem). Asks the user for any detail the rules need that the text does not supply. By default also writes a social-media title, description, caption and tags for each new video; "social off" turns that off. A "full detail" switch (always on for recreated scenes) writes each scene as a fully standalone prompt — location, environment, positions, actions and two-way facing restated for every moment. Use when the user says "cantina prompt", "make a Cantina prompt", "turn this scene/screenplay into a prompt for Cantina", "fix/revise my Cantina prompt", "recreate/redo the scene/dialog where…", or types /cantina-prompt.
argument-hint: "<scene text, a prompt to fix, 'recreate <scene or line>: <problem>', or 'social on|off', 'detail full|standard'; add 'full detail' to any request>"
---

# Cantina scene prompt builder

Turn the user's text into one or more Cantina scene prompts that follow the rules in
[references/cantina-prompting-101.md](references/cantina-prompting-101.md).

## 0. Load the rules first

Read `references/cantina-prompting-101.md` in full before doing anything else. If it
is missing or empty, stop and tell the user the skill's rules file is missing; do not
write a prompt from guessed rules. Section K of that file (common failures and fixes)
also guides Recreate jobs (step 9).

## 1. Work out the job

From the user's input (`$ARGUMENTS`, or the text they pasted), decide which applies:

- **Create** — prose, an idea, or a screenplay scene: build a prompt from it.
- **Revise / correct** — the text is already a Cantina prompt: keep the user's intent,
  fix every place it breaks a rule, and list what you changed and why.
- **Recreate** — the user wants a scene or part of a video redone because it came out
  wrong ("recreate the dialog where…", "redo scene 2, they're facing the camera"):
  go to step 9.
- **Social switch** — the input is just `social off` / `social on`: go to step 8.
- **Detail switch** — the input is just `detail full` / `detail standard`: go to step 5b.

Any job can also carry the words "full detail" / `--full` (step 5b) or "no social" /
`--no-social` (step 8) for that request only.

A screenplay with several scenes (several sluglines, e.g. `INT. KITCHEN - NIGHT`) gets
one prompt per scene unless the user asks otherwise, and any scene that is too big for
Cantina's limits is split further (step 4b). Cantina's limits always beat a user's
request for fewer prompts. Keep scenes in order and keep each
character's description identical across scenes so they stay consistent.

Also decide the **prompt type**: an HQ video scene (the default for screenplays and
scenes), or a selfie in chat (opens with the word "selfie"). Ask only if unclear.

## 2. Pull out the scene elements

Extract everything the rules in the reference file ask for:

- **Cast:** every character in view, and their exact Cantina character name for the
  `@` tag (screenplay names like `MAYA` are not necessarily the Cantina names)
- **Action and dialogue**, in time order: who does what, who says each line, to whom,
  and how it is delivered
- **Who is in view** and **which way each character faces**
- **Location**, specifically
- **Tone and environment:** mood, sounds, light, weather, time of day
- **Moment changes:** new sluglines, time jumps, or place changes inside the scene
- Optional layers when the text gives them or the user wants them: wardrobe, camera
  (shot, angle, cuts, focus shifts, moves), lighting, color/atmosphere, finish

## 3. Ask for what is missing — never invent it

**Required — always ask when the text doesn't settle it:**

1. The exact Cantina character name to tag for each character (`@Name`). Always confirm
   these unless the user already wrote them as `@` tags.
2. The location, if not named or too vague ("a room" → which room, what's in it?).
3. Tone/environment, if none is given (offer a default built from the scene's mood).
4. Delivery for any dialogue line where how it's said matters and isn't clear.
5. Whether listeners are in view, when a character speaks and it's unclear (step 4).

**Optional — offer, don't require:** camera direction, wardrobe, lighting, color grade,
finish. Ask once in the same message, e.g. "Want camera direction (cuts, push-ins), or
should I leave the camera to Cantina?"

For each item the text does not answer, ask the user. Ask all missing items in **one** message, numbered, each with a short suggested
default the user can accept ("2. Time of day? (default: daytime)"). Use the
AskUserQuestion tool when the choices are few and clear; otherwise ask in chat.

Do not ask about things the text already settles, and do not ask about optional details
unless leaving them out would make the prompt break a rule. Wait for the answers before
writing the final prompt.

## 4. Speaker / listener facing rule (always applies)

Whenever one character speaks to other characters who are also in view, the prompt must
say explicitly that:

- the **speaker faces the listener(s)**, and
- **each listener faces the speaker**.

Write it into the prompt in plain words for every line or exchange (e.g. "Maya turns
to face Leo and Ana as she speaks; Leo and Ana face Maya, listening."). When the speaker
changes, update the facing for the new speaker and listeners.

Only skip or change this when the screenplay or the user says otherwise (e.g. "she says
it without looking up", "he speaks with his back to them", a voice-over, a phone call,
or a speaker who is off-screen). If it is unclear whether the listeners are in view,
ask in step 3.

## 4b. Fit each scene inside Cantina's limits (split where needed)

Cantina fails a scene (one prompt = one generation) that goes over any of these:
**6 unique tagged characters**, **3 dialogue turns**, or **50 words of dialogue**
(see section J of the reference file). Plan the scene list before writing:

1. **Untag the extras first.** Tag only characters who speak or do a specific action
   in that scene. Everyone else in view becomes untagged background ("the other
   students", "the class"). A tagged character who just sits and listens in a given
   scene is an extra *in that scene*, so leave them untagged there.
2. **Lay out the beats** in order: each dialogue turn (speaker + word count) and each
   tagged action, with the moment changes ("Cut to…", new place) between them.
3. **Walk the beats and start a new scene** as soon as adding the next beat would
   give a 4th turn, push dialogue past 50 words, or bring in a 7th unique tag.
   Prefer to split at a natural break that comes earlier: a location change, a
   "Cut to…", or a change of speaker. Never split in the middle of a sentence of action.
4. **Merge same-speaker quotes** in one moment into a single turn when that saves a
   turn: move the action in between to before the line ("@B forces a calm smile and
   says nervously: 'I'm just playing. Nothing happened. What clown is saying that?'").
   Keep the speaker's words; only join them.
5. **One line over 50 words:** split it at a sentence break into two scenes, and
   continue the second one with the same speaker, place and facing. Tell the user.
6. **Make each split scene stand alone.** Cantina doesn't carry anything between
   generations, so every scene restates its location, who is in view and the facing,
   and its own tone line. Open a continuation with its action, e.g. "@A, still at the
   podium facing the class, continues: '…'".
7. **Label the scenes** in order (1, 2, 3…, or 2a/2b for a split of the user's scene 2)
   so the user can see where you split and why.

## 5. Write the prompt

Follow the structure, order, syntax and wording rules in the reference file exactly.
Keep the user's story, dialogue and characters; change only what the rules require or
what the user's answers supply. Write it as one flowing prompt, in this order:

1. **Cast and opening action** — lead with the action; group characters who share it:
   `@A and @B lean on the counter of their food truck.`
2. **Facing + dialogue and delivery**, beat by beat, with an `@` tag on every action and
   line: `@A turns to face @B and says, grinning: "Line." @B faces @A, listening.`
3. **Location**, specific: `A silver food truck by a beach boardwalk, menu board lit up.`
4. **Specific moments** as their own sentences: `@B drops a whole tray of fries.`
5. **Moment changes** marked: `Cut to…`, `Later that night…`, `Back at the apartment…`
6. **Tone and environment** — sounds, mood, light, weather, time of day.
7. **Style stack last**, only if used: camera, lighting, color grade, finish.

Turn screenplay conventions into plain prompt language: sluglines become the location
and time of day, parentheticals become delivery, action lines become stacked verbs.
Drop scene numbers, `CONT'D`, `V.O.`/`O.S.` markers (but use them to judge facing).
Use concrete wording; replace vague phrases with specific ones from the user's text or
answers.

## 5b. Detail level: standard or full (standalone)

Cantina reads each prompt, and each moment inside it, on its own. Gaps — a "Cut to…"
with no location, "still at the desk" with no desk described, a listener whose facing
isn't stated — let it guess, and the guess is often wrong. **Full** detail closes every
gap.

**Which level applies** (first match wins):

1. The input says so: "full detail", "standalone", "detailed", `--full` → full;
   "standard detail", "short", `--standard` → standard.
2. **Recreate** jobs (step 9) → full, always, unless the input asks for standard.
3. `"detail"` in `config.json`: `"full"` or `"standard"` (default `"standard"`, also if
   the file or key is missing).
4. **Turning it on or off for good:** when the input is just `detail full` /
   `detail standard`, set `detail` in `config.json`, say which it is now, and stop.

**Standard** is everything in steps 4–5. **Full** adds, for *every moment* of the scene
(the opening and each "Cut to…", "Later…" or flashback):

- **Location, restated in full** at the start of the moment: the place, what's in it
  and where ("a school music classroom: upright piano at the front facing the class,
  rows of student chairs, posters of musical notes on the walls"), and the time of day.
  Never "the same room", "back in the classroom", or "still there" on its own.
- **Environment from earlier in the conversation, carried over word for word:** any
  light, weather, sounds, wardrobe or props already given for this place or character
  in earlier scenes or answers, so the scene looks the same without relying on them.
- **Who is in view and where:** every tagged character with their position ("@A sits
  on the edge of the teacher's desk on the left; @B stands by the door on the right"),
  and the untagged extras in one clause ("the other students sit at their desks").
- **What each tagged character is doing** at that moment, even if it's just "listening"
  or "standing still with arms crossed". No one in view without an action.
- **Facing on every line, both ways, by name:** "@A faces @B and says…: '…'
  @B faces @A, listening." With three or more people, name every listener, including
  untagged ones ("@C and the other students face @A"). Voice-over, phone or
  off-screen speakers say so explicitly ("is heard off-screen; no one on screen
  speaks").
- **Who is silent:** after each line, characters in view who must not speak say so
  ("@B stays silent"), so the lips move on the right person.
- **No pronouns or carry-over words** where a tag or noun fits: no "he", "they",
  "again", "the same", "as before".
- **Camera per moment:** the shot for each moment ("medium two-shot from the side,
  both in profile"), so framing isn't left to chance — unless the user said to leave
  the camera to Cantina.
- **Tone line per moment:** sounds, light and mood for each moment, not once at the end.

Full detail adds words to the prompt but not to the dialogue, so the step 4b limits
(tags, turns, dialogue words) are unchanged. Keep each added sentence short and
concrete. Label full-detail prompts `(full detail)` after the scene name.

## 6. Check before handing it over

Run the **Checklist** at the end of the reference file against each prompt and fix
anything that fails. Confirm the facing rule from step 4 is stated for every exchange
where it applies (untagged listeners count too: "the other students face @A").

Actually count, for each scene: unique `@` tags, quoted lines, and words inside the
quotes. If any count is over the limit, go back to step 4b and split again.

For a **full detail** prompt, also check every moment against the step 5b list:
location restated, everyone in view placed and given an action, facing both ways on
every line, silent characters named, no pronoun or "same/again/still" standing in for
a description, camera and tone given per moment.

## 7. Output

Give the user, in this order:

1. The finished prompt(s) in a fenced code block each, labeled by scene, ready to paste
   into Cantina. Under each label, one line of counts, e.g.
   `4 characters · 3 turns · 47 dialogue words`.
2. Where you split one of the user's scenes, one line saying where and which limit
   forced it.
3. For a revision: a short bulleted list of what changed and which rule required it.
4. Any assumptions you made from defaults the user accepted.
5. A one-line reminder to check each action in Cantina's Script view before generating,
   and to change cast, actions, locations or sounds together, then generate once.
6. The **social post** (step 8), when the switch is on and the job is Create.
7. When the prompts are at standard detail, one line: "If a scene comes out wrong, ask
   for it again with `full detail`."

## 8. Social post: title and description (automatic, can be switched off)

**The switch.** Read `config.json` in this skill's folder. `"social_post": true` (the
default, and what to assume if the file is missing or unreadable) means: write the
social post after the prompts of every **Create** job. Skip it for Revise and Recreate
jobs unless the user asks for it.

- **Per request:** "no social", "no title", "skip the description" or `--no-social`
  in the input skips it this time; "with social", "add a title" or `--social` adds it
  this time even when the switch is off or the job is a Revise/Recreate.
- **Turning it on or off for good:** when the input is just `social off` / `social on`
  (or "turn off/on the titles and descriptions"), set `social_post` in `config.json`
  to `false` / `true`, say which it is now, and stop. Write no prompt.
- One line under the post reminds the user of the switch, e.g.
  "Turn these off with `/cantina-prompt social off`."

**What to write.** One post for the whole video (all its scenes together), not one per
scene, written from the story rather than from the prompt text:

1. **Title:** 3 options, the recommended one first. At most 100 characters each (the
   YouTube limit). If the user has a series name and episode number in this
   conversation, use the form `<Series> Ep. <n>: <hook>`.
2. **Description:** 3–6 short lines: the setup, the hook, and a line that teases the
   ending without giving away the twist or punchline. Then the series line, if any.
   End with 3–5 hashtags.
3. **Short caption** (TikTok / Instagram / Shorts), at most 150 characters, with 1–2
   emoji.
4. **Tags:** 8–12 comma-separated search tags.

**Rules for the post:**

- Keep the twist hidden (no emoji or word that gives it away). Mention the twist in a
  note to the user when it's easy to spoil.
- Use only names from the story (character names as the story says them, not the
  `@` handles). No real brand, company or celebrity names; no song lyrics.
- Add one reminder line: the video is AI-generated, so answer **Yes** to YouTube's
  "altered or synthetic content" question, and pick the audience setting yourself
  ("made for kids" turns off comments).

## 9. Recreate a scene or part

The user asks to redo a piece of a video that came out wrong, naming the piece and the
problem, e.g. "recreate the dialog where he said hello. Characters are all standing
facing the camera and not each other when talking."

**1. Find the piece.** The user can point to it in any of these ways:

- a **scene label or number** ("scene 2b", "the second scene");
- a **line of dialogue**, quoted exactly or roughly ("where he said hello", "the
  'let's jump him' part"): match it against the quoted lines, ignoring case and
  punctuation, and pick the closest;
- a **description** of the moment ("the part where he falls off the rope").

Look for it in the prompts written earlier in this conversation, or in a prompt or file
the user pasted or attached. If it matches more than one place, or nothing, show the
candidates (scene label + the line) and ask which one. If there is no source prompt at
all, ask the user to paste the scene's prompt. Never rebuild a scene from memory.

**2. Name the cause.** Turn the user's description of the problem into what in the
prompt let it happen. Common problems and fixes:

| Problem in the video | Fix in the prompt |
|---|---|
| Characters face the camera, not each other | State facing for speaker *and* every listener on that line; add "they face each other in profile, not looking at the camera"; add a side-angle two-shot or over-the-shoulder shot to the style stack |
| The wrong character says the line / lips move on the wrong person | Tag only the speaker on that line; add "@B stays silent, listening"; put the speaker's action right before the quote |
| A character is missing or appears twice | Tag them in the opening action and on every action; describe their position ("stands on the left") |
| An untagged extra steals the scene | Keep extras in one plain clause ("the other students sit at their desks") |
| A line is rushed, cut off or skipped | Fewer beats in that scene: split it so the line has its own scene, and cut turns or actions around it |
| An action doesn't happen | Give it its own sentence with stacked verbs, right where it happens in the sequence |
| Wrong place, time, look or mood | Make the location, light and tone lines concrete; repeat the same wardrobe words as the other scenes |

If the user's description does not say what is wrong clearly enough to fix, ask one
question about it, with your best guess as the default.

**3. Write the recreated prompt.** By default, recreate only the **part** the user
named, as its own short standalone scene they can cut into the video: the same
location, cast, wardrobe, light and tone wording as the original scene, so it matches,
plus just enough of the action before the line to set it up. Recreate the **whole
scene** instead when the user asks for it, or when the problem runs through all of it.
Keep the user's dialogue word for word. Write it at **full detail** (step 5b) unless
the user asks for standard: the original scene may have relied on things said earlier
in the prompt or in another scene, and that is often why it went wrong. Apply the
facing rule (step 4), the limits (step 4b) and the check (step 6) as usual.

**4. Output:** the recreated prompt in a code block, labeled after the original
(e.g. `Scene 2 (redo)` or `Scene 2 — "There he is" (redo)`) with its counts line;
then a short list of what changed and how each change fixes the problem; then the
Script view reminder. No social post unless the user asks.
