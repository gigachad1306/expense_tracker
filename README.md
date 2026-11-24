# Trip split

A single-page expense splitter: log expenses, split them equally, by shares or by exact amounts,
record repayments, and see who pays whom. No build step. The whole app is `index.html`.

## 1. Put it on GitHub Pages (2 minutes)

1. Create a new GitHub repository and upload `index.html` (and this README if you like).
2. Repository **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*,
   Branch = `main`, folder = `/ (root)`. Save.
3. After a minute your app is live at `https://<your-username>.github.io/<repo-name>/`.

That's enough to use it. It starts in **browser mode**.

## 2. Two ways to store data

| | Browser mode (default) | Cloud mode (Firebase) |
|---|---|---|
| Setup | none | about 5 minutes, free |
| Where data lives | the browser that created the account | your own Firebase database |
| Sign-in | username + password, checked in the browser | real email + password accounts |
| Same data on phone and laptop | no (use Export / Import backup) | yes |
| Whole group sees the same numbers | only on one shared device | yes, share one login |

**Be aware of browser mode:** the password only locks the app on that device. Anyone with access to the
browser's storage can read the data. Clearing site data deletes it, so use *Export backup* now and then.

## 3. Turn on cloud mode (free Firebase plan)

1. Go to <https://console.firebase.google.com> → **Add project** (turn Analytics off).
2. **Build → Authentication → Get started → Email/Password → Enable.**
3. **Build → Firestore Database → Create database** (production mode, any region).
4. Firestore **Rules** tab: paste the contents of `firestore.rules` and **Publish**.
   This makes each account able to read and write only its own data.
5. **Project settings (gear) → Your apps → Web (`</>`)** → register an app. Copy the `firebaseConfig` values.
6. In `index.html`, find the `CONFIG` block near the top of the script and replace `firebase: null` with:

   ```js
   firebase: { apiKey: "…", authDomain: "…", projectId: "…", appId: "…" }
   ```
7. **Authentication → Settings → Authorized domains → Add domain:** `<your-username>.github.io`.
8. Commit the change. Create your account on the live page and share the login with your group.

The Firebase `apiKey` is not a secret; it only identifies your project. Access is controlled by the
rules in step 4. Do not skip that step.

## Using it

- **Overview:** totals, the fewest transfers that settle everyone (*Mark as paid* records it), balance per person, spending by category.
- **Expenses:** add, edit, delete, search, filter. Splits: equal (tick who shared it), shares (2 : 1 : 1), exact amounts.
- **Payments:** every repayment. Balances update immediately.
- **People and data:** add or rename people, edit categories, export JSON / CSV, import a backup, delete everything.

Don't remove a person who appears in expenses or payments; the app blocks it. Rename instead.
