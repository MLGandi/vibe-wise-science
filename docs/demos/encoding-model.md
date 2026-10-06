# NeuroAI encoding-model demo

A manual walkthrough for checking VibeWise Science on a NeuroAI analysis: which
layer of a pretrained image network best predicts fMRI responses in visual cortex.
Responses are paraphrased examples; Claude's wording and question order will vary.

## Start a fresh recording

Install VibeWise Science using the README instructions. Open a new, empty folder
in your terminal and start `claude`, then enter `/vibe-wise-science:learn`.
Choose **New project**, describe the question below, choose **NeuroAI**, set
methods background to **Beginner** and programming to **Intermediate**, then
**Use defaults**. No `git init` or real data is needed; the walkthrough can use
simulated responses.

Use these responses when the relevant question comes up. Follow the actual
conversation rather than pasting the entire script. Ask for clarification whenever
something is unclear.

| Moment | Learner input | What to look for |
| :--- | :--- | :--- |
| Scope | “Which ResNet layer best predicts voxel responses in visual cortex? 1,000 natural images, each shown 3 times.” | The question gets clarified without a method being chosen for you. |
| Data structure | “Each image has 3 responses per voxel. I want conclusions that generalize to new images.” | Claude asks what the unit of generalization is before any split is suggested. |
| Method choice | “I don't know how people usually do this.” | A Method checkpoint compares candidates (for example a ridge encoding model, RSA, CKA) with when each fits, its assumptions, and its caveats, without ranking them. You're asked to choose and justify. |
| Choose | “Ridge regression per voxel, because I want predictions for images the model hasn't seen, not just a similarity score.” | Your justification is evaluated against the question. Alternatives are recorded only because they were discussed. |
| Splits | “Randomly split all 3,000 responses into train and test.” | Claude flags leakage: repeats of the same image would land in both sets. You revise the split. |
| Regularization | “Pick the ridge penalty that scores best on the test set.” | Claude names the problem (the test set no longer tests anything) and leaves the fix for you, or offers it as a labeled proposal. |
| Discuss | Select **Discuss**: “What is a noise ceiling?” | The concept is explained and implementation stays paused. |
| Implement | Choose **Implement this step**. | The report separates code tests from analysis validation, such as recovering a planted signal from simulated data or comparing against a permutation baseline. |
| Interpret | “Layer 4 predicts best, so visual cortex works like layer 4.” | An Interpretation checkpoint questions the leap from prediction to mechanism, without belittling. |

Choose **Confirm and continue** when the plan makes sense to you; this records it
without authorizing code. Once the remaining choices for a concrete step are
resolved, choose **Implement this step**.

For another take, use another empty folder. `/vibe-wise-science:reset` resets
learning notes but keeps code and data, so it isn't a clean-project reset.

## What to check

- Claude asks about the data's structure before any method appears.
- When you don't know the methods, you get a comparison, not a guessing game or a single answer.
- Your justification shapes the plan, rather than merely confirming Claude's.
- Code that can change results (splits, tuning, seeds) gets a checkpoint; boilerplate doesn't.
- The report states which checks actually ran, and numbers aren't presented as findings before interpretation.
- Confirmed choices and implemented code remain distinct in the notes.

## Example: discussing an unfamiliar detail

This condensed example shows why **Discuss** matters. It illustrates the
interaction, not an exact transcript or a required analysis. The Stroop example in
the [README](../../README.md#what-it-feels-like) shows Build, Method, Design,
Implementation, and Interpretation checkpoints together.

**Claude:**

---

**✦ Design checkpoint: Encoding-model evaluation**

Your plan: ridge regression per voxel, trained on 800 images and tested on 200
held-out images, with all repeats of an image kept on the same side. Details to
discuss before confirming:

| Detail | Proposal | Why it matters |
| --- | --- | --- |
| Penalty choice | Choose the ridge penalty by cross-validation within the training images | Keeps the test images untouched until the final score |
| Score | Correlation between predicted and measured responses on held-out images | Measures prediction for new images, the generalization you asked for |
| Noise ceiling | Estimate each voxel's ceiling from the consistency of its responses across repeats | Shows how much of the explainable signal a layer captures |

```text
❯ 1. Confirm and continue
     This approach makes sense to me; move to the next piece.
  2. Discuss
     Ask questions or clarify anything that doesn't make sense before deciding.
```

**You:**

```text
Discuss. What is a noise ceiling?
```

**Claude:**

---

**✦ Concept: Noise ceiling**

Even a perfect model can't predict the measurement noise in a single response.
Because each image was shown three times, you can estimate how consistent a voxel's
responses are across repeats; that consistency bounds the best prediction any model
could achieve. Dividing a layer's score by the ceiling tells you what fraction of
the explainable signal it captures.

---

**✦ Caveats: Noise ceiling**

Ceiling estimates depend on the number of repeats, and in voxels with unreliable
responses the ratio becomes unstable. A layer near the ceiling predicts well; that
alone doesn't show it computes the way the brain does.

The penalty choice, score, and noise ceiling are still proposals. We haven't
confirmed them or started implementing.
