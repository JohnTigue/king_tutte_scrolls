# King Tutte Datamap Scrolls

A curation/documentation repo (not an application) for building "King Tutte
pipelines": permissively licensed open source toolchains, mostly from the Tutte
Institute (UMAP, HDBSCAN, DataMapPlot, Toponymy, EVōC, ...), that turn
collections of embedding vectors into interactive datamaps.

The goal is Seshette, a generic `/datamap` Agent Skill: point it at a
collection of documents (or embeddings) and it runs a King Tutte pipeline
locally to produce an interactive datamap. Source-specific mappers live in
their own repos and use Seshette as a component; keep source-specific
material out of this repo.

## References


The Connoiter blog is the main documentation for what a King Tutte Pipeline is:
https://connoiter.com/blog/


## Layout

- `Readme.md` — the main narrative and project direction.
- `docs/terminology.md` — descriptions of various project specific nouns.
- `docs/agents/` — configuration for Matt Pocock's engineering skills.
- `.scratch/` — specs and issues (the local-markdown issue tracker).
- `docs/talks/` — curated datamapping tech talks.
  - TODO: A very early work in progress
- `docs/papers/` — annotated bibliography of datamapping papers
  (`index.md`) with BibTeX for each in `citations.bib`. The repo is used commercially: local PDFs in `pdfs/` only
  for CC BY/CC0 papers. Never copy in anything NC, ND, arXiv-default or
  publisher-copyright; link it with a short description instead.
- `tools/` — curation tools packaged as Agent Skills (symlinked into
  `.claude/skills/`). `tools/youtube-transcripts/` pulls talk transcripts +
  metadata into `docs/talks/`, driven by `docs/talks/by_tutte/talks.json`.
- `library/` — notes on specific techniques and papers.
- `images/` — assets used by the README.
- `repos/` — upstream git submodules, kept as reference code for how the
  tools are meant to be used. Don't edit the submodules; they track upstream.
  `repos/README.md` (ours) indexes them with each one's license, what it
  asks you to cite, and the licenses of what it installs; `repos/citations.bib`
  has the BibTeX for using the code.
  - Pipeline stages: `vectorizers` (embed), `umap` + `pynndescent` (reduce),
    `hdbscan` / `fast_hdbscan` / `fast_plscan` / `evoc` (cluster), `toponymy` (name
    clusters), `datamapplot` + `glasbey` (render, colour palettes).
  - Examples and adjacent tools: `tutorials`, `thisnotthat` (interactive
    labeling), `temporal-mapper` (time-evolving maps).
  - Everything after `umap`/`hdbscan` is a shallow clone (`datamapplot` alone
    is ~900 MB).
  - A plain clone leaves `repos/*` empty. If they are, run
    `git submodule update --init` (it honours the shallow setting) before
    looking for reference code; don't conclude the code is missing.
  - Exception: in a git worktree (for example an implementer subagent's),
    never init the submodules; each init would copy about 2 GB. They are
    read-only reference, so read them from the main checkout instead: it is
    the parent folder of `git rev-parse --path-format=absolute --git-common-dir`,
    and the code is in its `repos/`.

## Conventions

- Only curate material that is permissively licensed, and credit/cite upstream sources.
- There's no integrated pipeline yet, so don't describe one as runnable unless
  the code for it is actually in the repo.

## Citations and licenses

The upstream researchers are credited through citations, so citing them
is a requirement, not a courtesy. Showing that a pipeline is
permissively licensed is part of the same job.

- When you build a datamap, or write code or docs that use these code
  bases (including in another repo that uses Seshette), ship a credits
  file with it, as described in `repos/README.md` under "Credits as a
  build artifact": each package that ran with its version and license,
  the generated license list for the environment, the models used, and
  references. Cite what each code base asks for (`repos/README.md`,
  "What to cite") using `repos/citations.bib`. In a README, notebook or
  datamap page, add a short "References" or "Built with" section too.
- Not everything is permissive: `datamapplot` requires `pylabeladjust`
  (GPL-3.0). Say so whenever you describe a pipeline as permissively
  licensed, and don't call a build permissive without checking its
  resolved environment.
- Seshette's `SKILL.md` must carry these instructions, because agents
  in other repos read the skill, not this file.
- When a submodule moves to a new commit, re-check its license and
  citation request and update `repos/README.md` and `repos/citations.bib`.
- Every paper added to `docs/papers/index.md` gets a `**Cite:**` line
  and a BibTeX entry in `citations.bib`. Use the citation the upstream
  repo asks for, copied unchanged, when there is one. Otherwise build it
  from the DOI's Crossref record or the arXiv API, and never from memory.

## Agent skills

### Issue tracker

Issues and specs live as local markdown files under `.scratch/<feature>/`. See `docs/agents/issue-tracker.md`.

### Triage labels

The five default triage roles, recorded as a `Status:` line in each issue file. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context; the glossary is `docs/terminology.md`. See `docs/agents/domain.md`.
