# Team 10 — Hackathon

Human oversight of AI-assisted eligibility decisions: interactive prototypes, a
simulation study of the oversight metrics, and the background literature.

The question behind the work: when a caseworker reviews an AI suggestion, how do
you tell *real* oversight from rubber-stamping — and can you measure the
difference well enough to notice when oversight degrades?

## Contents

### `Demos/` — interactive prototypes

Self-contained HTML, no build step. Open in a browser.

| File | What it is |
| --- | --- |
| `Cashy Review Simulator(1).html` | Caseworker-facing review workstation: a queue of households, the AI eligibility suggestion, and the review steps (independent decision → see the suggestion → rate it → final decision). |
| `Oversight Review.html` | Supervisor-facing dashboard: oversight of eligibility decisions across offices and caseworkers, with alerts and closed-alert reasons. |

### `experiments/` — simulation study

`simulation_metrics_en(1).html` is an exported Jupyter notebook: *"Simulation: do
the oversight metrics work?"*

It builds simulated caseworkers with deliberately different behaviours —
attentive, "sees but doesn't act", rubber-stamper, distrustful, fatigued — has
them review the 1,900 households of the S8 sample, and tests whether the
candidate metrics can separate them. It then simulates a year of production to
see whether and when a monitor notices a decline in oversight, and computes the
audit size needed to detect a 15-point drop.

Metrics examined include switch fraction, mean WOA (weight on advice), WOA
discrimination (WOA when the AI is right minus when it is wrong),
judgment–action inconsistency, correct override, over-reliance and
under-reliance.

Main findings, as stated in the notebook:

- Correct override on its own rewards whoever overrides everything — always
  report the four measures together.
- Switch fraction and WOA measure *how much* the AI is followed, not whether it
  should be; use them for change over time, not as a level.
- WOA discrimination is the only measure that separates the attentive profile
  from all the others.
- Judgment–action inconsistency detects "sees but doesn't act" without needing
  the right answer — hence the main metric of the daily monitor.
- Metrics without a reference detect a decline in the same month; verification
  sentinels are slower. So: a two-level monitor.
- The original design has power 0.30 for a 15-point drop; roughly 8 discordant
  cases per caseworker and 25 caseworkers per group are needed (at σ = 0.9).

The notebook is explicit about its limits: the profile parameters are plausible
assumptions, not estimates. It shows that the metrics *can* separate those
behaviours, not that real caseworkers behave that way. All results are
properties of the simulation on S8.

Note: the notebook imports `simcore.py` (simulation) and `didattica_en.py`
(figures), which are not yet in this repository — the exported HTML includes all
code and output, but is not re-runnable as-is.

### `references/` — background literature

Papers on over-reliance on AI, trust calibration, advice taking and
accountability, including Buçinca et al. on cognitive forcing functions and
Mohamud (2025) on accountability in the humanitarian sector.

These PDFs are included for the team's convenience and remain under their
original publishers' copyright. They are not covered by any licence granted by
this repository.
