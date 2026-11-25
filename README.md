# RadioVISTA: Seeing the Invisible

**How Vision-Language Models Read, Predict and Trace Radio Fields**

[Dataset](https://huggingface.co/datasets/ScreeperC/radiovista-bench) ·
[Scene engine](https://github.com/RadioVISTA/radiovista) ·
[Website](https://radiovista.github.io)

Operating in the physical world requires reasoning beyond what cameras capture. In a city, radio
signals are invisible to the lens, yet their strength is governed by the buildings and streets an
image does show. **RadioVISTA** asks whether vision-language models can infer the invisible field
from these visible structures, and gives them the data to learn it.

## Why RadioVISTA

- **Any city on Earth.** A label-free engine turns any coordinate into a ray-traceable 3D city,
  built from a uniform global baseline of buildings, terrain, land cover and roads.
- **Exact answers, zero annotation.** Every answer is computed from the simulated field, so a new
  city or physical setting yields a fresh, exactly graded test suite.
- **Controlled physics.** Each scene is a factorial experiment over three environments and four
  propagation modes. Matched single-factor counterfactuals isolate reflection, scattering,
  diffraction and ground materials one at a time.
- **Physically validated.** In free space the solver agrees with the Friis law within 3 dB on 98%
  of 3,000 distance rings.
- **Global and held out.** 100 real cities on six continents, with test cities strictly disjoint
  from training.
- **Benchmark and training set in one.** The same engine synthesizes training data for unseen
  cities, ready for SFT and reinforcement fine-tuning.

## Twelve tasks, three competences

| Type | Tasks | What it tests |
|---|---|---|
| **Geometry** | G1 transmitter height, G2 line of sight, G3 building occlusion, G4 path reachability | Whether a direct or one-wall path exists |
| **Propagation** | P1 free-space loss, P2 reflection, P3 scattering, P4 diffraction | How the signal responds to one physical change |
| **Field** | F1 field reading, F2 mode prediction, F3 material prediction, F4 joint prediction | Reading and predicting the full field |

| Split | Cities | Questions |
|---|---|---|
| train | 68 | 4,735 |
| validation | 15 | 1,055 |
| test | 17 | 1,200 |

## Key findings

- **Field-path dissociation.** Frontier VLMs accurately judge where a field is strong, but fail
  to tell whether a single direct or one-wall path exists.
- **Open models fail earlier.** They struggle to read the field itself and score below random
  guessing even when credited for any of four attempts.
- **Engine data teaches the field.** Fine-tuning a 9B open model on unseen cities brings it close
  to frontier proprietary models on field tasks.
- **Path tracing stays out of reach.** Neither supervised nor reinforcement fine-tuning improves
  single-path geometry, which points to a clear open problem.

## Release roadmap

We release RadioVISTA in stages, so that each part is usable on its own from day one.

- [x] **Paper & official website** — [Paper](https://arxiv.org/abs/2611.28123) and [project website](https://radiovista.github.io).
- [x] **Dataset** — All 12 tasks with images and answers, and train / validation / test splits on [Hugging Face](https://huggingface.co/datasets/ScreeperC/radiovista-bench).
- [ ] **Evaluation toolkit** (this repo) — Official answer parser and scorer, API, vLLM and Transformers backends, the exact prompts of the paper, Pass@k and correction protocols, official scores and raw predictions, reproducible commands, and a public leaderboard.
- [ ] **Training baselines** — SFT and GRPO recipes and the fine-tuned Qwen3.5-9B LoRA weights.
- [ ] **Scene engine** — [`radiovista`](https://github.com/RadioVISTA/radiovista): any coordinate to a ray-traced city and new questions, with the full raw simulated fields (`ScreeperC/radiovista-raw`).

## Related repositories

| Repository | Contents |
|---|---|
| [HF `ScreeperC/radiovista-bench`](https://huggingface.co/datasets/ScreeperC/radiovista-bench) | Benchmark questions, images and answers |
| [`RadioVISTA/radiovista`](https://github.com/RadioVISTA/radiovista) | Scene engine that generates the dataset |
| [`RadioVISTA/RadioVISTA.github.io`](https://github.com/RadioVISTA/RadioVISTA.github.io) | Project website |

## Citation

```bibtex
@article{zhu2026radiovista,
  title   = {Seeing the Invisible: How Vision-Language Models
             Read, Predict and Trace Radio Fields},
  author  = {Zhu, Yiyang and Li, Xin and Liu, Guangyuan and
             Liu, Ziheng and Zhang, Jiayi and Yuen, Chau},
  journal = {arXiv preprint arXiv:2611.28123},
  year    = {2026},
  doi     = {10.48550/arXiv.2611.28123},
  url     = {https://arxiv.org/abs/2611.28123}
}
```

## License

Code: [GPL-3.0-only](LICENSE). Data: see the dataset card on Hugging Face.
