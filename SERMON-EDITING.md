# Sermon-Editing Prototype: Encode the Parts That Change

[Portfolio](PORTFOLIO.md) / Sermon-editing prototype

**Context:** A prototype for extracting and editing sermon footage from a longer church-service recording.

**My contribution:** The selective-rendering approach and later boundary/output requirements. AI supplied implementation code, the quotation-to-timestamp matching concept, and detailed FFmpeg/keyframe mechanics.

## The processing decision

Most of an edited sermon is unchanged footage. When a full-video render was proposed, I asked whether the process could encode only the transitions and reconnect the unchanged clips.

The implementation copies the bulk segments, encodes transitions, and joins them, with a full re-encode fallback where needed. That is the specific rendering approach I contributed; it is not a claim that I independently designed the entire editor or its low-level video mechanics.

## Keep interpretation and timing connected

I also specified preserving the word-timestamp transcript while sending only its text to the semantic model. The returned transition phrases needed to map back to the retained timing information.

Later requirements distinguished the start of a phrase from the end of a phrase, placed cuts in surrounding silence, and corrected actual outputs where a cut removed the wrong side of speech. I also required the small intro clip to adapt to the important sermon footage's format.

## Status and boundaries

This is a prototype, not a routine unattended weekly production pipeline. A later redesign remained planning and is not presented as completed work. This case makes no render-time benchmark or quality guarantee.

The local working folder, recordings, transcripts, and configuration remain private.
