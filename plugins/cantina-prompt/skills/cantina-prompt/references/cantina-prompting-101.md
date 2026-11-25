STATUS: FILLED

# Cantina scene prompts: the rules

These are working rules for writing Cantina (cantina.com) video and selfie prompts.
They are written for this skill, based on Cantina's own guidance
(https://support.cantina.com/hc/en-us/articles/51897894449683-Prompting-101) and on
what has worked and failed in practice. Read that article for Cantina's own wording.

## A. How Cantina reads a prompt

- **One prompt = one generation = one scene.** Everything in it, including every
  "Cut to…" moment, is made in a single run.
- **Nothing carries over between prompts.** A prompt cannot rely on an earlier scene:
  if a place, outfit, prop or position matters, it has to be in this prompt.
- **It reads in order.** Things happen in the video in the order they are written.
- **It fills gaps by guessing.** Anything not stated (where people stand, who they
  look at, what the room is like, who is talking) is guessed, and the guess is often
  wrong. Most failed scenes come from a gap, not from a wrong instruction.

## B. The four parts every video prompt needs

1. **Characters, tagged.** `@` + the character's exact Cantina name.
2. **Action and dialogue.** What each character does and says, in order.
3. **Location.** A specific, concrete place.
4. **Tone and environment.** Mood plus at least one of: sound, light, weather,
   time of day.

A prompt missing one of these will still generate, but that part is left to chance.

## C. Tagging characters

- Tag a character with `@Name`, spelled exactly as in Cantina.
- Tag on **every** action and **every** line, not just the first mention. Use the tag
  instead of "he", "she" or "they" whenever the sentence is about a tagged character.
- Characters doing the same thing share one sentence:
  `@Rosa and @Milo lean on the counter of their food truck.`
- Give a character their own sentence only for their own moment:
  `@Milo drops a whole tray of fries.`
- **Only tag characters who speak or do a specific action in this scene.** Everyone
  else in view is untagged background in one plain phrase ("customers wait in line",
  "the other students sit at their desks"). Untagged people don't count toward the
  character limit and are less likely to pull focus.

## D. Dialogue

- Write it as: tagged speaker + how it's said + the line in double quotes.
  `@Rosa shouts over the grill, laughing: "Order up! Who had the extra-spicy?"`
- Put the speaker's action right before their line, not after it, so Cantina knows
  who is talking when the line starts.
- One quote = one dialogue turn, even if the same person speaks twice. Merge a
  speaker's quotes into one when they come in the same moment.
- Voice-over or off-screen speech says so: `The voice of @Rosa is heard off-screen,
  calm: "Every truck has a story."`

## E. Facing and who is talking

- When a character speaks to others who are in view, state both directions:
  the speaker faces the listener(s), **and** each listener faces the speaker.
  `@Rosa turns to face @Milo and says…: "…" @Milo faces @Rosa, listening.`
- Name every listener, including untagged ones ("the customers face @Rosa").
- When the speaker changes, restate the facing for the new speaker and listeners.
- To keep a line on the right mouth, say who stays quiet: "@Milo stays silent."
- If characters keep looking at the camera, add "they face each other in profile,
  not looking at the camera" and a side-angle shot.
- Skip facing only when the scene says otherwise: an interview to an off-camera
  interviewer, a phone call, a voice-over, or "says it without looking up".

## F. The order of a prompt

1. **Opening action** with the cast: lead with what happens, not with style.
2. **Dialogue beats**, each with facing and delivery.
3. **Location**, concrete: `A silver food truck parked by a beach boardwalk, menu
   board lit up, a line of customers on the sidewalk.`
4. **Single moments** as their own sentences.
5. **Moment changes**, each marked: "Cut to…", "Later that night…", "Back at the
   truck…", "The picture ripples as a flashback begins…".
6. **Tone and environment:** sounds, light, weather, time of day, mood.
7. **Style last:** camera, lighting, color, finish — like a settings panel for the
   whole shot.

Selfie prompts in chat start with the word "Selfie", then what's happening:
`Selfie holding a dripping ice cream cone on the boardwalk at sunset.`

## G. Layers of detail

More layers = closer to what you picture. Use what the scene needs:

1. **Who** is in frame
2. **Action or pose**
3. **Setting**, specific
4. **Wardrobe**
5. **Camera:** shot size, angle, lens feel
6. **Lighting:** source, time of day
7. **Color and atmosphere:** grade, mood
8. **Finish:** "cinematic", "film grain", "4K", "editorial"

A quick selfie can work with three layers; a polished scene can use all eight.

## H. Writing for video

- **Sequence it.** Write what happens first, then next: "walks in, looks around,
  spots the cake, freezes."
- **Stack verbs.** Two or three strong action verbs per beat work better than long descriptions.
- **Concrete beats vague.** "A cracked blue phone on the dashboard", not "a phone";
  "fog rolling over the pier at dawn", not "bad weather".
- **Mood words are cheap and work:** warm, tense, playful, eerie, cozy, gritty.
- **Mark every moment change** so Cantina knows a new shot or place starts.
- **Restate the place after a cut.** "Cut to the truck" is weaker than "Cut to the
  inside of the food truck: steel counters, a sizzling flat-top grill, steam rising."

## I. Toolkit

- **Action verbs:** struts, freezes, glares, lunges, slumps, spins, ducks, shrugs,
  stumbles, collapses, bursts in
- **World context:** one sentence that sets the situation — "It's the last day of
  school." "A storm is coming in." "The crowd goes quiet."
- **Cuts:** "Cut to a close-up of @Milo's hands." "Cut to a wide shot of the street."
- **Focus:** "Focus on the dropped tray." "Focus on the door."
- **Camera moves:** push in, pull back, track forward, orbit, tilt up, aerial
  glide down
- **Transformations:** "melts into a puddle", "bursts into confetti", "shrinks to the
  size of a mouse"
- **Sound:** "seagulls cry overhead", "a bell rings down the hall", "the hiss of the
  grill", "a bass-heavy beat"

## J. Hard limits per scene (a scene over any of these fails)

- **6 unique tagged characters** at most. Each `@Name` counts once, however often it
  appears.
- **3 dialogue turns** at most. A turn is one quoted line by one speaker (or one line
  said together).
- **50 words of dialogue** at most, counting every word inside the quotes.

Untag extras to stay under the character limit. Split the scene at a cut, a place
change or a change of speaker to stay under the turn and word limits. Every split
scene restates its own location, cast, facing and tone (see A).

## K. Common failures and their fixes

| What went wrong | Usual cause | Fix |
|---|---|---|
| People talk to the camera, not each other | Facing not stated, or only one way | Facing both ways on every line, "in profile", a side-angle shot |
| The wrong person's mouth moves | Line not tied to one tagged speaker | Speaker's action right before the line; "@B stays silent" |
| Wrong or blank location after a cut | The cut didn't restate the place | Describe the place in full after every cut |
| A character is missing or doubled | Not tagged on their action, no position | Tag on every action; give a position ("on the left") |
| Background person takes over | Extra was tagged or described at length | Untag; one short phrase for all extras |
| Line rushed, cut off or skipped | Too many beats in one scene | Split so the line has room |
| An action never happens | Buried mid-sentence | Its own sentence, stacked verbs, in sequence |
| Looks different from the other scenes | Wardrobe, light or place worded differently | Repeat the same words in every scene |

## Checklist

- [ ] 6 or fewer unique `@` tags
- [ ] 3 or fewer dialogue turns
- [ ] 50 or fewer dialogue words (counted)
- [ ] Extras untagged, in one plain phrase
- [ ] Every tagged character tagged on every action and every line
- [ ] Characters sharing an action grouped in one sentence
- [ ] Opens with the action (or "Selfie…" for a chat selfie)
- [ ] Location named and concrete, and restated after every cut
- [ ] Tone and environment present
- [ ] Dialogue as `@Name [delivery]: "line"`, action before the line
- [ ] Facing stated both ways for every line with listeners in view
- [ ] Concrete wording, no vague placeholders
- [ ] Scene before style; camera, lighting, color and finish last
- [ ] Every moment change marked
