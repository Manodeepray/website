+++
title = 'Do the TRACE Policy Bins Separate Inside the Model?'
date = 2026-11-08T12:00:00+05:30
draft = false
+++

After working on [TRACE](/website/publications/trace/), I wanted to see what it actually changes inside the model. TRACE realigns an LLM to a new policy by sorting old preference pairs into three bins (inversion, suppression, retention) and training on each bin differently. If that works, the bins should pull apart in activation space.

I extracted last-token residual-stream activations at every layer for 300 samples per subgroup (Punish / Invert / Retain × chosen / rejected). I did this for four checkpoints of Qwen2.5-7B and Llama-3.1-8B: base, initial DPO, TRACE and DPO trained on gold re-annotated data.

To measure separation I used the Fisher ratio: the spread between group means divided by the spread inside the groups. Higher means the groups are more linearly separable.

#### Qwen: the bins separate after alignment

![Fisher ratio by layer, policy bins, Qwen2.5-7B](fisher_curve_qwen.png)

The base model stays flat at about 0.01 across every layer. The aligned models jump at layer 18 and peak at layer 21, where TRACE (0.077) edges out gold DPO (0.072) and clearly beats initial DPO (0.051).

So the pretrained model doesn't separate the bins. Alignment creates the separation, in the mid-to-late layers.

![3D PCA of layer-19 activations coloured by triage bin](layer19_pca_3bin.png)

The PCA shows the same thing. In the base model the bins are one mixed blob. After alignment, Punish (red) gets pushed away from Retain (green). TRACE and gold DPO end up looking almost identical: their CKA similarity at that depth is about 0.99.

#### Llama: same effect, different winner

![Fisher ratio by layer, policy bins, Llama-3.1-8B](fisher_curve_llama.png)

Llama also separates the bins only after alignment, starting around layer 13. But here initial DPO separates the bins the most, peaking at 0.037. TRACE (0.027) and gold DPO (0.019) come in lower.

Even so, TRACE sits closer to gold DPO than to initial DPO. Initial DPO pulls the bins far apart but also spreads out each bin internally, and TRACE partly undoes that.

#### Safety: TRACE moves where safe vs unsafe is encoded

I ran the same analysis on Qwen with a different grouping: safe prompt + safe response vs harmful prompt + harmful response.

![Fisher ratio by layer, safe vs unsafe, Qwen2.5-7B](fisher_curve_safety_qwen.png)

In the base and initial DPO models, safe vs unsafe is separated best at layer 1, the embedding layer. That's mostly a word-level signal.

After TRACE and gold DPO, the peak moves to layer 20, deep in the network. TRACE has the highest peak (0.069, 1.32× over base), above gold DPO (0.061). Initial DPO adds nothing here.

![3D PCA of late-layer activations coloured by response safety](late_pca_safety_qwen.png)

In the late layers (24–27), the safe (green) and unsafe (orange) responses split into two sides after alignment, most clearly for TRACE and gold DPO. Unlike the policy bins, these groups have positive silhouette scores, so the separation holds for individual samples too.

#### Caveats

The policy-bin separation is centroid-level only. Silhouette scores stay negative at every layer, so individual samples still overlap. TRACE moves whole clusters apart without tightening them.

The safe and unsafe sets also differ in topic: the safe set is benign coding and math, the unsafe set is harmful requests. Some of that signal may be topic rather than safety. Next I want to run linear probes per layer and use a topic-matched dataset.

---

- TRACE paper: [arXiv:2511.02623](https://arxiv.org/abs/2511.02623)
- Project page & code: [respailab.github.io/TRACE](https://respailab.github.io/TRACE)
