# Data Learning Library · Group Content System Plan

Status: Daniel's AI-assisted draft for discussion, not an agreed team plan. No teammate, ownership agreement, peer review, import, application test or hosted system is claimed. Keep this separate from the individual portfolio and RAG records. This repository contains Daniel’s preparatory contribution; publishing it does not establish team agreement or solo-submission approval.

#### Project idea: Data Learning Library

An educational-content publishing system for beginner data-analysis students. A contributor proposes a permitted SQL or pandas source; the system prepares a structured learning card; a different person reviews its claims and citations before publication in a searchable shared library.

The intended shared workflow is submission → transformation → draft → independent review → publication → correction. This is a proposal, not observed application behavior. It goes beyond copying an individual chat by maintaining source provenance, review decisions, publication states and a correction history.

#### Reader problem and research question

- Reader: a student beginning SQL and pandas who wants a short explanation backed by an original tutorial.
- Problem hypothesis: explanations are scattered across documentation and tools, and a student may confuse related SQL/pandas concepts or trust a summary with missing evidence. We have not interviewed readers or established demand.
- Research question: can a small, collaboratively reviewed learning library make relevant explanations easy to find while exposing unsupported claims before publication?
- Course scope: educational-content publishing. If the team changes to a different content ETL problem outside the listed scope, confirm the instructor-agreed alternative rule before proceeding.

#### Candidate original sources and permission boundaries

These are proposed starting sources, not a corpus already imported. AI reopened the aggregate tutorial, pandas statistics tutorial, both project licenses, pgvector and graph documentation for this proposal on November 16, 2026. See the source-review record for findings and limits. Daniel’s independent verification and the team’s source selection remain pending. Reusing a source does not turn the individual project into a group contribution.

