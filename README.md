# Sanasto

A simple, public, no-login Finnish→English vocabulary trainer (Flashcards + Learn mode). Progress is saved per device in `localStorage`. Anyone can visit, study, and add their own sets.

## How to add a new vocab set

### Option A — In the browser (private to your device)

1. Click **+ Lisää sanasto** on the home page.
2. Paste your set using this format:

```
Name: My set name
Description: short summary (optional)

# Comments and section headings start with #
fi term = en translation
toinen sana = another word | optional hint
kissa = cat
juosta = run | verb
```

3. Click **Tallenna sanasto**. The set appears immediately on home and is saved in your browser only.

### Option B — Share with everyone (committed to the repo)

If you want a set to appear for every visitor, ask Claude to add it to `vocab.js` in this repo. Vercel auto-deploys the change.

**Prompt to give Claude** along with your raw vocab:

> Add this vocabulary as a new set in `vocab.js`. Use `{ fi, en, hint? }` shape, give it a sensible `id`, `name`, and `description`. Then commit and push so Vercel redeploys.

## Format rules

- One pair per line, separator is `=` (with or without spaces).
- Optional hint after `|` (e.g. `juosta = run | verb`).
- Lines starting with `#` or `//` are comments and ignored.
- `Name:` is required. `Description:` is optional.
- Multiple English answers can be slash-separated and either is accepted in Learn mode: `tili = account / bank account`.

## Tech

- Pure static site: `index.html` + `vocab.js`. No build step.
- Progress: `localStorage` per set id, key prefix `sanasto_v2_`.
- Custom sets: `localStorage` key `sanasto_custom_sets_v1`.
- Hosted free on Vercel (Hobby plan).
