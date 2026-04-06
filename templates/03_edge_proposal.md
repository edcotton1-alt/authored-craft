# Edge Proposal — [PRACTITIONER NAME]

**Stage 3 of the three-stage workflow.** The profile entry is drafted (stage 2). Now the new practitioner is connected to existing practitioners through `webEdges` — the array at the bottom of `profiles.js` that powers the Shared DNA constellation and the pair picker.

**Edges are the most powerful idea in the project and the easiest one to fake. Take this stage seriously.**

---

## How edges work

Each edge in `webEdges` looks like:

```javascript
["new_practitioner_id", "existing_practitioner_id", weight, ["Tag One", "Tag Two", "Tag Three"]]
```

- `weight` is the number of shared tags. It must be at least 3 — pairs sharing only one or two tags don't get an edge.
- The tags are a controlled vocabulary. Do not invent freely. Read existing edges in `profiles.js` to see the active vocabulary before proposing new ones.
- Both practitioners must have evidence in their profile (and ideally their fact sheet) for every tag listed. If you can't point to the line in each profile that justifies the tag, the edge does not exist.

---

## Existing tag vocabulary (read this before proposing)

Open `profiles.js`, find the `webEdges` array, and skim the tags. There are roughly 60 active tags. Examples include:

- Family / formative: "The father", "She shaped everything", "Born in a war zone", "The wound became the method"
- Materials and tools: "No computer", "One material", "The wrong tool", "Paint", "Drums"
- Time and patience: "The 1,000-day commitment", "8 hours for 1", "One place forever", "Punk to patience"
- Refusal: "Closed it down", "No website", "Restriction as freedom", "Silence as strategy", "Gave up the bigger thing"
- Outsiderness: "The immigrant eye", "Built the world that rejected them", "Left for freedom", "Ran away", "Not discovered until..."
- Structure: "The architect and the baker", "The teacher", "Only works with friends", "The audience completes the work"

Most new practitioners will share several existing tags. That's the point — the project is interesting *because* the same moves keep recurring. A new practitioner that introduces five brand-new tags is suspicious — usually it means the writer was reaching for novelty instead of finding the actual rhymes.

**You can introduce a new tag, but only if a genuinely new structural move appears that no existing tag captures.** Adding a new tag means: write it in the proposal below, explain why no existing tag works, and note that all future edges to other practitioners using this tag will need to be considered.

---

## Candidate edges

Go through the existing 65 practitioners (or filter by likely matches first — same discipline, similar origins, similar refusals) and identify which ones share three or more structural moves with the new practitioner.

For each candidate, fill in this block:

### Candidate 1: [existing_practitioner_id]

**Their name:** [Display name]
**Their discipline:** [Discipline]
**Why they might rhyme:** [One sentence — what's the structural overlap that made you consider them]

**Proposed shared tags:**

| Tag | Evidence in [new practitioner] | Evidence in [existing practitioner] |
|---|---|---|
| [Tag from existing vocabulary] | [Specific line/claim from new fact sheet] | [Specific line from existing profile] |
| [Tag] | [Evidence] | [Evidence] |
| [Tag] | [Evidence] | [Evidence] |

**Weight:** [number of tags above — must be 3 or more]

**Edge as it will appear in `webEdges`:**

```javascript
["new_id", "existing_id", N, ["Tag One", "Tag Two", "Tag Three"]],
```

**Decision:** [propose / reject / hold for review]

---

### Candidate 2: [existing_practitioner_id]

[Same structure as above.]

---

### Candidate 3: [existing_practitioner_id]

[Continue for as many candidates as warrant a real edge. A new practitioner typically gets 2–6 edges. More than 10 is unusual and should be a flag — it might mean tags are being applied loosely.]

---

## New tags introduced (if any)

If you propose a tag that doesn't exist in the current vocabulary, list it here with justification.

| New tag | Why no existing tag works | First two practitioners it applies to |
|---|---|---|
| [New tag] | [Justification] | [practitioner_a, practitioner_b] |

If this section is empty, that's a good sign. Most rounds should not introduce new tags.

---

## Final edges to add to `webEdges`

After review and approval, paste the final edge lines here, ready to drop into `profiles.js`:

```javascript
["new_id", "existing_id_1", 4, ["Tag", "Tag", "Tag", "Tag"]],
["new_id", "existing_id_2", 3, ["Tag", "Tag", "Tag"]],
["new_id", "existing_id_3", 5, ["Tag", "Tag", "Tag", "Tag", "Tag"]],
```

These get pasted into the `webEdges` array near the bottom of `profiles.js`. The order doesn't matter to the rendering, but keeping new edges grouped near the bottom of the array makes it easy to see what was added in this round.

---

## Integrity check after adding

After pasting the new edges and the new practitioner entry, run the integrity check from `README.md`. The script should report:

- Practitioner count went up by exactly one
- All edge endpoints reference real practitioner IDs (no orphan edges)
- All new tags either exist in the vocabulary or are listed in the "New tags introduced" section above
- The file still parses

If any check fails, do not push.
