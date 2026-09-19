# Three Papers — Working Comparison

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

## Evidence map

| Question | RT-2 | SelfWAM | DreamZero |
|---|---|---|
| Semantic/generalization transfer | Strong focus | Less central | Language following plus task/environment transfer |
| Explicit action-conditioned future prediction | Not the central mechanism | Central mechanism | Central: jointly models video and action |
| Direct action generation | Yes | Yes | Yes |
| Future visual prediction | Not central | Yes | Yes, using a pretrained video-diffusion backbone |
| Real-world testing | Yes | Yes | Yes |
| Controlled test of core mechanism | Less direct | Stronger direct action-sensitivity test | Cross-task/environment and cross-embodiment transfer |
| Main evidence limitation | Does not directly test explicit physics | Sensitivity is not physical correctness | WAM advantage is confounded with a 14B video backbone/data/compute |
| Evidence for universal general-purpose superiority | No | No | No |

## Emerging research question

The useful debate may not be:

> “VLA or WAM?”

but rather:

> “When does explicit predictive world modeling provide enough additional value over direct VLA policies to justify its data, compute, modeling and planning complexity?”

## Provisional conclusion after Paper 3

A hybrid approach could potentially divide responsibilities:

- VLA: semantic understanding, language grounding, task-level intent;
- WAM: action-conditioned prediction, physical consequences, local planning;
- controller: execute and observe actual outcomes.

DreamZero provides independent, promising evidence that large-scale video priors may improve physical and cross-embodiment transfer. However, it does not isolate whether the benefit comes from explicit world-action modeling, the pretrained video backbone, the data mixture, or the compute budget.

Therefore the defensible PS-04 conclusion is not “WAM beats VLA.” It is:

> VLA-style semantic grounding and WAM-style action-conditioned prediction appear complementary; stronger matched comparisons are still needed to establish when the predictive component justifies its complexity.
