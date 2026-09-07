# Sanasto

A Finnish→English vocabulary trainer with no login, no backend and no build step. Two
study modes:

- **Flashcards** — flip through a set at your own pace.
- **Learn** — every term moves through three buckets: new → learning (answered
  correctly as multiple choice) → mastered (typed out correctly from memory). A term
  you get wrong is requeued two to four cards ahead, so it comes back while it is still
  fresh instead of at the end of the deck. The set is done when everything is mastered.

Progress is stored per device in `localStorage`, so anyone can open it, study, and add
their own sets without an account. The whole app is one HTML file plus a data file.

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

Add the set to `vocab.js` as a `{ id, name, description, cards: [{ fi, en, hint? }] }`
object and push. Vercel redeploys automatically.

## Format rules

- One pair per line, separator is `=` (with or without spaces).
- Optional hint after `|` (e.g. `juosta = run | verb`).
- Lines starting with `#` or `//` are comments and ignored.
- `Name:` is required. `Description:` is optional.
- Multiple English answers can be slash-separated and either is accepted in Learn mode: `tili = account / bank account`.

## Tech

- Pure static site: `index.html` + `vocab.js`. No framework, no bundler, no build step.
- Progress: `localStorage` per set id, key prefix `sanasto_v2_`.
- Custom sets: `localStorage` key `sanasto_custom_sets_v1`.
- Hosted free on Vercel (Hobby plan).
