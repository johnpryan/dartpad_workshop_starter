# A list of lists using Slivers

The code on the right builds the same UI as before, but this time it uses `Slivers`
instead of shrink wrapped `ListView` objects. The rest of this page walks you step-by-step
through the changes.

## How to migrate nested lists to Slivers

### Step 1

First, change your outermost ListView to a `SliverList`.

```dart
// Before
@override
Widget build(BuildContext context) {
  return ListView.builder(
    itemCount: numberOfLists,
    itemBuilder: (context, index) => innerLists[index],
  );
}
```

becomes:

```dart
// After
@override
Widget build(BuildContext context) {
  return CustomScrollView(slivers: innerLists);
}
```

---

### Step 2

Second, change the type of your inner lists from `List<ListView>` to
`List<SliverList>`.

```dart
// Before
List<ListView> innerLists = [];
```

becomes:

```dart
// After
List<SliverList> innerLists = [];
```

---

### Step 3

Now it's time to reconstruct the inner lists. The `SliverList` class is slightly
different than the raw `ListView` class, with the primary difference being the
appearance of a `delegate`.

The original version uses `ListView` objects for everything, unaware that the
inner builder constructors will be overridden by `shrinkWrap`.

```dart
// Before
@override
void initState() {
  super.initState();
  for (int i = 0; i < numberOfLists; i++) {
    final _innerList = <ColorRow>[];
    for (int j = 0; j < numberOfItemsPerList; j++) {
      _innerList.add(const ColorRow());
    }
    innerLists.add(
      ListView.builder(
        itemCount: numberOfItemsPerList,
        itemBuilder: (BuildContext context, int index) => _innerList[index],
        shrinkWrap: true,
        physics: const NeverScrollableScrollPhysics(),
      ),
    );
  }
}
```

After the change, `ListView` objects have been replaced with `SliverList` objects,
each using a `SliverChildBuilderDelegate` to provide efficient on-demand building.

```dart
// After
@override
void initState() {
  super.initState();
  for (int i = 0; i < numLists; i++) {
    final _innerList = <ColorRow>[];
    for (int j = 0; j < numberOfItemsPerList; j++) {
      _innerList.add(const ColorRow());
    }
    innerLists.add(
      SliverList(
        delegate: SliverChildBuilderDelegate(
          (BuildContext context, int index) => _innerList[index],
          childCount: numberOfItemsPerList,
        ),
      ),
    );
  }
}
```

## Lazy building, restored!

The code on the right has already applied these changes. Run the app and notice
that Flutter no longer has to immediately render 100 ColorRow widgets. As you
scroll, more widgets are built dynamically, just as you expect. What's better,
scrolling all the way to the next list doesn't incur any special cost.

Flutter is back to building widgets as they're needed, and no sooner.
