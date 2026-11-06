# KaiHSK Google sign-in setup

The site uses Firebase Authentication to create or sign in to a KaiHSK account
with Google. Firebase manages the OAuth flow and keeps the signed-in session in
the browser.

## Publish on GitHub Pages

The `Deploy KaiHSK to GitHub Pages` workflow publishes `index.html` and
`firebase-config.js` whenever code is pushed to `main`. Once the workflow
finishes successfully, open
[`https://khaiforces.github.io/kai-hsk/`](https://khaiforces.github.io/kai-hsk/).
You can also run the workflow manually from the repository's **Actions** tab.

## Configure Firebase

1. Create a Firebase project at [Firebase Console](https://console.firebase.google.com/).
2. In **Authentication → Sign-in method**, enable **Google** and select a
   support email.
3. In **Project settings → General**, register a Web app and copy its
   `apiKey`, `authDomain`, `projectId`, and `appId` into `firebase-config.js`.
   Firebase web configuration is public client configuration; do not put a
   service-account key or OAuth client secret in this file.
4. In **Authentication → Settings → Authorized domains**, add every hostname
   used to serve the site. For local testing, add `localhost`.
5. Serve the folder over HTTP instead of opening `index.html` directly, for
   example:

   ```powershell
   python -m http.server 8000
   ```

   Then open `http://localhost:8000`. Add your production hostname to Firebase
   Authorized domains before deployment. Google sign-in popups do not work
   reliably from a `file://` URL.

Firebase Authentication creates an account automatically the first time a
person continues with Google and signs them in on subsequent visits. This
static prototype does not yet save learning progress to a database; add a
backend or Firebase database with appropriate security rules before storing
user-specific learning data.
