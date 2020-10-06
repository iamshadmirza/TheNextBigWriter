# State Management in Flutter using Provider: Part 2

In the previous [article](https://suresh.hashnode.dev/state-management-in-flutter-using-provider-part-1-cke8vk1cb00iny0s11lu933ch),
we have discussed the problem of using `setState` to update the app's state in the moderate or complex app, This part will cover the solution to those problems. Let's start.

## What we are going to learn in this article

1. What is Provider, Why we use it?
2. What are the types of Provider?
3. How to use Provider in our code?
4. What is Consumer & Selector?
  
### 1. What is Provider, Why we use it

`Provider` is one of the most popular state management solution, created by  [Remi Rousselet](https://github.com/rrousselGit/provider), used for flutter app development.

On the beginner stage, we use `setState` to update the app's state, because it is easy, and switching from `setState` to other complex techniques like `flutter_bloc` or `Mobx` is not that easy to follow. 😓

Provider uses `InheritedWidget` internally, to manage all complex computations and provide a simple feature to manage our app's state

> Why `provider`? We have some other techniques that can be used for managing state.

Passing data via constructors is not a good idea. In doing so, all those widgets will rebuild just for passing the data. This may cause the performance issue and our code get too much complicated.

So, what we should do now? We will use the provider

> `flutter_bloc` & `Mobx` uses provider internally 🥳 And now the flutter team also recommends using the provider.

So, let's learn about the types of provider

### 2. What are the types of provider

Provider can handle different type of objects

Complete [list of all objects](https://pub.dev/documentation/provider/latest/provider/provider-library.html)

| Name|Description|
|-----|-----------|
|Provider|The most basic form of provider. It takes a value and exposes it, whatever the value is.|
|ListenableProvider|A specific provider for Listenable object. ListenableProvider will listen to the object and ask widgets which depend on it to rebuild whenever the listener is called.|
|ChangeNotifierProvider|A specification of ListenableProvider for ChangeNotifier. It will automatically call `ChangeNotifier.dispose` when needed.|
|ValueListenableProvider|Listen to a ValueListenable and only expose `ValueListenable.value`.|
|StreamProvider|Listen to a Stream and expose the latest value emitted.|
|FutureProvider|Takes a `Future` and updates dependents when the future completes.|

So, let's discover more about the categories

#### Provider

This is a very basic form of `Provider`, manages the lifecycle of the value it provides by delegating to a pair of `Create` and `Dispose`. This can provide any type of value.

```dart
class Counter {
    int count = 0;

  void increment() {
      count += 1;
      notifyListeners();
  }
}

class Stateless extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Provider<Counter>(
      create: (context) =>  Counter(),
      dispose: (context, value) => value.dispose(),
      child: ...,
    );
  }
}

```

#### ListenableProvider

`ListenableProvider` is a bit different from the other providers in the list, as this provider provides `state source` as the value.

Other providers generally provide the single value from the `object<T>`, but `ListenableProvider` provides the whole model as the value to its dependents.
When the state changes in Listenable, it notifies the provider about the state change. Now provider, via it's `InheritedWidget`
marks it's listening dependent to rebuild.

In the above example, the whole `Counter()` object is being returned from `create`, as this value is provided to the dependents, dependents use this value as `Counter()` and updates it's state and rebuilds again to show the updated value on the screen.

#### ChangeNotifierProvider

In the change notifier provider, everything is the same as `ListenableProvider`, one additional specification of `ListenableProvider` for ChangeNotifier is, it automatically calls `ChangeNotifier.dispose` to dispose the provider when needed.

#### ValueListenableProvider

`ValueListenableProvider` gets the value change notification from  `ValueListenable`, and provides the value to its dependent as state. `ValueListenableProvider<T>` receives values of type T from a `ValueListenable<T>`.

#### StreamProvider

StreamProvider gets the events from a subscribed stream and provides these events(values) to its dependent widgets. we can use `StreamProvider<T>` to receive events of type T from a `Stream<T>`.

```dart
StreamProvider<int>(
  initialData: 0,
  builder: (context) {
    return Stream<int>
      .periodic(Duration(milliseconds: 100), (count) => count + 1)
      .take(100);
  },
  child: ...
)

```

In the above example, `StreamProvider` emits `count` value ranges from 0 to 100, on the interval of 100 milliseconds, dependents can use these events for some purpose.

#### FutureProvider

`FutureProvider` gets the value of a future and provides to its dependents. We can use `FutureProvider<T>` to get the `Future<T>` value and this value represents the state.

```dart
FutureProvider<int>(
  initialData: 0,
  builder: (context) {
    return Future.delayed(Duration(seconds: 4), () => 1);
  },
  child: ...
),
```

This, `FutureProvider<int>` gives the binary value 0 and 1. In the initial state, it provides the 0, and as soon as future resolves (after 4 seconds)this provides the 1 as a value

### 3. How to use a provider in our code

Provider has some methods and we will look at 3 major one

- `context.watch<T>()`, which makes the widget listen to changes on `T`
- `context.read<T>()`, which returns `T` without listening to it
- `context.select<T, R>(R cb(T value))`, which allows a widget to listen to only a small part of `T`.
  
> Here `<T>` is a type of value, like `String`, `int`, `double` or any other complex type

We can also use the `static` method `Provider.of<T>(context)` or  `Provider.of<T>(context, listen : false)` which will behave similarly to `watch`/`read` respectively

### How these methods work 🤔

These methods will look up in the widget tree starting from the widget associated with the `BuildContext`, and will return the nearest variable of type `T` found (or throw if nothing is found).

```dart
class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text(
      context.watch<String>(),
    );
  }
}
```

we must pass the `type<>` here in `watch()`, searches the same type of data in the widget tree. this `watch()` will listen to a state change, and rebuilds with the new value, whenever the state changes.

Similarly, `read<T>()` will look for the variable of type `T` in the widget tree from it's `BuildContext` and retrieves the data.

In the case of `select((T value))`, it only listens to those parts of `T`, if state change happens in this part, only then it's dependents will update there value. It prevents widget from unnecessarily rebuilding if something other changes.

Now, one static method which works the same as the above method `Provider.of<T>(context)` this method performs the same as `watch()`, listen to changes in state `T`

 ```dart
class Home extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
      String provider = Provider.of<String>(context);
    return Text(provider
    );
  }
}
```

`Provider.of<T>(context)` method has `listen`, which is set to `true` by default, which means if we are using this method it will listen to state change.

If we set `listen` to `false` then, this will not listen to state change

Alternatively, the same thing we can also obtain by using [Consumer](https://pub.dev/documentation/provider/latest/provider/Consumer-class.html) and [Selector](https://pub.dev/documentation/provider/latest/provider/Selector-class.html)

### Introduction to Consumer and Selector

The consumer gets the value from ancestors using `Provider<T>` and passes this value to it's `builder`
> Consumer widget gets the value from the `Provider<T>` when there is no `BuildContext`

`Selector` works same as `select((T value))`, it rebuilds only when, if there is a change in selected value, for which this is listing, no rebuilds happen when others value changes

`Selector` determines, if `builder` needs to be called again by comparing the previous and new result of `selector` using `DeepCollectionEquality` from the package collection

### Takeaways

- We learned how `provider` helps to overcome the limitations of `setState` in a complex project
- Discussed 5 different types of `provider`
- We got to know that `flutter_bloc` & `Mobx` also uses `provider` internally
- Got introduction about Consumer & Selector Widget
  
So, that's all for this article. I hope this helped you to understand the provider in Flutter. If I'm left with something crucial, please let me know in the comment section.

Feel free to connect with [me on twitter](https://www.twitter.com/iamsureshsharma)
