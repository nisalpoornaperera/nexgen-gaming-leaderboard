# Firebase setup

GitHub Pages remains the free website host. Firebase Firestore is the shared, free data store for the leaderboard.

## One-time Firebase console setup

1. Create a Firebase project on the Spark (free) plan at https://console.firebase.google.com/.
2. Add a Web app and copy its configuration object from **Project settings** > **Your apps**.
3. In **Authentication** > **Sign-in method**, enable **Anonymous** and **Email/Password**.
4. In **Authentication** > **Users**, add the tournament operator's email/password account. Copy its UID.
5. In **Authentication** > **Settings** > **Authorized domains**, add `nisalpoornaperera.github.io`.
6. Create a Cloud Firestore database in Production mode. Choose a nearby region; the default is suitable for a two-day event.

## Configure this repository

1. Confirm the Firebase web configuration and operator UID in [firebase-config.js](firebase-config.js) match the Firebase project.
2. Confirm the operator UID in [firestore.rules](firestore.rules) matches the operator account.
3. From this repository, deploy the Firestore rules:

```powershell
npx firebase-tools login
npx firebase-tools use --add
npx firebase-tools deploy --only firestore:rules
```

4. Commit and push the configuration. The GitHub Pages workflow automatically publishes the site.

The Firebase web configuration is safe to publish. It identifies the Firebase project, while [firestore.rules](firestore.rules) controls access. Do not commit the operator email password.

## Result

Teams and qualification settings are stored in Firestore and shared across all devices. Contact numbers are stored separately and can only be read by the configured operator account. Data remains until an operator deletes it.