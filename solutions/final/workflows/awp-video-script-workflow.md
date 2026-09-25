# Voiceover Script Workflow (AWP)

## Trigger
Runs every time a new video needs a voiceover script — when Leo says "new script for [topic]" or a video topic is confirmed.

## Steps
1. **Interview Leo.** Ask one question at a time: what is the video topic, who is it for, and what should the viewer be able to do after watching? Confirm a working title.
2. **Search the web.** Research the topic: current sources, best practices, what others already cover, and what is missing. Verify the topic is current and worth a video. Keep the key findings for the outline.
3. **Build the outline.** Divide the video into sections — Hook, Value steps, Recap, CTA — with a time budget for each section. Present the outline to Leo, discuss, and adjust until he confirms.
4. **Write the first draft.** Follow `specs/youtube-script-standard.md`: hook in the first 20 seconds, one idea per section, short spoken sentences, about 130–150 words per minute for the target duration.
5. **Polish to standard.** Read the script aloud mentally; cut filler, dead air, and any sentence that stumbles. Confirm all four sections are present and the CTA comes once, at the end.
6. **Save the final script.** Write the finished script to `business/youtube/` with a four-part filename.

## Check
Reference `specs/youtube-script-standard.md` and `specs/naming-convention.md`:
- Hook in the first 20 seconds — opens with a problem or promise, not "hey guys, welcome back".
- All four sections present: Hook, Value, Recap, CTA.
- Read-aloud test: every sentence short and spoken-natural; no sentence over 25 words.
- No filler words, no begging for likes before the end.
- Word count ≈ 130–150 × target minutes.
- Filename follows the four-part rule: `video-script-youtube-{YYYYMMDD}.md`.

## Lands in
`business/youtube/` — named `video-script-youtube-{YYYYMMDD}.md` (type-object-scope-date).
