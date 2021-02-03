# Understanding the State in Flutter for Beginners

_We know everything is a widget in Flutter _

The very first code while creating a new project in Flutter starts with two types of widgets: **Stateless** and **Stateful**.

What is the difference between them?  
Why _Stateless Widget_ has less line of code than _Stateful_?  
Where do we use these two buddies? 😅

We will answer all that in this article. 💪

## What we are going to answer in this article

1.  What are **Stateless** and **Stateful** widgets?
2.  How are they different from each other?
3.  How do they work?

## Let's start

**Stateless** widget doesn't have any data that changes with time. It doesn't have any mutable state or internal state that updates on user interaction.

_Stateful_ has the mutable state, which will change over time.

_Oh wait! You said this is for beginners, but this is still not clear to me_ 😦.

Don't worry, everything is better with examples 😉 .

```dart
class  MyApp  extends  StatelessWidget {
final  String name = 'myName';
@override
Widget  build(BuildContext context) {
return  Text(name);
}
}
```

In the example, we used the **Text Widget**, which is a \*_Stateless_ widget.
In the above code, the `name` field is marked as final because the value of `name` will not change with user interaction.

> You may have more fields in your app, now I'm taking only one to keep things basic.

In the case of **Stateful** widget, we have some fields that might change over time.

```dart
class  MyHomePage  extends  StatefulWidget {
final  String name = 'Suresh';
@override
_MyHomePageState  createState() => _MyHomePageState();
}
class  _MyHomePageState  extends  State<MyHomePage> {

int age;
@override
Widget  build(BuildContext context) {
return  Text('you are ${widget.name} and $age years old');
}
}
```

In the above code, we can see that there are two fields: `name` and `age`.

`name` is immutable and it will not change but age can hence it is mutable.

How are we sure about this?

In **Stateful** widget, you can see that there are two classes.
One is simply a `Widget` and another is `State` Object

```dart
MyHomePage extends StatefulWidget
```

`Widget` has the field `name`, which is marked as _final_ and _State_ Object has the field age.

```dart
class  _MyHomePageState  extends  State<MyHomePage>
```

The **State** is a super class which accepts a stateful widget as a type parameter: `MyHomePage`

This state object contains only those fields **whose state may change.**

> Okay, I understand that age is mutable but who will change the internal state of age?

For this purpose, we drop the new Widget who can perform some action on user interaction. A button will be a good fit for this.

```dart
GestureDetector(
onTap: () {
setState(() {
age ++;
});
},
```

I have chosen the Gesture Detector, you can choose any from [this widget library](https://flutter.dev/docs/development/ui/widgets/material#Buttons)

The `onTap` function is performing two actions here

1. Updating the age field value
2. Marking this field as dirty (changed) and calls the framework to rebuild its children.

In the process of rebuilding, Flutter creates the whole new widget with the new data and replaces it with the old one. This happens very fast so we generally see the old one gets updated.

So, that's all for this article. I hope this helped you understand how the state is managed in Flutter. Let me know what you want me to write next on Flutter in the comment section.

Feel free to connect with [me on twitter](https://www.twitter.com/iamsureshsharma)
