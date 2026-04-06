# The Creative Resistance

A field guide to how authored work survives. Sixty-five practitioners across twenty disciplines, the same six decisions appearing over and over.

Live site: [authored-craft.vercel.app](https://authored-craft.vercel.app)

---

## What's in this repo

```
the-creative-resistance/
├── index.html              ← The site itself. CSS, markup, picker, constellation, all interactive layers.
├── profiles.js             ← Practitioner data and shared-pattern edges. The growable file.
├── STYLE.md                ← Voice and format conventions. Read before writing any new entry.
├── README.md               ← This file.
├── templates/
│   ├── 01_fact_sheet.md    ← Stage 1: gather and confirm sourced material.
│   ├── 02_profile_entry.md ← Stage 2: draft the entry in the house voice.
│   └── 03_edge_proposal.md ← Stage 3: propose constellation edges to existing practitioners.
└── archive/
    └── fact_sheets/        ← Permanent fact sheets for every published practitioner.
```

The site is two files at runtime: `index.html` loads `profiles.js` and renders. To deploy, push both. To send to someone offline, send both. (A bundler script can recombine them into one file on demand if needed — see "Bundling" below.)

---

## Adding a practitioner — the three-stage workflow

The site claims that all entries are built "from primary sources — podcasts, long-form interviews, profiles, their own words." Honoring that claim is the responsibility of every new entry. The three-stage workflow is how it gets honored.

**Stage 1 — Fact sheet.** Open `templates/01_fact_sheet.md`, copy it, and fill it in. Every claim about the practitioner that will eventually appear on the site has to be present here first, with a source attached. No Wikipedia, no AI summaries, no SEO content. Only primary sources.

**Stage 2 — Profile entry.** Once the fact sheet is complete, open `templates/02_profile_entry.md` and draft the entry in the house voice (defined in `STYLE.md`). Every sentence in the draft must trace back to a line in the fact sheet. The template includes a sourcing audit table — fill it in.

**Stage 3 — Edge proposal.** Once the profile is locked, open `templates/03_edge_proposal.md` and propose edges to existing practitioners. Read the existing tag vocabulary in `profiles.js` first. Most new practitioners will share existing tags — that's the point. Inventing new tags should be rare.

After all three stages: paste the new entry into `profiles.js` (alphabetical order), add the new edges to `webEdges`, save the fact sheet to `archive/fact_sheets/PRACTITIONERID.md`, run the integrity check (below), commit, push.

---

## Working with an LLM

A typical session for adding one practitioner looks like this:

1. **Open a new conversation** with whatever LLM you're using. Upload `STYLE.md`, `profiles.js`, and the three template files.
2. **Tell the LLM who you want to add**, and provide the source material — interview transcripts, links to long-form profiles, your own notes. The more raw material, the better the fact sheet.
3. **Ask it to do Stage 1.** It produces a fact sheet using the template. You read it, flag anything that looks off, ask for revisions until you trust every claim.
4. **Ask it to do Stage 2.** It writes the profile entry from the fact sheet, in the house voice. You read it. You check the sourcing audit. You revise.
5. **Ask it to do Stage 3.** It reads the new profile against the existing 65, proposes edges with tag-by-tag evidence, hands them back. You approve or reject each one.
6. **Get back the final paste-ready bundle:** the line for `profiles.js`, the new edge lines, and the fact sheet to save to `archive/fact_sheets/`.
7. **Paste, run integrity check, commit, push.**

Sessions can be split across days or even across LLMs. Each stage's output is a markdown document, so nothing is locked into one conversation.

---

## Integrity check

Before pushing any change, run a quick check that nothing is broken. Save this as a script (`check.py`) in the repo root or run it inline:

```python
import re

with open('index.html') as f:
    html = f.read()
with open('profiles.js') as f:
    profiles = f.read()

# Practitioners
keys = re.findall(r'^([a-z][a-z0-9_]*):\{n:"', profiles, re.MULTILINE)
print(f"Practitioners: {len(keys)}")

# Edges
edges = re.findall(r'^\["([a-z][a-z0-9_]*)", "([a-z][a-z0-9_]*)"', profiles, re.MULTILINE)
print(f"Edges: {len(edges)}")

# Modal targets in HTML
modal_targets = set(re.findall(r"openModal\('([^']+)'\)", html))
data_set = set(keys)
orphans_html = modal_targets - data_set
orphans_edges = set()
for a, b in edges:
    if a not in data_set: orphans_edges.add(a)
    if b not in data_set: orphans_edges.add(b)

print(f"HTML orphans (modal targets without data): {len(orphans_html)} {sorted(orphans_html)}")
print(f"Edge orphans (edge endpoints without data): {len(orphans_edges)} {sorted(orphans_edges)}")

# Syntax check
import subprocess
r = subprocess.run(['node', '--check', 'profiles.js'], capture_output=True, text=True)
print(f"profiles.js syntax: {'OK' if r.returncode == 0 else 'BROKEN: ' + r.stderr}")
```

Run with `python3 check.py`. If anything is non-zero except practitioner count and edge count, do not push.

---

## Bundling for offline / single-file delivery

If you want to send the site to someone as a single self-contained HTML file (e.g., for an offline demo), recombine the two files:

```bash
# Inline profiles.js into index.html
python3 -c "
with open('profiles.js') as f: profiles = f.read()
with open('index.html') as f: html = f.read()
bundled = html.replace('<script src=\"profiles.js\"></script>', '<script>' + profiles + '</script>')
with open('the_creative_resistance_bundled.html','w') as f: f.write(bundled)
print('Bundled to the_creative_resistance_bundled.html')
"
```

The bundled file is the same single-file format as the original. Use it for sending to people who won't be running a server. Don't commit it to the repo — `index.html` and `profiles.js` are the canonical source.

---

## Editorial principles (the short version)

These are also in `STYLE.md` but worth surfacing here.

1. **Primary sources only.** If a claim can't be traced to the practitioner's own words or a long-form profile, it doesn't go in.
2. **Voice is consistent across all entries.** Present tense, short sentences, no hedging, no business-school nouns, specific over general, the reader is already in the fight.
3. **Variety in section headings is intentional.** No fixed schema. Each profile has 4–6 sections whose headings match the shape of that specific practice.
4. **Edges are not casual.** Every shared tag has to be backed by evidence in both profiles. The constellation is the project's most powerful idea and the easiest one to fake.
5. **Fact sheets are kept forever.** They're the audit trail. They live in `archive/fact_sheets/` and can be revisited when revising or defending an entry.

---

## What's deliberately not in the workflow

A few things that look like good ideas and have been considered and rejected:

- **A fixed six-part profile schema.** Considered, rejected. The site's reader experience depends on discovering patterns across people, not on every page being predictable. Variable headings preserve the discovery.
- **Tags as free-form keywords.** Rejected. Tags are a controlled vocabulary precisely so the same moves recurring across distant practices is a real claim, not a labeling artifact.
- **AI-generated material in fact sheets.** Rejected. Fact sheets are sourced. An LLM can help draft the entry from a fact sheet, but the fact sheet itself contains only what a primary source says.
- **One file per practitioner.** Considered. For now, all practitioners live in `profiles.js` together. The day there are 200+ practitioners and the file becomes unwieldy, splitting into individual files becomes attractive — but not until then.

---

## Credits

Built by Ed Cotton — Inverness Consulting. 2025–2026.
