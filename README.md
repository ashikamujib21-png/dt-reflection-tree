# The Daily Reflection Tree

A deterministic end-of-day reflection tool for employees. No LLM at runtime — just a well-designed tree walked by simple Python.

## What It Does

Guides an employee through a 5-minute structured reflection across three psychological axes:

1. **Locus** — Did you move through today as an agent, or a passenger? *(Rotter, 1954; Dweck, 2006)*
2. **Orientation** — Were you oriented toward giving or receiving? *(Organ, 1988; Campbell et al., 2004)*
3. **Radius** — How wide was your circle of concern? *(Maslow, 1969; Batson, 2011)*

Every question has fixed options. Every option leads to a known branch. Same answers → same path → same reflection. Always.

---

## Repository Structure

```
/tree/
  reflection-tree.json   ← The tree as structured data (37 nodes)
  tree-diagram.md        ← Mermaid diagram of all branches

/agent/
  agent.py               ← Python CLI that walks the tree

/transcripts/
  persona-1-transcript.md  ← Victim/entitled/self-centric path
  persona-2-transcript.md  ← Victor/contributing/altrocentric path

write-up.md              ← Design rationale (2 pages)
README.md                ← This file
```

---

## Running the Agent

**Requirements:** Python 3.10+, no external dependencies.

```bash
# From the project root:
python agent/agent.py
```

The agent loads `tree/reflection-tree.json` automatically. The session runs in your terminal with slow-printed text for a more reflective feel.

---

## Reading the Tree (Part A)

The tree lives in `tree/reflection-tree.json`. You can read every possible conversation path without running code — just follow the `target` fields and `options` arrays.

### Node Types

| Type | Behavior |
|------|----------|
| `start` | Auto-advances after employee reads opening |
| `question` | Renders options 1–N, waits for input, records answer in state |
| `decision` | Invisible routing — matches prior answer against rules, jumps to target node |
| `reflection` | Shows reframe text, employee clicks Continue |
| `bridge` | Auto-advances with axis transition text |
| `summary` | Interpolates path-based summary using accumulated signals |
| `end` | Closes session |

### Decision Routing

Decision nodes contain an `options` array of routing rules:

```json
{
  "match": ["Sunny — things flowed, I felt in stride", "Unpredictable — some highs, some real lows"],
  "goto": "A1_Q2_HIGH"
}
```

The agent matches the previous question's answer against `match` arrays and jumps to `goto`. No fuzzy matching — exact string comparison only.

### Signals and State

Question and reflection nodes carry a `signal` field (e.g., `"axis1:internal"`). As nodes are visited, signals are tallied in state:

```python
state["signals"]["axis1"]["internal"] += 1
```

At the summary node, the dominant pole per axis is computed and interpolated into the summary text using `{axis1.dominant}` placeholders. Earlier answers are interpolated using `{NODE_ID.answer}` syntax.

### Tracing a Path by Hand

To trace the "victim" path:
1. Start at `START` → follow `target` to `A1_OPEN`
2. At `A1_OPEN`, choose "Stormy" → goes to decision `A1_D1`
3. `A1_D1` matches "Stormy" → jumps to `A1_Q2_LOW`
4. At `A1_Q2_LOW`, choose "Wait for someone else" → goes to `A1_D2_LOW`
5. Continue following decisions and question answers...

See `/transcripts/persona-1-transcript.md` for the complete path annotated.

---

## Tree Statistics

| Metric | Value |
|--------|-------|
| Total nodes | 37 |
| Question nodes | 14 |
| Decision nodes | 9 |
| Reflection nodes | 8 |
| Bridge nodes | 2 |
| Summary nodes | 1 |
| End nodes | 1 |
| Start nodes | 1 |
| Distinct conversation paths | 12 |
| Questions per session | 9 (always) |
| LLM calls at runtime | 0 |
