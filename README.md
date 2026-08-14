[README.md](https://github.com/user-attachments/files/31050684/README.md)
# Orchard Bites — F&B Directory

A single-page, static F&B directory covering the malls near Concorde Hotel Singapore
between Dhoby Ghaut and Somerset: Plaza Singapura, Concorde Shopping Mall,
313@Somerset, Orchard Gateway, and Orchard Central — including the area's
bubble tea and kopitiam scene (CHAGEE, Molly Tea, KOI Thé, Chicha San Chen,
Toast Box, Killiney Kopitiam, Ya Kun, Gong Cha).

Pure HTML/CSS/JS — no build step, no dependencies, no backend. This makes it a
zero-config static deploy on Vercel.

## Project structure

```
orchard-bites/
├── index.html      ← the whole app (markup, styles, data, filtering logic)
├── vercel.json      ← tells Vercel this is a static site, no build command
├── package.json     ← optional metadata, lets Vercel/npm tooling recognize the project
└── README.md         ← this file
```

## Deploy: GitHub → Vercel

### 1. Push this folder to a new GitHub repo

```bash
cd orchard-bites
git init
git add .
git commit -m "Initial commit: Orchard Bites F&B directory"
git branch -M main
git remote add origin https://github.com/<your-username>/orchard-bites.git
git push -u origin main
```

(Create the empty repo on GitHub first at github.com/new — don't initialize it
with a README there, since this folder already has one.)

### 2. Import into Vercel

1. Go to [vercel.com/new](https://vercel.com/new)
2. Click **Import Git Repository** and select the `orchard-bites` repo
3. Vercel will auto-detect it as a static site (Framework Preset: **Other**)
   - Build Command: leave blank / "None"
   - Output Directory: `.` (already set in `vercel.json`)
4. Click **Deploy**

Your site will be live at `https://orchard-bites-<random>.vercel.app` within
about 30 seconds. You can rename the project or attach a custom domain from
the Vercel project settings afterward.

### 3. Future updates

Any push to `main` auto-redeploys:

```bash
git add .
git commit -m "Update outlet data"
git push
```

## Editing the data

All outlet data lives in the `DATA` array near the bottom of `index.html`
(search for `const DATA = [`). Each entry looks like:

```js
{
  mall: "Plaza Singapura",
  addr: "68 Orchard Road, S238839 · linked to Dhoby Ghaut MRT",
  name: "Nando's",
  unit: "Level 2 (unit TBC)",
  cuisine: "Western",
  type: "Restaurant",
  halal: true,
  veg: false,
  phone: "",
  reserveNote: "Walk-in / large groups call ahead",
  website: "https://www.nandos.com.sg",
  online: "Nando's App / GrabFood"
}
```

`veg: true` marks outlets with a solid vegetarian menu or clearly veg-friendly
format (Indian restaurants, food courts, bakeries/cafes, hot pot with veggie
broths, etc.) — it does not mean 100% vegetarian, just that a vegetarian diner
has real options there.

Add, remove, or edit entries directly — the search bar, halal toggle, and
cuisine/type filters all rebuild automatically from whatever is in `DATA`.

## Known limitations (read before going live)

Mall tenants rotate frequently, and not every outlet publishes a public unit
number, phone line, or reservation link. Entries marked `"unit TBC"` or with
`reserveNote: "Walk-in only"` are placeholders based on the best public
information available at time of writing — verify against each mall's live
store directory (CapitaLand for Plaza Singapura, 313somerset.com.sg,
orchardgateway.com.sg) before treating this as authoritative. The same caution
applies to the `halal` and `veg` flags — both were set from public menu/brand
info, not a live certification feed, so double-check with the outlet directly
for dietary-critical visits. Outlets with `type: "Beverages"` (bubble tea,
kopitiam coffee, milk tea) power the "Beverages only" toggle at the top of
the page — add `type: "Beverages"` to any new drink stall you add and it'll
pick it up automatically.
