# Write-Up: Design Rationale — The Daily Reflection Tree

## Why These Questions

The hardest constraint in this design wasn't the code. It was writing questions that a tired person at 7pm would answer *honestly* — not the way they want to appear, but the way they actually are.

Three principles guided question design:

**1. Avoid leading options.** Each set of options had to be genuinely chooseable. If option A is clearly "the good answer," people pick it reflexively and learn nothing. The victim/victor framing had to be implicit in the *branching*, not explicit in the *wording*. Nobody sees "You're the victim" — they just answer what felt true, and the tree routes accordingly.

**2. Make the dimensions concrete.** Locus of control is an abstract concept. "When things got difficult today, what was your first instinct?" is concrete. The psychological construct lives in the branching logic, not in the question text. This mirrors how good assessment design works — you measure indirectly, through observable behavior.

**3. Leave room for nuance.** The "Unpredictable — some highs, some real lows" option for the opening question exists because most real days aren't cleanly good or bad. Forcing a binary at the start would feel dishonest and alienate the employee immediately. The decision node handles the nuance — routing "Unpredictable" to the same branch as "Sunny" because someone who reports a mixed day still has enough cognitive access to reflect on agency.

## How the Branching Was Designed

The core branching challenge on Axis 1 was creating a two-stage funnel: first route by *day quality*, then route by *agency marker*, then ask the axis-specific deeper question. This two-decision structure (A1_D1 → A1_D2_HIGH/LOW) allows the third question to be more targeted — someone arriving via the "stormy" path gets a question that meets them where they are ("was there any moment of choice?"), while someone on the "sunny" path gets asked what *drove* their decision-making.

The trade-off here was depth vs. symmetry. A fully symmetric tree would give every person the same three questions. But a person who had a rough day and an internal locus needs a different question than someone who had a great day and attributes it to luck. The branching earns its complexity by asking more relevant questions, not just different questions.

On Axes 2 and 3, the branching is shallower — one decision per axis versus two on Axis 1. This was deliberate: Axis 1 is the hardest concept (locus of control is counterintuitive), so it gets the most scaffolding. By Axis 3, the employee is already in a reflective state and can handle a more direct question.

## Psychological Sources

**Axis 1** draws directly on Rotter's (1954) Internal-External Locus of Control Scale. The key insight from Rotter is that locus is a *generalized expectancy* — a stable belief about the relationship between behavior and outcomes. The tree surfaces this not by asking "do you have an internal locus?" but by asking about specific behavioral responses to specific situations, which is how Rotter's original scale was structured. Dweck's Growth Mindset (2006) informs the framing of the reflection nodes — particularly the language around "staying in it as an active participant," which reflects the growth-oriented belief that engagement drives outcomes.

**Axis 2** draws on Organ's (1988) Organizational Citizenship Behavior framework and Campbell et al.'s (2004) work on psychological entitlement. The critical design challenge here was making entitlement *visible to the person holding it* without triggering defensiveness. The question "At any point today, did you feel like your effort wasn't being seen?" isn't accusatory — it's empathetic. But it surfaces the entitlement orientation through the follow-up ("what did you do with that feeling?"). Someone who let it go and moved on shows a different orientation than someone who pulled back from their work.

**Axis 3** draws on Maslow's (1969) paper "Theory Z," which introduced self-transcendence as a level above self-actualization in his revised hierarchy. Maslow argued that the healthiest humans orient outward — their motivation becomes contribution to something beyond themselves. The tree operationalizes this through Batson's (2011) perspective-taking construct: not "do you care about others?" but "whose experience were you aware of today?" Awareness precedes action. The branching on Axis 3 deliberately includes a "customers/users" option as the widest possible radius — reflecting Maslow's point that transcendence scales beyond immediate social circles.

## What I Would Improve With More Time

**More branching depth on Axes 2 and 3.** Currently, the Axis 2 decision node (A2_D2) has to handle four possible previous answers across two question branches, which creates an awkward routing structure. With more time, I'd introduce an intermediate "mixed signal" detection mechanism — perhaps a separate path for employees whose signals are ambiguous within an axis, giving them a tie-breaking question rather than defaulting to "mixed."

**Longitudinal state.** The tree currently reflects a single session. The most powerful use of this structure would be trend detection — if an employee routes through the "external locus" branch three sessions in a row, the tree could surface that pattern explicitly. This would require a session history store, but the tree structure already supports it via signals.

**Softer language on the summary.** The summary currently names the dominant pole directly ("you leaned external"). This is accurate but potentially jarring after a session that tried to avoid judgment. A revised summary would use more oblique language — "today's pull was outward" rather than "you leaned external" — preserving self-awareness without the clinical label.

**A fourth, optional axis.** The three axes as designed move from *self-perception* (Locus) to *behavioral orientation* (Contribution) to *cognitive scope* (Radius). A natural fourth axis would be *temporal orientation* — whether the employee is anchored in past grievances, present action, or future possibility. This draws on psychological flexibility research (Hayes, 2004) and would round out the reflection with a forward-looking question.

---

*Total nodes: 37 | Questions: 14 | Reflection nodes: 8 | Distinct paths: 12*
