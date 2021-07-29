# DartPad Workshop Starter Pack
A starter project for DartPad workshops. Follow the quickstart below to create
your own step-by-step workshop, similar to these
[workshops](https://github.com/flutter/codelabs/tree/master/dartpad_codelabs)
maintained by the Flutter team:

- [Getting Started with Slivers](https://dartpad.dev/workshops.html?webserver=https://dartpad-workshops-io2021.web.app/getting_started_with_slivers)
- [Inherited Widget](https://dartpad.dev/workshops.html?webserver=https://dartpad-workshops-io2021.web.app/inherited_widget)
- [Null Safety](https://dartpad.dev/workshops.html?webserver=https://dartpad-workshops-io2021.web.app/null_safety_workshop)

For more information on authoring a DartPad workshop, see the [Workshop Authoring
Guide](https://github.com/dart-lang/dart-pad/wiki/Workshop-Authoring-Guide) on
the DartPad wiki.


# Quickstart (Firebase Hosting)

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

4. Edit the files in `public/` to create your own step-by-step workshop. The
   `meta.yaml` to configures the metadata such as the project type (Dart or
   Flutter), number of steps, and title.

4. Deploy to Firebase:

```bash
firebase deploy
```

5. Load in DartPad using the following URL, replacing `<FIREBASE_PROJECT_ID>`
   with your project ID:

```
https://dartpad.dev/workshops.html?webserver=https://<FIREBASE_PROJECT_ID>.web.app
```
