# Workflow

## When a design milestone is finished
1. Design and Product decisions are finalised.
2. The Owner approves the milestone.
3. Update the milestone's `delivery-record.md` and the [decision log](docs/decisions/decision-log.md).
4. If a new product decision needs a PRD update, mark it `Required` and add it to the [PRD sync queue](docs/decisions/prd-sync-queue.md). Do not edit the PRD unless the Owner asks.
5. Update the [Figma node index](docs/figma/figma-node-index.md).
6. Then commit and push.

A milestone is **never** recorded as final or pushed as final before Owner approval. Work delivered but not yet approved lives in `milestones/delivered/`; after approval, `git mv` it to `milestones/design-complete/NN-name/`.

## Commits
- Semantic and short, for example:
  - `design: complete brand listing`
  - `docs: record supplier listing decisions`
  - `docs: sync prd with approved decisions`
  - `chore: update figma node index`
- One understandable commit per completed milestone.
- Optional tags for important milestones: `design/<milestone>-complete`.
- Never rewrite existing history (no force-push, no rebase of pushed commits).

## What belongs here
- Documentation, delivery records, decisions, Figma node references, history.

## What does not
- Figma exports, screenshots, duplicate images, generated files. Figma is the source of truth for design output.