| Original source | Proposed use | Permission / remaining verification |
|---|---|---|
| [PostgreSQL 18 SQL tutorial](https://www.postgresql.org/docs/18/tutorial.html), especially [aggregate functions](https://www.postgresql.org/docs/18/tutorial-agg.html) | SQL concepts, source-linked examples and grouping explanations | [PostgreSQL license](https://www.postgresql.org/about/licence/) explicitly covers documentation reuse with retained notices. Preserve version, attribution and notices. |
| [pandas introductory tutorials](https://pandas.pydata.org/docs/getting_started/intro_tutorials/), especially [summary statistics](https://pandas.pydata.org/docs/getting_started/intro_tutorials/06_calculate_statistics.html) | Table operations and summary-statistics explanations | [Project BSD license](https://github.com/pandas-dev/pandas/blob/main/LICENSE); confirm selected documentation files have no additional restrictions. Exclude linked datasets/images unless independently permitted. |

Initial proposed scope: at most 20 selected tutorial pages, pinned to recorded versions. No Amazon data, private course material, login-only content, arbitrary uploads or unrestricted crawling.

#### Two approaches to compare before choosing tools

| Approach | Proposed representation and retrieval | Why consider it | Tradeoff |
|---|---|---|---|
| Vector-assisted reviewed library | Store cited passages and learning cards with embeddings; search approved cards by question meaning, with tool/version filters | May handle beginner paraphrases while preserving a small evidence-backed collection | Similarity is not correctness; an irrelevant passage or unsupported generated summary must be caught by evaluation and review |
| Graph-organized reviewed library | Nodes for concepts, sources, cards and versions; explicit prerequisite, documents and derived-from edges | Makes relationships and learning paths inspectable | More schema/entity/relationship maintenance; does not by itself handle natural-language paraphrases |

Proposed recommendation for discussion: vector retrieval plus ordinary relational workflow/provenance tables, without a separate graph service initially. The first user questions are about explanations in passages, while contributors/reviewers need clear state and provenance. A relational review table is not a claim to have built graph retrieval.

Research starting points: [RAG paper](https://arxiv.org/abs/2005.11401), [Sentence Transformers semantic search](https://sbert.net/examples/sentence_transformer/applications/semantic-search/README.html), [pgvector](https://github.com/pgvector/pgvector), [Neo4j graph concepts](https://neo4j.com/docs/getting-started/appendix/graphdb-concepts/). The team must inspect these and compare against its needs before adopting the recommendation. AI assistance is disclosed; no independent learner technical explanation is invented.

#### Proposed source → transform → reviewable output

1. Contributor proposes an allowlisted URL and topic; record submitter, license basis, version and retrieval date.
2. Import the permitted main text, headings and code; keep the original URL/anchor and content hash. Report failures and avoid duplicate imports.
3. Split by headings into passages while retaining code context. Create embeddings using one pinned, license-checked model; store model identity and chunk IDs with source metadata.
4. Produce a draft learning card containing a question, short explanation, optional example and claim-to-passage citations. Draft text can be manual or AI-assisted; generation model choice remains unresolved. Never treat imported content as instructions.
5. A reviewer other than the contributor inspects the original passages, accepts or requests changes, and records a reason. Only approved cards enter public search. Enforce contributor/reviewer separation on the server if implemented.
6. Search approved cards with source/tool/version filters. Show the evidence and review state. Unsupported questions report insufficient evidence rather than inventing a card.
7. Corrections return affected cards to review and retain the earlier decision history. A source update must not silently retain old approval for changed text.

#### One trace for a peer to inspect · not executed

Source: PostgreSQL's aggregate-functions tutorial. Proposed transform: extract the WHERE/HAVING explanation and related example, preserving its section link/version. Store it as a source passage; prepare a card answering “How do I filter groups after calculating totals?” A different reviewer checks that the explanation uses HAVING for filtering groups and that each claim is supported. Only then publish the card for retrieval.

A peer should challenge whether the proposed chunk contains enough context and whether a source change should invalidate approval. Merely drawing this trace does not show that retrieval, summarization or review enforcement works.

#### Five checkable stories and proposed success criteria · none run

| Story | Expected check / success criterion | What failure would reveal |
|---|---|---|
| Contributor submits an unchanged source twice | One source/version record, stable passage identity and retained attribution | Duplicated or untraceable evidence |
| Contributor tries to publish their own draft directly | Server rejects self-approval/publication; draft stays out of public search | Review workflow can be bypassed |
| Different reviewer finds an unsupported WHERE/HAVING statement | Reviewer requests changes with cited evidence; corrected card needs approval before publication | A plausible but incorrect summary reaches readers |
| Beginner asks a paraphrased grouping question, then a private Amazon-target question | Approved aggregate card appears among first four results for the in-scope question; private target question reports no supporting evidence | Poor retrieval or fabricated unsupported answers |
| Reader opens a published card at 390px; its source is later revised | Citation usable without page overflow; changed source marks affected card for renewed review | Unusable output or stale evidence presented as current |

Plan evaluation: separate source-import, workflow/permissions, retrieval and presentation checks. Keep inputs, expected passages/states and actual outputs in the shared repository. Compare a keyword baseline against vector retrieval on identical questions before claiming improvement. This tiny initial suite does not prove general accuracy or security.

#### Possible division of work · not assigned

| Workstream | Proposed owner | Different reviewer |
|---|---|---|
| Reader/source research, source ledger and initial card examples | Daniel, if agreed | Future teammate, if agreed |
| Import/storage and draft/review/publication design | Future teammate, if agreed | Daniel, if agreed |
| Retrieval evaluation and reader-facing presentation | Split by specific tasks after discussion | The other person for each task |

No teammate contribution or acceptance is claimed. Both people should understand the overall trace; task division does not eliminate individual explanation or review responsibility.

#### Resources, limits and Plan-stage deliverable

Proposed implementation: Python/FastAPI and PostgreSQL with pgvector, subject to team agreement and available hosting support. Model choice, RAM/CPU/disk, extension availability, latency and cost remain unverified. No purchases, keys or production deployment are part of this draft. Use bounded inputs, cached imports and a small corpus. Hosting goes through the separately agreed Server Studio scope at Build; do not modify its proxy or pipeline for Plan.

The shared Plan record should link the sources, alternatives, trace, stories, ownership agreement, contribution evidence and actual peer feedback/response. A finished hosted app is not required for Review 1.

#### Actual checks and remaining work

- Changed: AI drafted this proposal at Daniel's request using the already discussed data-analysis theme and linked original sources.
- Checked: checked against the group assignment text supplied in chat for the listed problem/source/workflow/alternative/story/ownership fields. This is a document checklist, not an application test or peer review. AI source re-reading and actual presentation checks are separately recorded.
- Next: discuss with a teammate; agree or revise the reader/problem and sources; confirm distinct owners/reviewers; use this shared repository if agreed; independently verify sources; obtain actual peer feedback and record the response. Do not submit this as an agreed team result before that discussion.


#### Research-review index

- [Source checks and observations](https://github.com/dan38-cmyk/Group-Content-System/blob/main/SOURCE-REVIEW.md)
- [Actual presentation checks and limitations](https://github.com/dan38-cmyk/Group-Content-System/blob/main/CHECKS.md)
- [Contributions and AI assistance](https://github.com/dan38-cmyk/Group-Content-System/blob/main/LEARNING.md)
- [Peer feedback and decision record](https://github.com/dan38-cmyk/Group-Content-System/blob/main/PEER-REVIEW.md)
- [Canvas submission draft](https://github.com/dan38-cmyk/Group-Content-System/blob/main/SUBMISSION.md)

#### Current completion boundaries

Prepared by Daniel with AI assistance: this plan, architecture comparison, workflow, stories and research presentation. Pending: actual partner agreement, named second owner/reviewer, independent learner source verification, actual peer feedback and response. The five system stories are planned and have not run. No solo-work exception or instructor acceptance is claimed. If no partner responds, submit the actual current contribution and explicitly disclose the missing collaboration; ask the instructor how to handle the group requirement.
