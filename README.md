# PyGLoBES

*A batteries‑included, pure‑Python re‑imagining of the classic **GLoBES** neutrino‑experiment toolkit*

---

## Why another GLoBES?

If you have tried to compile the original **GLoBES** you already know the drill:

* 😩 **C tool‑chain gymnastics** – autotools, Makefiles, and mysterious compiler errors.
* 🪫 **ROOT dependency hell** – hunting for the right ROOT version and environment variables.
* 🔒 **System‑wide installs** – scattered headers & libraries that break with every OS update.
* 🐧 **Linux‑only comfort‑zone** – Windows and M1/M2 macOS users are left out in the cold.

We love what GLoBES can do, but not what it takes to *get there*.

### The PyGLoBES magic ✨

**PyGLoBES** is a *from‑scratch* Python implementation – **not** a thin wrapper – so you can:

1. **`pip install pyglobes`** and start running oscillation studies in seconds.
2. Stay in the **Python ecosystem** you already use (NumPy, SciPy, Jupyter).
3. Prototype, debug and visualise **interactively** without recompiling.
4. Use the same AEDL files you know from GLoBES – or build new ones in plain JSON/YAML.
5. Enjoy first‑class **type hints**, docstrings and automated tests.

---

## Key Features

| Category           | PyGLoBES                                             | Classic GLoBES           |
| ------------------ | ---------------------------------------------------- | ------------------------ |
| Language           | Pure Python ≥3.9                                     | C99 + autotools          |
| AEDL support       | Full parser + validator                              | Native                   |
| Probability engine | NUFAST by peter denton ( we will do smthn abt it)    | Native                   |
| Detector model     | Modular smearing / efficiency loaders                | Hard‑coded C hooks       |   ??
| Analysis           | Built‑in χ², scans, plotting                         | DIY C / external scripts |    ??
| Extensibility      | Python plugins, JIT via numba                        | Requires C plugins       |   ??

---

## Installation

```bash
pip install pyglobes
# Optional speed‑ups
pip install "pyglobes[numba]"
```

<details>
<summary>Need the bleeding edge?</summary>

```bash
pip install git+https://github.com/your‑org/pyglobes.git
```

</details>

---

## Quick‑Start (360 km ESSνSB example)

```python
import pyglobes as pg
from pyglobes.presets import essnusb_360km

experiment = essnusb_360km()
result = experiment.event_rates()
result.plot_stack("reco_energy")
```

➡️ *Under the hood*: PyGLoBES loads the AEDL, cross‑sections, fluxes and smearing matrices, computes oscillation probabilities with matter effects, and gives you a tidy `pandas.DataFrame` ready for analysis.

---

## Migrating from C GLoBES      ## i dont know how this will turn out tho.. lets seeeeee 

| You did this in C…                        | …do this in Python                              |
| ----------------------------------------- | ----------------------------------------------- |
| `glbInitExperiment("essnusb.glb");`       | `exp = pg.Experiment.from_aedl("essnusb.aedl")` |
| `glbSetOscParams(p, GLB_THETA12, value);` | `exp.params.theta12 = value`                    |
| `glbDefineParams(p, …)`                   | `pg.Params(...)`                                |
| `glbChiSys();`                            | `pg.analysis.chi2(exp, systematics=True)`       |

No `Makefile`. No `libglobes.so`. Just Python.

---

## Roadmap

* **v0.4** – ??
* **v0.5** – 
* **v1.0** – i hope this workssss

See the [open issues](https://github.com/your‑org/pyglobes/issues) and come help!

---

## Contributing

1. Fork the repo and create your branch (`git checkout -b feature/awesome`).
2. Install dev dependencies: `pip install -e .[dev]`.
3. Run `pre‑commit install` and make sure `pytest` passes.
4. Submit a pull request – GitHub Actions will run the full test suite.

We adhere to the [Contributor Covenant](CODE_OF_CONDUCT.md).

---

## Citation

If PyGLoBES helps your research, please cite us.

```bibtex
@misc{pyglobes2025,
  author       = {Somy, Edwin and Contributors},
  title        = {{PyGLoBES}: A Pure‑Python Toolkit for Neutrino Event Simulation},
  year         = {2025},
  howpublished = {\url{https://github.com/your‑org/pyglobes}},
  note         = {Version 0.4.0}
}
```

---

## License

PyGLoBES is distributed under the permissive **MIT License** – use it, fork it, embed it.

---

### Acknowledgements

PyGLoBES draws inspiration from the original GLoBES authors and the wider neutrino‑physics community. Thank you for paving the way!
