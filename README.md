# Quantum Machine Learning — binary classifiers for noisy datasets

Reference implementation and benchmarking notebooks for hybrid classical–quantum binary
classifiers evaluated on noisy, non-convex synthetic datasets.

The work combines hybrid classical–quantum neural networks, parametric (variational) quantum
circuits and data re-uploading, and benchmarks the resulting "FULL HYBRID" models against both
existing quantum classifiers and standard classical classifiers. Performance is measured by the
area under the ROC curve (ROC AUC), with particular attention to how each model degrades as
noise in the dataset increases.

## Citation

If you use this code, please cite the peer-reviewed article:

> N. Schetakis, D. Aghamalyan, P. Griffin and M. Boguslavsky,
> "Review of some existing QML frameworks and novel hybrid classical–quantum neural networks
> realising binary classification for the noisy datasets",
> *Scientific Reports* **12**, 11927 (2022).
> https://doi.org/10.1038/s41598-022-14876-6

Earlier preprint version: [arXiv:2111.03372](https://arxiv.org/abs/2111.03372).

```bibtex
@article{schetakis2022qml,
  title   = {Review of some existing QML frameworks and novel hybrid classical--quantum
             neural networks realising binary classification for the noisy datasets},
  author  = {Schetakis, N. and Aghamalyan, D. and Griffin, P. and Boguslavsky, M.},
  journal = {Scientific Reports},
  volume  = {12},
  pages   = {11927},
  year    = {2022},
  doi     = {10.1038/s41598-022-14876-6}
}
```

## Repository layout

### `paper-2022-scientific-reports/` — classifier models and benchmarks

| Notebook | Contents |
| --- | --- |
| `Generate Dataset 2D.ipynb` | Generation of the synthetic non-convex 2-dimensional datasets, with controllable noise |
| `Generate Dataset 3D.ipynb` | The 3-dimensional equivalent |
| `VC.ipynb` | Variational classifier (VC) — parametric quantum circuit baseline |
| `DRC.ipynb` | Data re-uploading classifier (DRC) |
| `HYBRID v5.6 - 2Q.ipynb` | Full hybrid classical–quantum model on 2 qubits; loads a pre-trained classical model and freezes its weights for transfer learning |
| `Classical Classifiers comparison.ipynb` | Classical classifier baselines used for the benchmark comparison |

### Root — demos and model variants

| Notebook | Contents |
| --- | --- |
| `Pennylane DEMO v4.ipynb` | End-to-end walkthrough of the quantum binary classifier in Keras: parameters, dataset generation and pre-processing, quantum node construction, hybrid model training, prediction grids |
| `QML - HYBRID v6.1 -  Transfer Learning.ipynb` | Hybrid model with hot-start / transfer learning, including the weight-freezing step |
| `VCDR_ST2_-pi_pi.ipynb` | VC/DRC variant evaluated on dataset ST2 over the [-π, π] input range |
| `Demo v5.ipynb` | Earlier demonstration notebook |
| `Hybrid_lstm_V4.3 - run1.ipynb` | Hybrid model with an LSTM layer (time-series variant, outside the scope of the paper above) |

### Circuit terminology used in the notebooks

- **Block** — one `AngleEmbedding` followed by `StronglyEntanglingLayers`
- **Layer** — a repetition of `StronglyEntanglingLayers` within a block
- `Q`*n* in a filename denotes the qubit count, `B`*n* the number of blocks, `L`*n* the layers per block

## Installation

Developed against Python 3.8.

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

PennyLane plugin backends used across the notebooks (install the ones you need):

```bash
pip install pennylane-sf pennylane-qiskit pennylane-cirq pennylane-forest pennylane-qsharp
pip install amazon-braket-sdk amazon-braket-pennylane-plugin
```

## Reproducibility notes

- The notebooks are committed with their stored outputs, so the figures and ROC AUC values can be
  read without re-running anything.
- Some notebooks were run on Windows and contain absolute paths from that machine in their saved
  outputs and, in places, in code cells. Expect to adjust paths before re-running.
- Quantum circuits are executed on simulators, not on hardware.

## License

Released under the MIT License — see [LICENSE](LICENSE).

## Authors

Nikolaos Schetakis, with co-authors as listed in the citation above.
