# 01: `/datamap-okf`, an example sub-skill for OKF bundles

**Status:** needs-triage

**What to build:** A sub-skill of `/datamap`, provisionally `/datamap-okf`, that knows how to turn an OKF (Open Knowledge Format) bundle into a datamap. It holds the OKF-specific knowledge: which files in a bundle are documents, how to split or combine them into points, and what to use for each point's `id`, `text`, `title` and `url`. It writes `documents` and then hands off to Seshette's scribes for the rest of the pipeline. Any agent that is datamapping can notice an OKF bundle and use this specialist instead of improvising.

**Why it lives here:** It's a cookbook example (`docs/terminology.md`). The Scrolls carry a few of these, for sources that are widely used. Nearly everyone will have an OKF repo, so it's the natural first thing to try: "your first `/datamap`: map your own OKF and see what's in it". It is also a simple, readable case of a source-specific caller, so someone with a niche format can study it and build their own mapper, using the Scrolls like an SDK. (This replaces the 2026-10-25 plan that kept all source-specific mappers, OKF included, out of the Scrolls.)

**Shape:**

- A thin caller: OKF knowledge plus a hand-off to Seshette. No pipeline code of its own.
- Written to be read: short, commented, and explicit about which parts are OKF-specific and which you'd change for another format.
- Uses the same `documents` contract as any other caller (spec, "Caller"), and gets the same cleaning advice as `/datamap` on a folder (`.scratch/seshette/issues/11-folder-ingest.md`).
- Ships the credits file like any other build (CLAUDE.md, "Citations and licenses").

**Open questions:**

- [ ] Name and invocation: `/datamap-okf` as its own skill, or `/datamap okf` routed by `/datamap`? Same choice applies to `02-datamap-chroma.md`.
- [ ] Does `/datamap` detect an OKF bundle and suggest this sub-skill on its own?
- [ ] What's in an OKF bundle that matters for mapping: one point per file, per section, or per entry? Work this out from the OKF format docs, not from memory.
- [ ] Which public OKF bundle is the worked example?

**Acceptance:**

- [ ] `/datamap-okf` on an example OKF bundle produces a datamap that passes the run checker, plus its credits file.
- [ ] A reader can see, in one pass, which parts to change to map a different format.

**Blocked by:** `.scratch/seshette/issues/06-tracer-bullet-500-sample.md`

Related: `02-datamap-chroma.md`, `.scratch/seshette/spec.md`.
