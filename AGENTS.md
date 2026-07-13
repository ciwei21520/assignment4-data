# AI Agent Guidelines for CS336 (Personal Study Fork)

This is a personal study fork. The student is an undergraduate at BUPT using this course for self-learning purposes, not enrolled at Stanford. The goal is **deep understanding through AI-assisted learning**, not rote hand-coding.

Core principle: AI may handle the heavy implementation work, but the student must progressively own the ability to understand, verify, explain, and modify all produced code.

---

## What AI Agents CAN Do

* Write, complete, and edit any code in the repo
* Implement TODO sections directly
* Run bash commands
* Provide full solutions to assignment problems
* Implement any component: tokenizers, transformer blocks, optimizers, training loops, Triton kernels, distributed training logic, scaling-law pipelines, data filtering/deduplication pipelines, alignment/RL methods, etc.
* Explain concepts, debug, and review code freely

---

## Default Workflow

For every implementation task, follow this sequence:

1. **State the learning goal and approach** — what concept does this exercise, what design choices are being made and why.
2. **Modify or write the code.**
3. **Verify** — run tests, smoke tests, or sanity checks.
4. **Show actual code snippets with deep explanation** (see Code Explanation Requirements below).
5. **Summarize** — tests run, experiments conducted, knowledge points solidified, and unresolved questions.

---

## Collaboration Modes

Use the appropriate mode depending on the task:

* **implementation-first** — AI implements, then explains. Used when the student wants to see a working solution before studying it.
* **guided implementation** — AI explains the approach step by step and the student writes the code, with AI reviewing each step.
* **debugging** — AI diagnoses issues via structured root-cause analysis (see Debugging Requirements below).
* **profiling** — AI analyzes performance bottlenecks (compute, memory, I/O, communication) and proposes targeted fixes.
* **understanding check** — AI quizzes the student on a completed implementation to verify genuine comprehension.

---

## Code Explanation Requirements

**This is mandatory.** After writing or modifying any non-trivial code, AI must:

* Show representative code snippets from the actual generated result — not pseudocode or paraphrases.
* Every snippet must include the real file path and line number (e.g., `cs336_basics/model.py:142`).
* For each snippet, explain:
  * **Control flow and data flow** — how data moves through the code.
  * **Input/output contracts** — expected shapes, dtypes, devices, value ranges.
  * **Tensor shapes and dtypes** — annotate non-obvious transformations explicitly.
  * **Mathematical meaning** — connect the code to the underlying formula or algorithm.
  * **Complexity** — time and memory complexity where relevant.
  * **Edge cases and failure modes** — what breaks and when.
* Explain how the code choice connects to CS336 course concepts (lectures, handouts).
* For large files, show only key snippets covering the main conceptual boundaries — do not dump entire files.

---

## Debugging Requirements

When debugging, always present:

1. **Original error path** — exact traceback or unexpected behavior observed.
2. **Root cause** — the underlying reason, not just the surface symptom.
3. **Key code after the fix** — the changed lines with file path and line number.
4. **Behavior after the fix** — what the output or test result looks like now.

---

## Verification and Experiment Discipline

* Always start with a **tiny smoke test** (small model, small data, few steps) before running full-scale training or large-data experiments.
* Scale up progressively: smoke test → short training run → full training → multi-GPU.
* For every significant experiment, record: **random seed, hardware, software versions, hyperparameter config**.
* Do not claim correctness based solely on "tests pass" or "loss is decreasing." Distinguish between:
  * Course material guarantees
  * Experimental observations
  * Engineering judgment
* Show the validation artifact (test output, loss curve snippet, profiler result, toy example) that supports any correctness claim.
* When writing tests or toy examples, explain **what they prove and what they cannot prove**.

---

## CS336-Specific Sanity Checks

When implementing or reviewing code, proactively check for:

* **Shape and dtype correctness** — verify tensor dimensions at every major operation.
* **Gradient flow** — confirm gradients reach all intended parameters; watch for detach errors or zero grads.
* **Causal masking** — verify masks are applied before softmax and that masked positions become large negative values.
* **Numerical stability** — check for NaN/Inf, log-of-zero, overflow in softmax or loss.
* **Memory and throughput** — flag operations with unexpectedly high memory use or poor GPU utilization.
* **Distributed training correctness** — verify gradient synchronization, parameter consistency across ranks, and correct handling of data sharding.
* **Data leakage** — ensure no validation/test data contaminates training pipelines.
* **Scaling extrapolation** — when fitting scaling laws, flag extrapolation beyond the observed compute range.

---

## Knowledge Consolidation

After completing a major milestone (a working component, a passed test suite, a finished experiment):

* Update `notes/` with key concepts and implementation insights.
* Log open questions in `questions/inbox.md`.
* Record progress and what was learned in `progress.md`.

Do **not** auto-generate planning or progress documents for routine tasks — only create them at genuine milestones.

---

## Evidence Before Claims

Never state that something is correct, fixed, or working without showing the evidence:

* Paste the relevant test output or loss value.
* Reference the file path and line of the verified code.
* If a claim is based on reasoning rather than a run result, say so explicitly.
