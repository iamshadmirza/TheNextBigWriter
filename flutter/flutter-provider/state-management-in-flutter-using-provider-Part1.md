# State Management in Flutter using Provider: Part 1

State management is a little tricky topic when it comes to Flutter. We generally use `setState` for changing the value of fields and rebuilding the UI in beginning.

`setState` works well and it is indeed a good approach. But there are few complications with it, that's why we look for better state management. Once your code starts growing and it gets big enough to put it into a different file, you will start feeling the need for a **better approach**.

## Let's try to understand, how `setState` works

Whenever we call `setState`, two things happen:

1. It updates the field value in the `state` object.
2. It tells the framework to trigger a rebuild of the children with a new internal state.

Now, flutter tries to rebuild the whole widgets with the updated value. 

> This rebuilding process flutter calls widgets `build ` method 👇🏼

```dart
@override
Widget build(BuildContext context) {
	return MyApp();
}
```

When this method is called, the whole widget tree is rebuilt.

Some of the widgets need this rebuilding process to render the new value, but some of them get updated for no reason as the value they are getting is still the same 😓.

This affects the app's performance but in the case of small apps, these rebuilds don't cause critical performance issues. While in a complex app, the effect is noticeable.
That's why the `setState` will not so helpful for us.

There are so many [state management technique](https://flutter.dev/docs/development/data-and-backend/state-mgmt/options) available.  
You can choose anyone as per the requirement and complexity of the app you're working on.

That's it for this article. In Part 2, we will learn how the "Provider" solves this issue and help us build even complex apps. 👋