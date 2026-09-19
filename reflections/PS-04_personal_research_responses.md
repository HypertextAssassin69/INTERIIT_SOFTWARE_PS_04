# PS-04 — My Research Responses

This page records my own evolving answers from the reading discussion. They have been lightly edited only for clarity and structure; the claims are intentionally framed as my interpretation rather than as paper results.

## 1. What does DreamZero add beyond semantic knowledge?

I do not think DreamZero proves that WAMs are better than VLAs. However, it provides evidence that semantic knowledge alone may not be sufficient for broad physical generalization. A robot also benefits from spatiotemporal knowledge: an idea of how the world may evolve as it performs a task.

DreamZero uses large-scale video data to obtain those spatiotemporal priors. It is not exactly predicting a fixed, long future; it repeatedly updates its context from the real world in a closed loop, around seven times per second. This means its predictions can be corrected as the actual situation changes.

## 2. What is the difference between SelfWAM and DreamZero?

SelfWAM tries to ground future predictions in actions: different actions should lead to different predicted futures. It asks whether the model is genuinely relating an action to its consequence, instead of predicting a generic next step in the task.

DreamZero tries to exploit the enormous amount of existing video data to establish prior spatiotemporal knowledge about how a scene or task can evolve. In short:

- **SelfWAM:** Is the future prediction grounded in the specific action?
- **DreamZero:** Can video-derived priors help a robot model how the world may evolve?

## 3. Which approach would I choose for general-purpose robotics?

My current choice is a hybrid: **VLA + DreamZero-style WAM**.

We have evidence that prior spatiotemporal knowledge is useful for predicting how a physical situation may evolve, while semantic correlations and task knowledge help a robot generalize. I do not see these as competing abilities; they solve different parts of the problem.

### Example: using a rock as a hammer

Suppose the world contains a rock, a cup and a flower, and the instruction is:

> “Use an appropriate replacement for a hammer.”

The VLA/VLM side can use semantic knowledge to connect “hammer” with a hard striking tool and identify the rock as the relevant substitute. The DreamZero/WAM side can use spatiotemporal priors to model how the physical interaction may evolve and generate appropriate actions for using the rock.

So I would describe the division as:

`semantic task grounding → predictive physical reasoning → action → observe reality → update`

## 4. Why not call VLA the brain and WAM the body?

The brain/body analogy gives the right intuition, but it is too simple technically. A WAM is not merely an execution system or “body”; it is also a learned predictive/action model. Modern systems blur the boundary because they can jointly model future visual states and actions.

My more precise view is:

- **VLA:** What does the instruction mean, and which objects/concepts matter?
- **WAM:** Given this physical situation and possible action, how may the world evolve?
- **Robot control loop:** Execute, observe the actual result, update the context, and repeat.

## 5. Limits of my conclusion

My hybrid conclusion is an inference from complementary evidence across RT-2, SelfWAM and DreamZero. None of the three papers directly proves that my proposed hybrid is optimal.

I should therefore not claim:

> “WAMs understand the future exactly,” or “VLA + WAM is proven to be best.”

The defensible statement is:

> Semantic and spatiotemporal knowledge appear complementary for general-purpose robotics. A hybrid is a motivated research direction, but it still requires matched experiments that isolate the effect of each component.

## 6. What evidence would change my mind?

I would reconsider the hybrid position if a pure VLA, tested with comparable model scale, data, compute and real-robot settings, consistently matched or exceeded a video-based WAM on novel physical motions, environments and embodiments. That would suggest explicit predictive world modeling may not add enough value to justify its additional complexity.
