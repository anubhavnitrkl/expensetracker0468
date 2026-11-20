# Expense Tracker (Firebase edition)

A single-page expense tracker for a household. Data is stored in your own free
Firebase project (Cloud Firestore) and shared between the Google accounts you
allow. Without signing in, it works on the device only.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole app. GitHub Pages serves it as the home page. |
| `firestore.rules` | Database rules. Only the listed Google accounts can read or write. |

## One-time setup

1. **Database rules.** Open `firestore.rules`, replace the two example Gmail
   addresses with yours and your partner's (lowercase), then paste the whole file into
   Firebase console → Firestore Database → Rules, and click **Publish**.
2. **GitHub Pages.** Create a public repo (for example `expense-tracker`), upload
   `index.html`, then go to Settings → Pages → Build and deployment →
   Source: *Deploy from a branch*, Branch: `main`, folder `/ (root)` → Save.
   After a minute or two the site is at `https://<your-username>.github.io/expense-tracker/`.
3. **Allow sign-in from that site.** Firebase console → Authentication → Settings →
   Authorized domains → Add domain → `<your-username>.github.io`.
4. **Move your data in.** In the old app, open Details → Backup → Download backup.
   In the new site, sign in, then Details → Backup → choose that file → Add to this app.

## How data is stored

- `households/family`: categories, payment modes, recurring bills.
- `households/family/months/YYYY-MM`: one document per month with that
  month's expenses in a map called `e`.

One document per month keeps Firestore reads low. Opening the app reads roughly
one document per month of history, not one per expense.

## Updating the app

Replace `index.html` in the repo. GitHub Pages republishes within a few minutes.
Data is not affected.
