# AI Correction Monitor: Defining What Should Trigger Help

[Portfolio](PORTFOLIO.md) / AI correction monitor

**Project:** Factory918, a research prototype for recognizing when a user is correcting an AI assistant.

**My contribution:** The separate-monitor concept, the distinction between detecting a situation and proving that guidance helps, label definitions, and rulings on ambiguous examples. AI wrote the extraction, hook, labeling, and statistical implementation.

## Two different questions

An assistant may improve when given useful guidance at a particular point. That does not establish that a system can reliably recognize when to provide that guidance.

I distinguished these questions during the design discussion:

1. Does a proposed intervention improve the assistant's behavior?
2. Can the system consistently detect the moment when that intervention is appropriate?

I proposed a separate monitor for the second problem and corrected an interpretation that treated it as an inspector of the assistant's output alone.

## Label meaning comes before a score

The dataset contains about 600 conversation messages. Most labels were model-applied under the definitions and rulings; I did not personally label every message.

One important distinction was between an ordinary preference or disagreement and a response showing that the assistant had misunderstood the user's meaning, priorities, or constraints. I defined and refined those boundaries and resolved ambiguous examples.

That definition affects what a reported false alarm or missed correction actually means. Some labels depend on information appearing later in the conversation, while a deployed monitor can only see what has happened so far.

## Public source

The relevant work is on an existing research branch, separate from Factory918's default toolkit page:

- [Research source](https://github.com/Zenoctra/factory918/tree/research/moment-detector/moment-detector)
- [Label definitions and rulings](https://github.com/Zenoctra/factory918/blob/research/moment-detector/moment-detector/moments/definition.md)
- [Scoring implementation and research record](https://github.com/Zenoctra/factory918/tree/research/moment-detector/moment-detector/scoring)
- [Factory918 toolkit](https://github.com/Zenoctra/factory918)

## Status and evaluation limits

The research records detection experiments, model comparisons, and label revisions. Definitions and labels changed after errors had been examined, so later figures should be read as exploratory results rather than a fresh untouched holdout benchmark.

Detection results also do not establish that the monitor's guidance improves the main assistant. Those remain separate evaluation questions. This case intentionally makes no headline accuracy claim.

Private conversation transcripts and per-message research data are not copied into this portfolio.
