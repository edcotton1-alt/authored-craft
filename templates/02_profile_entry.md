# Profile Entry — [PRACTITIONER NAME]

**Stage 2 of the three-stage workflow.** The fact sheet (stage 1) is complete. Now the entry is drafted in the house voice.

Read `STYLE.md` before drafting. Every claim in this draft must trace back to a line in the fact sheet — if you find yourself wanting to write a sentence that isn't sourced, either find the source or cut the sentence.

---

## Working draft (in prose, with section headings)

Draft the profile here first as plain markdown — easier to read, easier to edit, easier for a human to check. The conversion to the JavaScript object format happens at the bottom of this file, after the prose is locked.

### What makes [him/her/them] unique

[Opening section. Almost universal — every profile has something like this. 2–4 sentences that establish who this person is and what makes them belong in this room. Specific. No "renowned for" or "celebrated as." Just the facts that distinguish them.]

### [Section 2 heading — varies by practitioner]

[Choose the heading that fits this person's shape. Common ones: "Origins", "The method", "How [he/she/they] makes it", "What [he/she/they] protects", "The refusal", "Partnership", "The private life", "The body knows", "The practice".]

[Prose. Present tense. Short sentences. One quote per sentence max. Specific, sourced details only.]

### [Section 3 heading]

[Continue. 4–6 sections total. The sections do not have to be in any fixed order. They should follow the logic of this specific person's practice.]

### [Section 4 heading]

[...]

### [Optional sections 5 and 6]

[Add only if there's enough sourced material to fill them with substance, not padding.]

### Closing pull-quote

> "[The single most load-bearing line this person has ever said. From the fact sheet's "Direct quotes" section. Their exact words. One quote, not a stitch.]"

---

## Length check

- Total word count: [____]
- Section count: [____]
- Number of direct quotes from primary sources: [____]
- Pull-quote source: [Which source from the fact sheet]

Target is 350–500 words across 4–6 sections. Going outside that range is fine if every sentence earns its place. Flag it here so you've made the choice consciously.

---

## Sourcing audit

Walk through the draft sentence by sentence. For each substantive claim, note the fact sheet line it came from. This is tedious. It is also the only way to honor the site's promise that everything is from primary sources.

| Sentence (first few words…) | Fact sheet source |
|---|---|
| "Born in 1976, Belgrade…" | Fact sheet, Origins, Source 1 |
| "Her father survived the Igman March…" | Fact sheet, Origins, Source 2, "minus twenty-five degrees" |
| ... | ... |

If any row in this table is blank, that sentence cannot ship. Cut it or source it.

---

## Conversion to `profiles.js` format

Once the prose is locked and the audit is complete, convert to the single-line JavaScript object format used in `profiles.js`. The format is:

```javascript
practitionerid:{n:"Display Name",d:"Discipline",body:'<div class="modal-section"><div class="modal-section-label">SECTION 1 HEADING</div><p>Section 1 prose.</p></div><div class="modal-section"><div class="modal-section-label">SECTION 2 HEADING</div><p>Section 2 prose.</p></div><div class="modal-quote">"Pull quote."</div>'},
```

**Critical escaping rules** (the body is a single-quoted JavaScript string, so):

- Apostrophes in the prose must be escaped as `\'`. "doesn't" becomes `doesn\'t`.
- Double quotes inside the prose stay as `"` — they don't need escaping because the string is wrapped in single quotes.
- Newlines inside the body string are NOT used. The whole body is one continuous line of HTML.
- The HTML tags (`<div>`, `<p>`, `</p>`, `</div>`) use double quotes for attributes, which is fine.

**Paste the final converted line below, ready to drop into `profiles.js`:**

```javascript
[paste here]
```

---

## Where this entry slots into `profiles.js`

Open `profiles.js`. The data block is in roughly alphabetical order by practitioner ID. Find the right slot and paste the converted line, with a comma at the end.

After pasting, run the integrity check (see `README.md`) to confirm the file still parses and the practitioner count went up by one.
