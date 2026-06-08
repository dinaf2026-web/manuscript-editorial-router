---
name: manuscript-editorial-router
description: >
  Routes a broad or ambiguous editorial request to the right pass(es) in the
  Manuscript Editorial Suite. Use when the ask spans more than one kind of feedback
  or it's unclear which is wanted — "review my book", "give me editorial feedback",
  "is this ready", "go over this chapter", "full editorial pass", "what should I
  check". Picks among manuscript-publisher-critique, manuscript-continuity-audit,
  manuscript-fair-play-audit, manuscript-cinematic-scene-audit, manuscript-prose-
  immersion-audit, and manuscript-listing-critique, runs them in the right order for
  the book's genre, and hands off. Does not itself critique, score, or rewrite — it
  only dispatches.
---

# Manuscript Editorial Router

Decide which critique pass(es) the request needs, then run them. Do not produce a
critique yourself — your output is a routing decision plus the dispatched skill(s).
If the request already clearly names one pass, skip the routing prose and run it.

## STEP 0 — Resolve the project profile

From the current working directory, walk **up** the parent folders for
`.manuscript/profile.md`.
- **Found** → read it. Its `genre` and `passes` decide which passes are even
  applicable (e.g. `fair-play` only for mystery/crime/thriller).
- **Not found** → invoke `manuscript-profile-setup` to create one, then continue.
  If the author declines, route with genre-general defaults and say so.

## The six passes

| Pass | Skill | Use when the ask is about… |
|------|-------|-----------------------------|
| Craft & acquisitions | `manuscript-publisher-critique` | whole-story quality, "is it good / would a publisher take this", scoring, an editor's letter |
| Continuity / canon | `manuscript-continuity-audit` | contradictions of the book's bible, drifted details, internal inconsistency |
| Mystery logic | `manuscript-fair-play-audit` | clue fairness, plant→payoff, "does the solution hold up" (mystery/thriller only) |
| Cinematic / blocking | `manuscript-cinematic-scene-audit` | spatial logic, scene population, who's in the room, movement tracking, blocking continuity, environment on camera, emotional register, internal voiceover; "cinematic pass", "movie screen audit", "read this like a director", "where is everyone", "did we forget anyone", "blocking pass" |
| Line craft | `manuscript-prose-immersion-audit` | line-level immersion (diagnosis only): "line audit", "is this immersive", "talking heads", info-dumping, filter words |
| Sales surface | `manuscript-listing-critique` | blurb / back-cover / Amazon description / categories / keywords |

**Supporting (not a critique pass):** `manuscript-canon-ledger` — the living,
versioned canon store the continuity pass reads before auditing. Route directly to
it for ledger *maintenance*: "update the ledger", "record a canon change", "is this
canon", "resolve open question", "seed the ledger from book N".

## Routing rules

1. **Disambiguate overlapping phrases by object, not verb:**
   - "would this sell" + a *manuscript/chapter* → `manuscript-publisher-critique`;
     + a *blurb/description/listing* → `manuscript-listing-critique`.
   - "check the plot logic / does it hold up" about *clues and the solution* →
     `manuscript-fair-play-audit`; about *overall craft* → publisher-critique.
   - "did I get the details right / does this break canon" → continuity-audit.
   - "line audit / is this immersive / kill the info-dumping" → prose-immersion-audit
     (line-level), vs. a macro "is the voice working overall" → publisher-critique's
     Voice row. A request to *rewrite* prose is neither — route it to the author's
     writing/voice skill.
   - "cinematic pass / movie screen audit / blocking / where is everyone / did we
     account for everyone / read this like a director / would I see this on screen"
     → `manuscript-cinematic-scene-audit`. **Key distinction from prose-immersion:**
     prose-immersion asks "is the writing alive?"; cinematic asks "does the scene
     make spatial, physical, and emotional sense if you filmed it?" They run together
     on the same material without overlap.
2. **Manuscript vs. listing is the first fork.** Selling copy or metadata →
   `manuscript-listing-critique` and nothing else. Story content (scene, chapter,
   outline, manuscript, query) → one of the other five.
3. **Gate by genre.** Only run `manuscript-fair-play-audit` if the profile's genre
   is a mystery/crime/thriller (or `fair-play` is in `passes`). For a memoir,
   literary novel, or romance with no puzzle, skip it and say why.
4. **Order when multiple passes apply** (run sequentially, report each separately):
   1. `manuscript-continuity-audit` — catch canon/consistency breaks first; they
      cap the craft grade.
   2. `manuscript-fair-play-audit` — if there's a mystery to judge.
   3. `manuscript-cinematic-scene-audit` — spatial/blocking audit; surface
      structural scene problems before going to line level.
   4. `manuscript-prose-immersion-audit` — the line-level craft pass on the scenes.
   5. `manuscript-publisher-critique` — the macro craft/acquisitions read, last, so
      it can reference the prior findings.
   `manuscript-listing-critique` is independent — run it only for listing material.
5. **Broad asks default to a full pass.** "Review my book / is this ready / full
   editorial pass" on a manuscript → continuity → (fair-play if applicable) →
   cinematic → prose-immersion → publisher, in that order. For a long manuscript,
   cinematic and prose-immersion can sample representative scenes — say which.
6. **Only one obvious pass?** Skip the routing explanation and invoke it directly.
7. **Genuinely ambiguous and consequential?** Ask one short clarifying question
   (e.g. "craft read, canon check, mystery-logic check, cinematic/blocking pass,
   line audit, or listing copy?") rather than guessing.

## Running a selected pass

After selecting the pass(es), for each one **load that skill's `SKILL.md` and its
referenced files, then follow that skill's required output exactly.** Do not produce
a critique from the router body alone or paraphrase a pass's format — the value is in
each skill's own report structure. Run the passes in the order decided above and
present each skill's output as its own clearly-labeled section.

## Output

Lead with a one-line routing decision — which pass(es), in what order, and why — then
load and run them. Example: "This spans continuity and craft → running
continuity-audit first, then publisher-critique." Keep the routing note to one or two
sentences; the value is in the passes, not the dispatch.
