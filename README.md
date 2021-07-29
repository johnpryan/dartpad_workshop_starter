# DartPad Workshop Template

## Quickstart (Firebase Hosting)

1. Fork this repository

2. Install the [Firebase CLI](https://firebase.google.com/docs/cli)

3. Set the default project ID in `.firebaserc`:

```
{
  "projects": {
    "default": "<FIREBASE_PROJECT_ID>"
  }
}
```

4. Deploy to Firebase:

```bash
firebase deploy
```

5. Load in DartPad using the following URL, replacing `<FIREBASE_PROJECT_ID>`
   with your project ID:

```
https://dartpad.dev/workshops.html?webserver=https://<FIREBASE_PROJECT_ID>.web.app
```

For more information, see the [Workshop Authoring
Guide](https://github.com/dart-lang/dart-pad/wiki/Workshop-Authoring-Guide) on
the DartPad wiki.
