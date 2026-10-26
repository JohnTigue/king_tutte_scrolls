# 02: `/datamap-chroma`, an example sub-skill for a Chroma vector database

**Status:** needs-triage

**What to build:** A sub-skill of `/datamap`, provisionally `/datamap-chroma`, for people who want to see what's in a vector database. It reads a Chroma collection's ids, documents, metadata and stored embeddings, writes Seshette's `documents` and `embeddings` tables, and starts the pipeline at the Reducer, skipping the Embedder. It's the second cookbook example (`docs/terminology.md`), next to `01-datamap-okf.md`: OKF shows a caller that starts from documents, Chroma shows one that already has embeddings.

**Shape:**

- A thin caller like `/datamap-okf`: Chroma knowledge plus a hand-off to Seshette.
- Uses the stored vectors as is, through the mid-pipeline path in `.scratch/seshette/issues/10-mid-pipeline-and-caller-embeddings.md`. Records which embedding model made them, if the collection says so, for the credits file.
- Falls back to re-embedding with the default embedder when a collection has documents but no stored vectors.
- Check `chromadb`'s license and its resolved dependencies (INAL, `.scratch/inal/`) before calling the example permissive.

**Open questions:**

- [ ] Local persistent Chroma only, or also a Chroma server?
- [ ] Which metadata field, if any, becomes `title` or `url`?
- [ ] Which public dataset makes the worked example collection?

**Acceptance:**

- [ ] `/datamap-chroma` on an example collection produces a datamap that passes the run checker in mid-pipeline mode, plus its credits file.
- [ ] The Embedder does not run when the collection has stored vectors.

**Blocked by:** `.scratch/seshette/issues/10-mid-pipeline-and-caller-embeddings.md`

Related: `01-datamap-okf.md`.
