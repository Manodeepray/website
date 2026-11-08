+++
title = 'TRACE: The Realignment Problem'
aliases = ['/projects/trace/']
date = 2026-10-21T12:00:00+05:30
draft = false
+++

### TRACE: The Realignment Problem — When Right Becomes Wrong in LLMs

Alignment isn't a one-time thing. The rules a model gets aligned to (safety policies, content guidelines, what counts as "acceptable") keep changing, but the model stays frozen at whatever it was trained on. We call this drift the **Alignment-Reality Gap**: a model that was "right" under the old policy becomes "wrong" under the new one. The obvious fix is to re-annotate the preference data under the revised rules and retrain, but that is expensive, slow and inconsistent. So the question we asked was: can you realign a model to a new policy by reusing the preference data you already have?

That's what **TRACE** (*Triage and Re-align by Alignment Conflict Evaluation*) does. It first triages the existing preference pairs against the new policy, using a stronger model as a proxy judge. Each pair is sorted into one of three buckets: **inversion** (the old preferred answer is now the wrong one), **suppression** (both answers are now unacceptable), or **retention** (still fine as is). A bi-level optimization then scores how much each sample matters, and the model is updated with a hybrid objective: IPO for inversions and NPO for suppressions, while the retained data keeps general capabilities intact. We tested it on Qwen2.5-7B, Gemma-2-9B and Llama-3.1-8B, on synthetic policy-shift benchmarks and on PKU-SafeRLHF. In both settings it realigned the models to the new policy without hurting their general utility.

I'm a co-author on this one. My main work was the **experiments** and the **rebuttal**. On the experiments side, that meant running and debugging the training and evaluation pipelines across the different model families and benchmarks, and making sure the comparisons were fair and the numbers held up. The rebuttal was its own experience. Reviewers asked hard questions, and answering them usually meant running new experiments and ablations on a tight deadline, then explaining the results clearly. I learned a lot about how a paper gets defended, not just how it gets written.

I also ran a small interpretability follow-up on my own, looking at whether the triage bins separate in the model's activations: [read it on the blog](/website/blog/trace-interp/).

---

- Paper: [arXiv:2511.02623](https://arxiv.org/abs/2511.02623)
- Project page & code: [respailab.github.io/TRACE](https://respailab.github.io/TRACE)
