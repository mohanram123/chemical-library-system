# Chemical Library System

A responsive, government-style chemical inventory and borrowing page hosted with GitHub Pages.

## Demo login

The first version runs in browser demo mode until Firebase is configured:

- **Username:** `admin`
- **Password:** `chemical123`

The password is intentionally hard-coded. It provides only a UI-level restriction and is not secure for public hosting. Firebase Authentication is strongly recommended before production use.

## Firebase setup

1. Open Firebase Console and create a project.
2. Enable **Firestore Database** in production or test mode.
3. Register a Web app and copy its Firebase configuration.
4. In `index.html`, replace the empty `firebaseConfig` values.
5. Change `const DEMO=true` to `const DEMO=false`.
6. Deploy the updated files to GitHub Pages.

### Firestore collections

- `personnel` — IC number, name, section and designation
- `chemicals` — name, formula, purchased date and quantity
- `borrowingRecords` — borrower, chemical, borrowed quantity and date; `active` indicates whether it remains outstanding
- `returnRecords` — borrower, chemical, returned quantity and date

### Suggested Firestore security rules

Public demo borrowing and return operations do not include secure Firebase Authentication. For production, use Firebase Authentication and restrict writes to authorized users:

```text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

This rule is a starting point; restrict each collection to an appropriate role before production use.

## GitHub Pages

The public site is published from the `gh-pages` branch:

- https://mohanram123.github.io/chemical-library-system/

After changing files on `master`, copy `index.html` and commit it to `gh-pages`, then push that branch.
