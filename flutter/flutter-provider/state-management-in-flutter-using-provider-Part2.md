# State Management in Flutter using Provider: Part 2

In previous [article](https://suresh.hashnode.dev/state-management-in-flutter-using-provider-part-1-cke8vk1cb00iny0s11lu933ch)
we have discussed the problem of using `setState` to update the app's state in the moderate or complex app.

## What we are going to know in this article

1. Why we should use provider
2. What are the types of provider
3. How to use provider in our code

In this article we'll know about `provider` package owned by  [Remi Rousselet](https://github.com/rrousselGit/provider), this is one of the best state management technique we can use in our app.

### Why we should use provider

 On the beginner stage, we generally use the `setState` to update the state of our app, because its easy to do so, and on this stage, if we try to use some moderate or say a complex type of state management technique like `flutter_bloc` or `Mobx`, it is not easy for beginners to take a big jump from using `setState` to these state management technique 😓

 
``` 
provider uses InheritedWidget internally, to manage all those complex computations and provide us simple and great feature to manage our state
```

&nbsp;

> Why `provider`? We have some other techniques that can pass data in the widget tree.

Yes, there is some other way, such as passing data via constructors this can be done, but definitely not the good approach.

***Explanation***
>Passing data via constructors, this is not feasible if data is 3 or 4 widgets above in the tree and we are trying to pass the data via constructor through a widget, and in doing so, all those widgets will rebuild just for passing the data. This may cause the performance issue and our code get too much complicated.

So, what we should do now? 

We will use provider 

``` 
flutter_bloc and Mobx use provider internally 🥳 And now the flutter team also supports to use provider for state management.
```

So, let's get started knowing more about provider

### What are the types of provider

&nbsp;

Provider has enough categories to handle different type of objects

The complete list of all the objects available is [here](https://pub.dev/documentation/provider/latest/provider/provider-library.html)

| Name|Description|
|-----|-----------|
|Provider|The most basic form of provider. It takes a value and exposes it, whatever the value is.|
|ListenableProvider|A specific provider for Listenable object. ListenableProvider will listen to the object and ask widgets which depend on it to rebuild whenever the listener is called.|
|ChangeNotifierProvider|A specification of ListenableProvider for ChangeNotifier. It will automatically call `ChangeNotifier.dispose` when needed.|
|ValueListenableProvider|Listen to a ValueListenable and only expose `ValueListenable.value`.|
|StreamProvider|Listen to a Stream and expose the latest value emitted.|
|FutureProvider|Takes a `Future` and updates dependents when the future completes.|

&nbsp;

### So, let's discover more about them

### **Provider**

This is a very basic form of `provider`, Provider that manages the lifecycle of the value it provides by delegating to a pair of `Create` and `Dispose`. This can provider any type of value.

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

### **ListenableProvider** 

ListenableProvider is a bit different from the other providers in the list, as this provider provides `state source` as the value.

Need more clarity?
 
> Sure, Other providers generally provide the single value from the `object<T>`, but `ListenableProvider` provides the whole model as the value to its dependents.
When the state changes in Listenable, it notifies the provider about the state change. Now provider, via it's `InheritedWidget`
marks it's listening dependent to rebuild.


In the above example, the whole `Counter()` object is being returned from `create`, as this value is provided to the dependents, dependents use this value as `Counter()` and updates it's state and rebuilds again to show the updated value on the screen.

### **ChangeNotifierProvider** 

In change notifier provider everything is same as `ListenableProvider`, one additional specification of `ListenableProvider` for ChangeNotifier. It will automatically call `ChangeNotifier.dispose` when needed.

 `ChangeNotifier` can be used with `ListenableProvider<T>`, but `ChangeNotifierProvider<T>` provides one additional benefit of disposing the ChangeNotifier when done using ChangeNotifier's dispose() method.

### **ValueListenableProvider** 

`ValueListenableProvider` gets the value change notification from  `ValueListenable`, and provides the value to its dependent as state. `ValueListenableProvider<T>` receives values of type T from a `ValueListenable<T>`.

### **StreamProvider** 


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

### **FutureProvider** 

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
This, `FutureProvider<int>` gives the binary value 0 and 1, in the initial state it provides the 0, and as soon as future resolves (after 4 seconds)this provides the 1 as value

### How to use provider in our code

Provider has some methods

- `context.watch<T>()`, which makes the widget listen to changes on `T`
- `context.read<T>()`, which returns `T` without listening to it
- `context.select<T, R>(R cb(T value))`, which allows a widget to listen to only a small part of `T`.

Or we can use the `static` method `Provider.of<T>(context)` or  `Provider.of<T>(context, listen : false)` which will behave similarly to `watch`/`read` respectively

### How these methods work

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

 In case of `select((T value))`, it only listen to those part of `T`, if state change happens in this part, only then it's dependents will update there value. It prevents widget to unnecessarily rebuilding if something other changes.

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

### Few things about Consumer and Selector 

Consumer gets the value from ancestors using `Provider<T>` and passes this value to it's `builder`
> Consumer widget gets the value from the `Provider<T>` when there is no `BuildContext`

`Selector` works same as `select((T value))`, it rebuilds only when, if there is a change in selected value, for which this is listing, no rebuilds happens when others value changes

`Selector` determines, if `builder` needs to be called again by comparing the previous and new result of `selector` using `DeepCollectionEquality` from the package collection

So, that's all for this article. I hope this helped you to understand provider in Flutter. If I'm left with something crucial, please let me know in the comment section.

Feel free to connect with [me on twitter](https://www.twitter.com/iamsureshsharma)
