# Stern-Gerlach Quantum Measurement Simulator
### A Solution Architecture Case Study in Quantum Pedagogy

**Author:** Dr. Boris Kiefer · [github.com/boriskiefer](https://github.com/boriskiefer) · [linkedin.com/in/boris-kiefer-85089831](https://linkedin.com/in/boris-kiefer-85089831)

---

## Overview

This repository demonstrates a solution architecture engagement applied to
quantum physics education. The Stern-Gerlach experiment — the canonical
demonstration of space quantization — is used as a concrete case study
showing how a customer-first methodology produces a working, pedagogically
sound deliverable.

| Stage | Content |
|---|---|
| **Customer** | Undergraduate students with classical intuition about continuous deflection |
| **Gap** | Static textbook diagrams cannot show the classical-to-quantum transition interactively |
| **Solution** | Interactive simulator with quantum/classical toggle and live metrics |
| **Deliver** | Two-cell Jupyter notebook, zero custom dependencies, runs anywhere |

---

## Repository Contents

```
/
  README.md                        — this file
  sg_sa_showcase.ipynb             — interactive simulator notebook
  sa_pipeline_brief.pdf            — SA methodology brief
  sg_educator_brief.pdf            — Educator brief 
  requirements.txt                 — Python dependencies
  LICENSE                          — MIT
```

---

## Simulator

The notebook is structured as two cells:

- **Cell 1 — Tools:** physics kernels (`run_quantum`, `run_classical`),
  metrics (`compute_metrics`), and plotting (`plot_results`). No global state.
- **Cell 2 — Simulator:** four interactive `ipywidgets` sliders. Adjust
  and observe in real time.

**Run:**
```bash
jupyter lab sg_sa_showcase.ipynb
```

---

## Interactive Controls

| Dial | Physical meaning | Pedagogical role |
|---|---|---|
| **N particles** | Statistical sample size | When does the pattern become trustworthy? |
| **Field strength ∂B/∂z** | Proportional to field gradient | Controls spot separation |
| **Thermal noise σ** | Transverse velocity spread from oven | The classical-to-quantum transition dial |
| **Screen distance** | Drift length post-magnet | Both separation and width scale together |

**Mode toggle:** Quantum (discrete eigenvalues ±½) vs. Classical
(cosine-weighted continuous distribution). The contrast is immediate
and student-controlled.

---

## Suggested Classroom Sequence

1. **Classical mode**, noise = 0.05, field = 1.0 → smooth smear confirms classical intuition
2. **Switch to Quantum** → two discrete spots appear
3. **Raise noise to 0.6** → spots merge, quantum signature washes out — discuss decoherence
4. **Field = 3.0, noise = 0.05** → spots sharply resolved, overlap < 0.01, χ² p > 0.05
5. **Vary screen distance** → spots broaden AND separate together, overlap stays roughly constant
6. **Vary N** → watch metrics stabilise above N ~ 2000

---

## Metrics Panel

| Metric | Meaning |
|---|---|
| z mean / z std | Distribution centre and width |
| frac up / frac down | Empirical split between spin states |
| separation | Distance between spot centres |
| overlap | Fraction of counts in the wrong spot — resolves the quantum signature |
| χ² p-value | Tests consistency with 50/50 — p > 0.05 means consistent |

---

## Physics Summary

**Classical prediction:** $\mu_z = \mu\cos\theta$, $\theta$ uniform on
$[0, \pi]$ → continuous smear.

**Quantum result:** $m_s = \pm\frac{1}{2}$, $P = \frac{1}{2}$ each → two
discrete spots.

Both deflection and thermal spread scale with screen distance:

```
z = m_s · field · distance + N(0, σ · distance)
```

The fixed display range (−4, +4) ensures the axis does not rescale with
distance, so apparent spot width directly reflects the physics.

---

## Hand-Off Notes

Natural extensions for a research-grade version:

- Replace physics kernels with Runge-Kutta integration of the
  time-dependent Schrödinger equation
- Higher-spin parameterisation: $s \in \{\tfrac{1}{2}, 1, \tfrac{3}{2}, 2\}$
  showing $2s+1$ spots
- Sequential measurement stages demonstrating non-commutativity
- Reproducible seeding via `np.random.seed()` for published results

---

## SA Methodology Note

This repository demonstrates an AI-augmented solution architecture workflow:
customer-first problem framing, gap identification, working POC delivery,
and explicit hand-off documentation. Built using domain-expert
human-in-the-loop guidance with LLM assistance.

*See also: [AI Datacenter Photonics — Tier 0](https://github.com/boriskiefer/ai-datacenter-tier0)*
