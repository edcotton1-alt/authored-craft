# STYLE.md — How to write a profile entry

This file describes the voice, format, and conventions for every practitioner profile in The Creative Resistance. The site claims that all 65 profiles are built "from primary sources — podcasts, long-form interviews, profiles, their own words." Honoring that claim is the responsibility of every entry. So is sounding like the same project as the 64 that came before.

If you're an LLM helping to write a new entry, read this file first. If you're a human, read it before drafting and again before publishing.

---

## The voice

**Present tense.** Even for things that happened decades ago. "He moves to New York at 18." Not "He moved." The site is a field guide to ongoing practices, not a museum of completed lives.

**Short sentences. Then longer ones. Then short again.** The rhythm matters more than any individual sentence. Read existing entries (Lemaire, Kéré, Abramović, Tyler, Robertson) out loud and you'll hear it.

**No hedging.** "He often" / "she sometimes" / "they tend to" all weaken the claim. If a thing is true, write it as true. If it isn't reliably true, cut it.

**No business-school nouns.** Avoid: ecosystem, framework, methodology, leverage, scale (as a verb), stakeholder, value-add, narrative arc. The site is allergic to consultancy English. The voice is closer to a long magazine profile than a case study.

**Quotes inside prose, not blockquoted.** Direct quotes from primary sources go inside the running prose, in double quotes, integrated into the sentence rhythm. They are not pulled out and visually separated. The exception is the closing pull-quote (see below).

**One quote per sentence, max.** Don't string together three quotes from a transcript and call it a paragraph. If you find yourself doing that, paraphrase two of them.

**The reader is already in the fight.** Assume they make things, that they feel the pressure of speed and scale, that they don't need the basic concepts explained. Don't define "authored work." Don't explain what a creative director is. Trust them.

**Specific over general. Always.** Not "the artist's challenging upbringing" but "her father survived the Igman March — minus twenty-five degrees, two hundred survivors, one night." Not "a perfectionist approach to materials" but "weeks on the twist of a yarn, months on a shade of red, years on a texture for a pair of jeans." The site lives on the small concrete details. Generalities kill it instantly.

---

## The structure of an entry

Every profile is one JavaScript object inside `profiles.js`, on one line, in this exact format:

```javascript
practitionerid:{n:"Display Name",d:"Discipline · Subdiscipline",body:'HTML STRING'},
```

The `body` field is an HTML string containing 4–6 sections. Each section is:

```html
<div class="modal-section">
  <div class="modal-section-label">SECTION HEADING</div>
  <p>The prose for this section.</p>
</div>
```

Followed at the very end by a single closing pull-quote:

```html
<div class="modal-quote">"The pull quote, attributed to the practitioner, in their own words."</div>
```

**Section headings vary by profile.** This is intentional. The site does NOT use a fixed schema like "Background / Method / Influences." Instead, each profile has 4–6 sections whose headings are chosen to match the shape of that specific person's practice. Common heading patterns you'll find in existing entries:

- **What makes him/her/them unique** (almost universal — the opening framing)
- **Origins** (childhood, family, formative event)
- **The method** / **How he makes it** / **The practice**
- **What he protects** / **The refusal**
- **Partnership** (when collaboration is structural)
- **The private life** / **The body knows** (when ritual or daily life matters)
- **The cost** / **What it took**

But also section headings unique to one profile only — "Patterns" (Collins), "Quartz crisis" (Collins), "The mirror" (Cecily Brown), "Alien 3 — the crucial error" (Fincher). When a practitioner has a defining episode or idea that doesn't fit the common headings, give it its own section with its own name.

**The grammar is loose on purpose.** A site reviewer once suggested locking every profile into a fixed six-part schema. We considered it and decided against. Reason: the variety in headings is what keeps the profiles from feeling like a database. The reader discovers the pattern across people, not inside any single page.

---

## Length

Average profile is about 4 KB of HTML, which translates to roughly 350–500 words of prose across 4–6 sections. The longest profiles (Saunders, Prince, Kojima) approach 700 words; the shortest (Papaioannou, The Row, Field) are closer to 200. Both extremes work as long as every sentence earns its place.

**Don't pad to length.** A 250-word entry with five real moves beats a 600-word entry that recycles biographical filler.

**Don't truncate to fit a target.** If a practitioner has six things worth saying, say six things. The constraint is "earned, sourced, in voice" — not "between 350 and 500 words."

---

## Sourcing (this is the part that matters most)

