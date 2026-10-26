# Upstream code bases

Each directory here is a git submodule: an upstream repo, pinned to a
commit and kept unmodified as reference code for how King Tutte tools
are meant to be used. A plain clone leaves them empty. See
[Getting the submodules](../Readme.md#getting-the-submodules).

This page lists each code base with its license and what to cite when
you use it. The BibTeX is in [`citations.bib`](citations.bib); the
papers behind the code are annotated in
[`docs/papers/index.md`](../docs/papers/index.md).

Checked on 2026-10-25 against the commits pinned in this repo, from each
repo's `LICENSE` file, its README and its `pyproject.toml` or
`setup.py`. Re-check when you move a submodule to a newer commit.

## The code bases

| Submodule | Upstream | PyPI | Stage | License | Copyright |
|---|---|---|---|---|---|
| `vectorizers` | [TutteInstitute/vectorizers](https://github.com/TutteInstitute/vectorizers) | `vectorizers` | embed | BSD-3-Clause | John Healy, Leland McInnes, Colin Weir and contributors |
| `umap` | [lmcinnes/umap](https://github.com/lmcinnes/umap) | `umap-learn` | reduce | BSD-3-Clause | Leland McInnes |
| `pynndescent` | [lmcinnes/pynndescent](https://github.com/lmcinnes/pynndescent) | `pynndescent` | reduce (kNN graph) | BSD-2-Clause | Leland McInnes |
| `hdbscan` | [scikit-learn-contrib/hdbscan](https://github.com/scikit-learn-contrib/hdbscan) | `hdbscan` | cluster | BSD-3-Clause | Leland McInnes |
| `fast_hdbscan` | [TutteInstitute/fast_hdbscan](https://github.com/TutteInstitute/fast_hdbscan) | `fast_hdbscan` | cluster | BSD-2-Clause | Tutte Institute for Mathematics and Computing |
| `fast_plscan` | [JelmerBot/fast_plscan](https://github.com/JelmerBot/fast_plscan) | `fast_plscan` | cluster | BSD-3-Clause | Jelmer Bot |
| `evoc` | [TutteInstitute/evoc](https://github.com/TutteInstitute/evoc) | `evoc` | reduce + cluster | BSD-2-Clause | Tutte Institute for Mathematics and Computing |
| `toponymy` | [TutteInstitute/toponymy](https://github.com/TutteInstitute/toponymy) | `toponymy` | name clusters | MIT | Tutte Institute for Mathematics and Computing |
| `datamapplot` | [TutteInstitute/datamapplot](https://github.com/TutteInstitute/datamapplot) | `datamapplot` | render | MIT | Tutte Institute for Mathematics and Computing |
| `glasbey` | [lmcinnes/glasbey](https://github.com/lmcinnes/glasbey) | `glasbey` | render (palettes) | MIT | Leland McInnes; Sergey Alexandrov |
| `thisnotthat` | [TutteInstitute/thisnotthat](https://github.com/TutteInstitute/thisnotthat) | `thisnotthat` | interactive labeling | BSD-3-Clause | Benoit Hamelin, Leland McInnes and contributors |
| `temporal-mapper` | [TutteInstitute/temporal-mapper](https://github.com/TutteInstitute/temporal-mapper) | `temporal-mapper` | time-evolving maps | BSD-3-Clause | Kaleb Ruscitti, Leland McInnes |
| `tutorials` | [TutteInstitute/tutorials](https://github.com/TutteInstitute/tutorials) | none | examples | MIT | Tutte Institute for Mathematics and Computing |

All thirteen are permissive licenses. They allow commercial use and
modification, and require only that the copyright notice and license
text go with any copy you redistribute. The BSD-3-Clause ones also
forbid using the authors' names to endorse your product.

## What to cite

Keys refer to [`citations.bib`](citations.bib). Where a README asks for
a citation, the request is quoted from the upstream file named.

- **umap**: [README, "Citation"](https://github.com/lmcinnes/umap#citation)
  (`umap/README.rst`). Cite `mcinnes2018umap-software` (JOSS) whenever
  you use the software and `2018arXivUMAP` for the algorithm. Add
  `SMG2020` for Parametric UMAP, `NBC2020` for densMAP, and `Healy2024`
  if the Nature Primer helped you.
- **hdbscan**: [README, "Citing"](https://github.com/scikit-learn-contrib/hdbscan#citing)
  (`hdbscan/README.rst`). Cite `mcinnes2017hdbscan` (JOSS) for the
  software, `mcinnes2017accelerated` for the accelerated algorithm, and
  `bot2025flasc` if you use branch detection.
- **fast_hdbscan**: no citation request; its README's "References"
  names the papers it adapts. Cite `mcinnes2017accelerated`,
  `campello2013density`, `bot2025flasc` (branch detection) and
  `bot2025plscan` (PLSCAN mode), plus the `fast_hdbscan` entry.
- **fast_plscan**: [README, "Citing"](https://github.com/JelmerBot/fast_plscan#citing)
  (`fast_plscan/README.md`). Cite `bot2025plscan`.
- **evoc**: README, "References" (`evoc/README.rst`). EVōC's own
  algorithm is unpublished, and the README asks you to cite
  `bot2025plscan` instead. Add the `evoc` entry.
- **glasbey**: no citation request; its README's "References" lists
  `glasbey2007colour` first. Cite that plus the `glasbey` entry.
- **pynndescent**: no citation request. Cite `dong2011nndescent` (the
  algorithm) plus the `pynndescent` entry.
- **datamapplot**, **toponymy**, **vectorizers**, **thisnotthat**,
  **temporal-mapper**: no paper and no citation request. Cite the repo:
  `datamapplot`, `toponymy`, `vectorizers`, `thisnotthat`,
  `temporal_mapper`, with the version you used.
- **tutorials**: examples, not a dependency. Credit the repo if you
  adapt a notebook. The MIT license requires keeping its copyright
  notice.

## Licenses of what they install

A pipeline runs more than these thirteen repos: `pip install` pulls in
their dependencies too. Here are the licenses of the direct runtime
dependencies, as reported by PyPI. Dependencies of those dependencies
are not covered, so generate the full list for your own build (see
below).

**One exception to "permissively licensed": `pylabeladjust` is
GPL-3.0.** It is a required dependency of `datamapplot`, and
`import datamapplot` loads it (`datamapplot/text_placement.py` imports
it at module level). Any environment that runs DataMapPlot therefore
contains GPL-3.0 code. GPL obligations generally apply when you
*distribute* the software, for example in an app, container image or
bundled environment, not when you run it to make a datamap. This is not
legal advice: if you plan to redistribute a pipeline commercially,
check this with someone qualified. Upstream:
[MNoichl/pylabeladjust](https://github.com/MNoichl/pylabeladjust).

Other licenses worth knowing about, all permissive or limited in scope:

| Dependency | License | Pulled in by | Note |
|---|---|---|---|
| `tbb` | Intel Simplified Software License | `umap-learn[tbb]` (optional) | Permissive but not OSI-approved; skip the extra if you need OSI-only. |
| `tqdm` | MPL-2.0 AND MIT | umap, evoc, toponymy, temporal-mapper | MPL-2.0 is file-level copyleft: only changes to tqdm's own files must be shared. |
| `colorcet` | CC-BY-4.0 | datamapplot, thisnotthat, `umap-learn[plot]` | The colormaps need attribution. |
| `litellm` | MIT, except its `enterprise/` directory | toponymy | The enterprise features are under a separate license. |
| `llvmlite` | BSD-2-Clause AND Apache-2.0 WITH LLVM-exception | pynndescent, numba | Permissive. |
| `matplotlib` | PSF-based matplotlib license | datamapplot, glasbey, fast_plscan, ... | Permissive. |

Everything else in the direct dependency set is BSD, MIT, Apache-2.0
or PSF-2.0: numpy, scipy, scikit-learn, numba, pandas, joblib, dask,
datashader, holoviews, bokeh, panel, param, pyarrow, jinja2, requests,
httpx, platformdirs, importlib-resources, rcssmin, rjsmin, scikit-image,
seaborn, colorspacious, networkx, plotly, adjustText, wordcloud,
cmocean, apricot-select, datasets, transformers, tokenizers, tenacity,
tensorflow (`umap-learn[parametric_umap]`), llama-cpp-python
(`toponymy[llama]`) and typing_extensions.

Interactive datamaps also load JavaScript in the viewer's browser.
DataMapPlot's HTML pulls deck.gl, d3, d3-cloud, Apache Arrow and jQuery
from unpkg. These are MIT, ISC, BSD and Apache-2.0 licensed, and none
is copyleft.

Models are licensed separately from code. The embedding model, and any
LLM Toponymy calls to name clusters, come with their own licenses and
terms. The current default embedder, `all-MiniLM-L6-v2`, is Apache-2.0.

## Credits as a build artifact

Every datamap built from these repos should ship with a credits file,
for example `CREDITS.md` next to the datamap's HTML. It lets anyone
using the datamap see at a glance that the pipeline is open and
permissively licensed, and credits the people who made it. List:

1. **Each King Tutte package that ran**, with its version, license and
   repo URL. Read versions and licenses from the installed environment
   (`importlib.metadata`), not from this page.
2. **The full license list for the environment**, generated, for
   example with
   [`pip-licenses`](https://github.com/raimon49/pip-licenses) (MIT):
   `pip-licenses --format=markdown --with-urls`. Call out anything that
   isn't permissive, as `pylabeladjust` is today.
3. **The embedding model and any LLM used**, with their licenses.
4. **References**: the citations for the packages that ran, from
   [What to cite](#what-to-cite), with BibTeX from
   [`citations.bib`](citations.bib).

There is no integrated pipeline in this repo yet. This is the
requirement Seshette, the `/datamap` skill, must meet when it produces a
datamap.
