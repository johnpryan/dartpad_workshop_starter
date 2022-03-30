# Nested lists - ShrinkWrap vs Slivers

If you've seen the [Decoding Flutter episode on `ShrinkWrap` vs `Slivers`](https://www.youtube.com/watch?v=LUqDNnv_dh0),
then you know that nesting viewports would puncture a hole in the spacetime
continuum, and so Flutter doesn’t do it. Instead of rendering your UI, Flutter
directs you here to understand your options. Well, buckle up, because things are
about to start making a lot more sense.

## A list of lists using ShrinkWrap

On the right is some code that renders a list of lists using `ListView` objects,
with inner lists having their `shrinkWrap` value set to true. As the
[Decoding Flutter episode](https://www.youtube.com/watch?v=LUqDNnv_dh0) explains,
`shrinkWrap` forcibly evaluates the entire inner list, allowing it to request
finite heights instead of the usual height for `ListView` objects, which is infinity!

Here's the basic code structure:

```dart
ListView(
  // Setting `shrinkWrap` to `true` here is both unnecessary and expensive.
  children: <Widget>[
    ListView.builder(
      itemCount: list1Children.length,
      itemBuilder: (BuildContext context, int index) {
        return list1Children[index];
      },
      // This forces the `ListView` to build all of its children up front,
      // negating much of the benefit of using `ListView.builder`.
      shrinkWrap: true,
    ),
    ListView.builder(
      itemCount: list2Children.length,
      itemBuilder: (BuildContext context, int index) {
        return list2Children[index];
      },
      // This forces the `ListView` to build all of its children up front,
      // negating much of the benefit of using `ListView.builder`.
      shrinkWrap: true,
    ),
    ...
  ],
)
```

> **Note**: Observe that the outer `ListView` doesn't have its `shrinkWrap`
> value set to `true`. Only inner lists need to set `shrinkWrap`.

> **Also note**: Although `ListView.builder` (by default) efficiently builds its
> children, saving you the unnecessary cost of building off-screen widgets, setting
> `shrinkWrap` to `true` overrides this default behavior!

## Everything builds!

The scary part comes when you scroll through this UI and notice how the
`ColorBarState.build` method is called. Each inner list contains 100 elements,
so when the UI loads, you immediately see 100 instances of "Building
ColorBarState" printed to the console. Eek!

What's worse, once you scroll down roughly a hundred rows, another hundred build.
😱😱😱

## Lazily building nested lists

To see how to save your users from the threat of jank, check out Step 2, which
rebuilds the same UI with Slivers instead of ListViews.