Every claim in a profile must trace back to a primary source. A **primary source** is one of:

1. **The practitioner's own words.** Direct quote from an interview, podcast, talk, essay, social post, or any place they chose to speak publicly.
2. **A long-form profile of them in a publication that did its own reporting.** (The New Yorker, FT Weekend, Monocle, 032c, Apartamento, similar.) Not a Wikipedia summary, not a SEO listicle, not a blog post that's recycling other coverage.
3. **A book they wrote, or a book about them with primary research.**

**What does NOT count as a primary source:**

- Wikipedia. (Useful for a starting point. Never a citation.)
- AI-generated summaries. (Including ones you wrote yourself this morning by asking an LLM for "key facts about X.")
- Press releases.
- Brand About pages written in third person.
- Anything you can't link to or name.

**Before writing the entry, build the fact sheet.** See `templates/01_fact_sheet.md`. Every claim in the fact sheet has a source attached. The profile entry is then written *from the fact sheet*, not from raw memory. If you find yourself wanting to write a sentence that doesn't have a source in the fact sheet, you have two options: find the source, or cut the sentence. There is no third option.

**Keep the fact sheet.** After the profile is published, the fact sheet for that practitioner lives at `archive/fact_sheets/practitionerid.md`. It is the audit trail. If a reader asks "where does this come from?" or if you want to revise the profile a year later, the fact sheet is what you go back to.

---

## The closing pull-quote

Every profile ends with one direct quote from the practitioner, in `<div class="modal-quote">"..."</div>`. This is the only place a quote gets visually pulled out.

**The pull-quote should be the line that, if you only read one sentence about this person, would tell you the most.** Not the most quotable. Not the most poetic. The most *load-bearing*. Lemaire's "Who designed the first trench coat?" works because the whole profile is about reverence for anonymous makers and that question is the entire stance distilled. Kojima's "I want to die while creating something" works because the profile is about a man whose loneliness is also his subject and he is naming that on the way out.

**One quote. Not a stitched-together composite. Not your paraphrase. Their words exactly, from a real source.**

---

## The constellation tags

When a new practitioner is added, they need to be linked to existing practitioners through `webEdges` — the array at the bottom of `profiles.js` that powers the Shared DNA constellation and the pair picker.

Every edge looks like:

```javascript
["practitioner_a", "practitioner_b", weight, ["Tag One", "Tag Two", "Tag Three"]]
```

Where `weight` is the number of shared tags (always equal to the length of the tag array — 3 minimum to count).

**Tags are NOT free-form keywords.** They are a controlled vocabulary of shared structural moves that already exist in the project. You can see the existing tags by reading the existing edges. Examples: "The father", "Born in a war zone", "The wound became the method", "No computer", "The 1,000-day commitment", "Built the world that rejected them", "Punk to patience", "The architect and the baker", "Closed it down".

**You can introduce a new tag if a genuinely new structural move appears.** But the bar is high. Most new practitioners will share existing tags. Inventing tags freely defeats the whole point of the constellation — which is to surface that the same moves recur, not to label every practitioner with bespoke vocabulary.

**See `templates/03_edge_proposal.md` for the full process.** Edges are not added casually. Every proposed edge has to be backed by evidence in both practitioners' fact sheets. If you can't point to the line in each profile that justifies the tag, the edge doesn't exist.

---

## What to avoid

A short list of things that will get cut from any draft:

- **"In conclusion" / "ultimately" / "what makes X unique is..."** as the opening of the closing thought. Trust the reader to draw the conclusion.
- **Adjectives doing the work of evidence.** "His brilliant approach to materials" — what does brilliant mean? What's the evidence? Replace with the evidence.
- **Three-quote chains.** "She has said 'X.' She has also said 'Y.' And in a recent interview she said 'Z.'" Pick one, paraphrase the others if you need them.
- **Career chronology as structure.** The profile is not "born → studied → first job → big break → today." If chronology serves the point, use it. If it doesn't, don't.
- **Name-checking famous collaborators to borrow shine.** "Worked with Karl Lagerfeld and Anna Wintour." Either there's a real story there or there isn't.
- **The site's own thesis sentences.** Don't write "this is what creative resistance looks like" inside an entry. The chapter framing carries that. Inside an entry, just show the work.

---

## When in doubt

Read three existing entries from the same discipline as the practitioner you're adding, out loud, before drafting. The voice will calibrate itself. The site is consistent enough that one reading session is usually all it takes.

The goal is never "match the template." The goal is always "this person belongs in this room with the others."
