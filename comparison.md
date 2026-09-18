# First Two Papers — Working Comparison

## The conceptual difference

### RT-2 / VLA

Primary question:

> **Given what I see and what I am asked to do, what action should I take?**

`vision + language → action`

The major advantage demonstrated by RT-2 is transfer of broad visual/semantic knowledge into robot control.

### SelfWAM / WAM

Primary question:

> **Given the current world and a particular action, what will happen next?**

`world + action → predicted future`

The major advantage investigated by SelfWAM is tighter grounding of future prediction in action consequences.

## Important correction

Do **not** write:

> VLA = knowledge, WAM = physics.

That is only an intuition.

A more defensible statement is:

> RT-2 demonstrates the value of transferring broad vision-language knowledge into robot action, while SelfWAM investigates whether explicit action-conditioned prediction of future observations adds useful physical grounding to policy learning.

Modern systems can overlap these categories.

## Current evidence map

| Question | RT-2 | SelfWAM |
|---|---|---|
| Semantic/generalization transfer | Strong focus | Less central |
| Explicit action-conditioned future prediction | Not the central mechanism | Central mechanism |
| Direct action generation | Yes | Yes |
| Future visual prediction | Not central | Yes |
| Real-world testing | Yes | Yes |
| Controlled test of core mechanism | Less direct | Stronger direct action-sensitivity test |
| Evidence for universal general-purpose superiority | No | No |

## Emerging research question

The useful debate may not be:

> “VLA or WAM?”

but rather:

> “When does explicit predictive world modeling provide enough additional value over direct VLA policies to justify its data, compute, modeling and planning complexity?”

## Hypothesis to test with Paper 3

A hybrid approach could potentially divide responsibilities:

- VLA: semantic understanding, language grounding, task-level intent;
- WAM: action-conditioned prediction, physical consequences, local planning;
- controller: execute and observe actual outcomes.

But this is currently a **hypothesis**, not our conclusion.

We need Paper 3 to give us independent evidence before deciding.
