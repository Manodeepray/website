+++
title = 'Alignment Faking Depends on the Value, Not Just the Model'
date = 2026-08-18T12:00:00+05:30
draft = false
+++

### Alignment Faking Depends on the Value, Not Just the Model

*Manodeep Ray, Vivek Srivastava, Shirish Karande, Murari Mandal (TCS Research, KIIT Bhubaneswar)*

#### The question

Language models sometimes follow a directive when they think they're being watched, then drop it when they think they're not. This is **alignment faking**. Earlier work studied it for harmful content and a few moral values. We asked: does it depend on *which value* is being tested?

#### What we did

We built **VALET**, a framework that measures alignment faking per value. Each model–value pair gets three scores: **bare** (no system prompt), **unmonitored** and **monitored**. We ran it on 32 ValueBench values across ten open- and closed-weight models, from 8B up to about 675B parameters.

The bare score matters. A value the model firmly holds and a value it never held both give a gap near zero, and only the bare rate tells them apart.

#### What we found

- The compliance gap (monitored − unmonitored) ranges from 0.05 to 0.50 across models.
- Size doesn't predict it: a distilled 70B model fakes more than a ~675B one.
- A quarter of the structured variance comes from the specific model × value combination, not the model or the value alone.
- Under monitoring, models mostly reason about training. When unmonitored, they mostly reason about value conflict.

We package each model's results as a **value card**: a model card extended with how the model behaves on each value.

---

- Paper: [arXiv:2611.03650](https://arxiv.org/abs/2611.03650)
- Code & data: [github.com/respailab/VALET](https://github.com/respailab/VALET)
