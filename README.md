Dear Reviewers!
In order to prove the paper enhancement we provide you some ablations studies on your request.

## Structure
This repository is organized around the rebuttal updates and supporting ablations.

As stated in the paper, HASBoost "reduces split-search cost within the sequential boosting framework" and shows "dataset-dependent behavior". The materials below are selected to document these two points directly.

### Figures
- `figures/computational overhead.png` — overhead attribution plot showing the relative share of weighting/sketching operations in total training time.
- `figures/inference_time_vs_f1_by_stabilization_threshold.png` — impact of stabilization threshold $\theta$ on inference-time vs quality trade-offs.
- `figures/inference_time_vs_train_time_by_stabilization_threshold.png` — relation between training and inference time across $\theta$ settings; helps visualize scheduler effects.
- `figures/method_scheme.png` — method diagram explaining stability-gated activation and adaptive sketching flow.
- `figures/smoothing_alpha_small_c.png` — effect of EMA smoothing parameter $\alpha$ in low column-budget settings.
- `figures/train_time_vs_f1_by_smoothing_alpha.png` — global $\alpha$ sensitivity for train-time vs F1 trade-offs.
- `figures/results.png` — consolidated results table snapshot from the current paper revision.

### Total dataset suite 
| Dataset | Samples | Labels/Classes | Features |
|---|---:|---:|---:|
| age\_prediction | 6234 | 8 | 16 |
| cifar10 | 50000 | 10 | 100 |
| genbase | 662 | 27 | 1186 |
| mediamill | 43907 | 101 | 120 |
| mnist | 70000 | 10 | 100 |
| yeast | 2417 | 14 | 103 |
| MoA | 23814 | 206 | 876 |
| Delicious | 16105 | 983 | 500 |

## Comments 

**Q:** What is the computational overhead of the different sketching algorithms?

**Answer**
- We added a dedicated overhead analysis block in the appendix: **“Contribution of Weighting and Sketching”**.
- We now report both a table and a figure quantifying overhead contribution to total train time (mean and std).
- This directly isolates the cost of weighting/sketching from the rest of boosting and clarifies when overhead is negligible vs dominant (see `computational overhead.png`).

**Table: Contribution of weighting variants to sketching overhead (from paper)**
| Metric | Linear | Sigmoid |
|---|---:|---:|
| Sketch proportion, % | 1.25 ± 0.35 | 1.33 ± 0.36 |
| Train time (ms) | 4371.70 ± 1148.70 | 3252.91 ± 1353.56 |

**Q:** claims are overstated; no uncertainty bars; limited alignment between motivation and evaluated scales; no sensitivity analysis

**Answer**
- **Uncertainty reporting:** runtime/quality reporting now includes dispersion statistics in added ablation blocks (mean ± std where applicable).
- **Sensitivity analysis added:** explicit hyperparameter sweep over $\theta$, $\alpha$ with relative comparisons vs SketchBoost under matched budgets.

**Q** Can you provide results for more metrics and larger multi-label datasets?

**Answer**
- We expanded the benchmark suite to include additional datasets beyond the earlier smaller set (including true multi-label settings such as Delicious and MoA in the final suite).
- We added richer quality-time analysis in the new ablation figures/tables and expanded regime-dependent discussion.
- Weighted F1 remains the primary reported task metric, now supported with macro/micro reporting in the full synthetic table.

**Q** Can you add the ablations promised for Appendix B?

**Answer**
- Yes. Appendix now includes the promised ablations:
  - contribution of weighting/sketching to total train time,
  - stabilization-threshold ($\theta$) sensitivity,
  - smoothing-factor ($\alpha$) sensitivity.

The visualizations for metric and efficiency changes are provided in `computational overhead.png`, `inference_time_vs_f1_by_stabilization_threshold.png`, and `smoothing_alpha_small_c.png`.