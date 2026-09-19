# Paper 3 — DreamZero

**World Action Models are Zero-shot Policies**  
Ye et al., 2026 — arXiv preprint

Paper: https://arxiv.org/abs/2602.15922  
Project: https://dreamzero0.github.io/

> Status: recent preprint. The performance figures below are author-reported results, not settled field consensus.

## 1. Problem

Vision-Language-Action (VLA) models can transfer broad visual and semantic knowledge into robot control, but the paper argues that they are less reliable when a task requires unfamiliar physical motions in new environments.

DreamZero asks whether a robot can gain a stronger prior for physical interaction from a large pretrained video model: video provides dense evidence of how scenes change over time, rather than only examples mapping an observation and instruction to an action.

## 2. Main claim

DreamZero claims that a **World Action Model (WAM)** built on a pretrained video-diffusion backbone can jointly predict future video and robot actions, allowing more effective generalization to new tasks, environments, and embodiments than selected VLA baselines.

## 3. Core idea

Conceptually:

`current image + language + action context → future video and action`

Rather than treating control only as:

`current observation + instruction → action`,

DreamZero learns an action-linked visual future. The hoped-for benefit is that a useful action must agree with how the scene is predicted to evolve.

This does **not** mean the system has an explicit symbolic physics engine. It learns statistical regularities about action consequences from video and robot data.

## 4. Model and training

DreamZero is a 14B-parameter robot foundation model built upon a pretrained image-to-video diffusion backbone. It is trained to jointly model videos and actions using heterogeneous robot data rather than relying only on repeated demonstrations of one task.

The paper's key source of prior knowledge differs from RT-2:

- RT-2 starts with broad vision-language/semantic pretraining;
- DreamZero starts with broad temporal and visual knowledge from video diffusion, then connects it to robot actions.

In principle, this makes video a representation of how the physical world tends to evolve. In practice, whether the model transfers that knowledge to a new robot task is an empirical question.

## 5. Why this is different from SelfWAM

SelfWAM tests whether future prediction becomes more useful when it is tied to the **specific demonstrated action**. DreamZero makes a broader scaling claim: a large video model can supply transferable physical/temporal priors before or alongside robot-specific learning.

| Paper | Main question |
|---|---|
| RT-2 | Can VLM semantic knowledge transfer into robot actions? |
| SelfWAM | Does action-conditioned future prediction improve control? |
| DreamZero | Can pretrained video dynamics reduce dependence on task-specific robot demonstrations? |

## 6. Reported real-robot results

The paper reports more than a 2× improvement in generalization to new tasks and environments compared with the state-of-the-art VLA baselines selected by the authors.

It also reports real-time closed-loop control at 7 Hz (150 ms per action chunk) after model, system, and implementation optimizations. This matters because a video-diffusion WAM would otherwise be difficult to use in a control loop.

These claims are promising, but a relative improvement does not by itself show how difficult the evaluated tasks were, whether the baselines had comparable pretraining/data/compute, or that all WAMs outperform all VLAs.

## 7. Cross-embodiment transfer

The paper reports two forms of transfer:

1. Video-only demonstrations from other robots or humans improve unseen-task performance by over 42% relative with 10–20 minutes of data.
2. A new robot embodiment can be adapted with about 30 minutes of play data while retaining zero-shot generalization in the reported setup.

This is especially relevant to general-purpose robotics: a useful robot policy should transfer not only across instructions, but potentially across environments and bodies.

## 8. What “zero-shot” means here

The title should not be read as “no relevant data or adaptation is required.” DreamZero still relies on large-scale pretraining, robot/action data, and—in the new-embodiment result—play data for adaptation.

Here, zero-shot means generalizing to particular unseen tasks or environments without task-specific demonstrations under the paper's evaluation protocol.

## 9. What the evidence supports

The reported experiments support the narrower conclusion that a large pretrained video-diffusion backbone, jointly trained with actions, can be a promising route to generalization in the authors' real-robot evaluations.

The cross-embodiment experiments are more relevant to the general-purpose robotics question than a benchmark score alone because they probe transfer beyond one fixed robot/task distribution.

## 10. What it does NOT establish

The paper does not establish that:

1. generated or predicted video is always physically correct;
2. the model has causal, equation-like understanding of physics;
3. WAMs are universally superior to VLAs; or
4. the gains are caused by the WAM paradigm alone rather than the 14B pretrained video backbone, data mixture, compute budget, and system engineering.

Plausible-looking future video is not the same thing as accurate counterfactual prediction under unusual friction, mass, contact, camera, or embodiment changes.

## 11. Strong points

1. Tests a different source of generalization from RT-2: temporal/video knowledge rather than primarily semantic VLM knowledge.
2. Includes real-time closed-loop robot control rather than only offline future-video generation.
3. Cross-embodiment experiments directly address an important form of generalization.
4. Makes a concrete, testable claim about reducing task-specific demonstration dependence.

## 12. Weak points / critique

1. The headline comparison can be confounded: DreamZero has a very large pretrained video model, so its result does not isolate the value of the WAM formulation.
2. “Over 2×” is a relative result from selected tasks and baselines, not a universal paradigm comparison.
3. Video prediction may be visually plausible while physically wrong; the paper's success metrics do not prove counterfactual physical accuracy under distribution shift.
4. 14B video diffusion plus the required optimizations may impose substantial training, inference, and deployment complexity.
5. Cross-embodiment adaptation still uses 10–30 minutes of additional data, so transfer is not fully data-free.

## 13. PS-04 defence notes

If asked “What is DreamZero's main contribution?”:

> DreamZero turns a pretrained video-diffusion model into a world-action model that jointly predicts video futures and robot actions, aiming to transfer temporal/physical priors into zero-shot robot control.

If asked “How is it different from RT-2?”:

> RT-2 mainly transfers broad visual-semantic knowledge from a VLM into action generation. DreamZero argues that pretrained video models contribute a different kind of knowledge: how visual scenes and interactions evolve over time.

If asked “Does it prove that WAMs understand physics?”:

> No. It provides promising behavioral evidence on robot tasks, but successful or plausible video prediction is not proof of physically correct, causal understanding in every new situation.

If asked “What is the fairest conclusion after all three papers?”:

> The evidence suggests that semantic VLA knowledge and action-conditioned predictive modeling target complementary strengths. A hybrid may be most promising, but the current papers do not yet prove a universal winner.
