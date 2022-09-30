# ❤️Awesome Flutter ❤️ tips and tricks ❤️
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Ferluxman%2Fawesomefluttertips&count_bg=%2379C83D&title_bg=%23555555&icon=prometheus.svg&icon_color=%23E7E7E7&title=hits&edge_flat=true)](https://hits.seeyoufarm.com)<a href="https://github.com/Solido/awesome-flutter">
   <img alt="Awesome Flutter" src="https://img.shields.io/badge/Awesome-Flutter-blue.svg?longCache=true&style=flat-square" />
</a>

## Tip 1 : `stless` & `stful`

We can type `stless` and `stful` and we get Autocomplete Suggestion to generate Stateless Flutter Widget or Stateful Flutter Widget Respectively.

![statful](assets/01stlesstful.gif)

## Tip 2 : `If Null` Operator (`??`)

`??` checks If something is `null`. If it's not null it returns its own value but if it's `null` it returns the value after `??`

`return abc??10; //returns 10 if abc is null else returns its own value,`

It also has shorthand assignment when it's null.

`abc??=5 //assigns 5 to abc if it's null`

```dart
testOldMethod() {
  print("NullChecking in old way");
  var abc;
  
  if (abc == null) {
    print("It's null");
  } else {
    print(abc);
  }

  if (abc == null) {
    abc = 5;
  }
  print(abc);
}

testIfNullOperator() {
  print("NullChecking with if Null Operator");
  var abc;

  print(abc ?? "It's null");
  abc ??= 5;
  print(abc ?? "It's null");
}
```
Output:
```
NullChecking in old way
It's null
5
--------------------
NullChecking with if Null Operator
It's null
5
```

## Tip 3 : Inner Function

We can define a function inside another function.

This is to encapsulate the inner function from everything else outside the outer function.

```dart
main() {
  String getName() {

    String getFirstName() { return "Laxman"; }

    String getLastName() { return "Bhattarai"; }

    return getFirstName() + " " + getLastName();
  }

  print(getName());
}
```
Output
```
Laxman Bhattarai
```


## Tip 4 : ..Cascade..Chaining..Fluent API

We can chain method/member calls without returning `this` from **method(), getter() and setter()** using cascade operator (..)

try in [Dartpad](https://dartpad.dartlang.org/290e17306b745ed83b9242653ca55041)

Before:
```dart
class User {
  String name;
  int age;

  User({this.name = "Foo", this.age = 0});

  User withName(String name) {
    this.name = name;
    return this;
  }

  User withAge(int age) {
    this.age = age;
    return this;
  }

  void printId() => print("$name is $age years old.");
}

main() {
  User()
  .withAge(27)
  .withName("Laxman")
  .printId();
}
```

Can be replaced with
```dart
class User {
  String name;
  int age;

  void printId() => print("$name is $age years old.");
}

main() {
  User()
  ..age = 27
  ..name = "Laxman"
  ..printId();
}
```

## Tip 5 : Dart `data class`

Dart does not support data class by default, but with plugins, we can simply generate data class (`copyWith()`,`fromMap()`, `toMap()`, `Named Constructor`, `toString()`,`hashCode()` & `equals()` methods implemented by the tool).

### `🚨❗️Caution❗️🚨` : **Your cursor should be inside the class that you want to generate data class.**

![dataclass](assets/05dataclass.gif)

Download Plugins :

[For Android Studio](https://plugins.jetbrains.com/plugin/12429-dart-data-class)

[For VsCode](https://marketplace.visualstudio.com/items?itemName=BendixMa.dart-data-class-generator)

## Tip 6 : RichText Widget

If you want to have a single text with different style within it? Do not bother or try to hack with with `Text()` and use `RichText()` with `TextSpan()`

[Try on dartpad](https://dartpad.dartlang.org/f87dddb2f48f1d1ef0f25903af1ded58)

[See Youtube Demo](https://www.youtube.com/watch?v=rykDVh-QFfw)

![richtext](assets/06richtext.png)

## Tip 7 : Spacer Widget

Using Container with certain height/width to create responsive space between Widgets? That may look good on one screen but will not look the same in different screen size.

Spacer Widget comes for the rescue. Instead of `Container(width: / height: )`, use `Spacer(flex: )`.

How on this earth did I not know about this widget earlier? This is going to save many lives 😂

[Try on dartpad](https://dartpad.dev/f0d077124527a8078cdb2eede1e9bf73)

[See Youtube Demo](https://www.youtube.com/watch?v=7FJgd7QN1zI)

![spacer](assets/07spacer.gif)

## Tip 8 : ListView.separated()

If you have you been adding `Container()` with `maxwidth` at the bottom of `ListItem` to put divider line like me, you have been doing it wrong all the time.

Flutter has `ListView.separated` just for that purpose. We have to also provide `separatorBuilder` in addition to what we already passed while using `ListView.builder`

**Bonus 🍾🎁🎊🎉 : You do not have to check if the item is last in order not to draw divider after the last item.**

[try in dartpad](https://dartpad.dartlang.org/31ec967b140ac6a5795c38ea4bdfd9a2)

```dart
ListView.separated(
  itemCount: 25,
  separatorBuilder: (BuildContext context, int index) => Divider(
    thickness: 1,
  ),
  itemBuilder: (BuildContext context, int index) {
    return ListTile(
      title: Text(
        'Index Number $index',
      ),
    );
  },
);
```

## Tip 9 : Passing Function as parameter

We can simply pass a `function` as `parameter` like we pass a variable. When we want to call the passed function from calling function, we just call it with `()` at the end along with parameters if it accepts any.

[try in dartpad](https://dartpad.dev/fa46336f5c1b3287c6420d3b3a277178)

```dart
void main() {
  f2(f1, 3);
  f2(f1, 4);
  f2(f1, 7);
}

f1(int venOrOdd) {
  print("$evenOrOdd is ${evenOrOdd % 2 == 0 ? "Even" : "Odd"}");
}

f2(Function(int) evenOrOddFunction, int argumentToPass) {
  evenOrOddFunction(argumentToPass);
}
```
OutPut
```dart
3 is Odd
4 is Even
7 is Odd
```

---

## Tip 10 : Relative Import : the right way to import `.dart` files we have in our lib package

Ever wondered what is the right way to import a file in your own package?

Prefer relative imports to absolute imports.

Why?

- It's shorter and cleaner.
- We can easily differentiate our files and third-party ones.
- It makes sense, doesn't it?

```
my_package
└─ lib
   ├─ src
   │  └─ utils.dart
   └─ api.dart
```
If `api.dart` wants to import `utils.dart`, it should do so using:
```dart
import 'src/utils.dart';
```

And not:
```dart
import 'package:my_package/src/utils.dart';
```

## Tip 11 : Reusing Text Style

Tired of defining `textStyle` everytime you want to customize `Text`? **Even worse** if you have multiple theme (**dark, light, full black theme etc**).

just use

`Theme.of(context).textTheme.title`

where there are other styles like `title` inside `textTheme`.

[try in dartpad with theme example](https://dartpad.dartlang.org/5270714ce97853fc36db1b17c255c999)

```dart
Text(
  "Title",
  style: Theme.of(context).textTheme.title,
)
```

## Tip 12 : Use Literal to initialize growable collections

If we are to initialize growable collection, use literal initialization rather than with constructors.

```dart
// Good
var points = [];
var addresses = {};

// Bad
var points = List();
var addresses = Map();

// With type argument

// Good
var points = <Point>[];
var addresses = <String, Address>{};

// Bad
var points = List<Point>();
var addresses = Map<String, Address>();
```

## Tip 13 : Fat arrow functions

We can use fat arrow `=>` members (`function, getter,setter`) in dart.

I would not use `=>` if the declaration is not **ONE LINER**. But few lines are OK.

[try on dartpad](https://dartpad.dev/76922028eccb4535f0cdddc8e4b17aa1)

```dart
void main() {
  User()
    ..firstName = "Laxman"
    ..lastName = " Bhattarai"
    ..age = 18
    ..printUser();
}

class User {
  String firstName;
  String lastName;
  DateTime birthday;

  String get fullName => firstName + lastName;

  set age(int age) =>  birthday = DateTime.now().subtract(Duration(days: age * 365));

  int get age => DateTime.now().year - birthday.year;

  bool get isAdult => age >= 18;

  printUser() => print(fullName + " is a ${isAdult ? "Adult" : "Child"}");
}
```

## Tip 14 : FractionallySizedBox

Ever wanted the widget to have height and width exactly in the same proportion to it's screen's height and width?

FractionallySizedBox is build exactly for that use case. Just give it the fraction you need for your height and width and it will handle everything else. The fraction value will range between 0.0 to 1.0

```dart
FractionallySizedBox(
  widthFactor: 0.5,
  heightFactor: 0.5,
  child: Container(color: Colors.green),
)
```
[try on codepen](https://codepen.io/erluxman/pen/rNOLOzG)

![fractionally](assets/14fractionallysizedbox.gif)

## Tip 15 : Flexible vs Expanded

Expanded() is nothing more than Flexible() with

```dart
Flexible (fit: FlexFit.tight) = Expanded()
```

but, Flexible uses `fit :FlexFit.loose` by default.

**FlexFit.tight** = Wants to fit tight into parent taking as much space as possible.

**FlexFit.loose** = Wants to fit loose into parent taking as little space as possible for itself.

**flex** = The factor of space taken from parent. Mostly not fully used if `flex: FlexFit.loose` used i.e. `Flexible`.

![flex](assets/15flexibleexpanded.png)

If you fully read the following image, you will fully understand the difference between `Flexible` and `Expanded`

```dart
class Flexible extends... {
  /// The flex factor to use for this child
  ///
  /// If null or zero, the child is inflexible and determines its own size. If
  /// non-zero, the amount of space the child's can occupy in the main axis is
  /// determined by dividing the free space (after placing the inflexible
  /// children) according to the flex factors of the flexible children.
  final int flex;

  /// How a flexible child is inscribed into the available space.
  ///
  /// If [flex] is non-zero, the [fit] determines whether the child fills the
  /// space the parent makes available during layout. If the fit is
  /// [FlexFit.tight], the child is required to fill the available space. If the
  /// fit is [FlexFit.loose], the child can be at most as large as the available
  /// space (but is allowed to be smaller).
  final FlexFit fit;

  ........
}

class Expanded extends Flexible {
  /// Creates a widget that expands a child of a [Row], [Column], or [Flex]
  /// so that the child fills the available space along the flex widget's
  /// main axis.
  const Expanded({
    Key key,
    int flex = 1,
    @required Widget child,
  }) : super(key: key, flex: flex, fit: FlexFit.tight, child: child);
}
```

[try in codepen](https://codepen.io/erluxman/pen/JjYKZGG)

## Tip 16 : Bulk declaration

If you have been declaring each member separately all the time, you can declare members of same types at once.

I wouldn't declare `age` and `shoeSize` at once because they are not related.

With great power comes great responsibility, Use this wisely.

```dart
class Footballer {

  String firstName = "Lionel";
  String middleName = "Andrés";
  String lastName = "Messi";

  double weightKG;
  double heightCM;

  int goals;
  int assists;
  int tackles;
  int takeons;
  int saves;
  int shots;
}

// The class above can be replaced with:
class Footballer {

  String firstName = "Lionel", middleName = "Andrés", lastName = "Messi";

  double weightKG, heightCM;

  int goals, assists, tackles, takeons, saves, shots;
}
```

## Tip 17 : SliverAppBar / Collapsable AppBar / ParallaxHeader

Remember CollapsableAppBar (android) / ParallaxHeader (ios)? We have SliverAppBar in Flutter to do exactly that.

To use it, you will have to have a CustomScrollView as parent.

then you add two slivers of it.

1. SliverAppBar
2. SliverFillRemaining

You can play with values of snap, floating, pinned etc to get desired effect

[try on dartpad](https://dartpad.dartlang.org/6874032a7a1ea129640b8f617f7ffed3)

[see various types of SliverAppBars here](https://api.flutter.dev/flutter/material/SliverAppBar-class.html#snippet-container)

![sliverappbar](assets/17sliverappbars.gif)

## Tip 18 : What the Key

![keys](assets/18keys.gif)

Ever wondered why we need GlobalKey(children : GlobalObjectKey, LabeledGlobalKey), LocalKey(children: ObjectKey, ValueKey & UniqueKey) right?

They are used to access or restore state In a statefulWidget (Mostly we don't need them at all if our widget tree is all Stateless Widgets).

### Purpose (Key to use inside bracket)

- Mutate the collection i.e. remove / add / reorder item to list in stateful widget like draggable todo list where checked items get removed (ObjectKey, ValueKey & UniqueKey)
- Move widget from one Parent to another preserving it's state. (GlobalKey)
- Display same Widget in multiple screens and holding its state.(GlobalKey)
- Validate Form.(GlobalKey)
- You can to give a key without using any data. (UniqueKey)
- If you can use certain field of data like UUID of users as unique Key. (ValueKey)
- If you do not have any unique field to use as key but object itself is unique. (ObjectKey)
- If you have multiple Forms or Multiple Widgets of same type that need GlobalKey. (GlobalObjectKey, LabeledGlobalKey whichever is appropriate , similar logic to ValueKey and ObjectKey)

[Learn more on this video](https://www.youtube.com/watch?v=kn0EOS-ZiIc)

## Tip 19 : Amazing Library `time.dart`

If you are tired to long and verbose DateTime and Duration calculation `time.dart` comes to your rescue.

```dart
//Before
var 3dayLater = DateTime.now().add(Duration(days: 3)).day;

//After
var 3dayLater = 3.days.fromNow.day;

//Before
var duration = Duration(minutes: 10) +Duration(seconds: 15) 
  - Duration(minutes: 3) + Duration(hours: 2;

//After
var duration = 10.minutes + 15.seconds - 3.minutes + 2.hours;

//Before
await  Future.delayed(Duration(seconds: 2))

//After
await 2.seconds.delay
```
[visit time.dart](https://github.com/jogboms/time.dart)

## Tip 20 : Testing errors

You can simply test if two values are equal in dart with `expect(actual, expected)`

But if you want to test errors use the `function closure` that throws error as actual and check with `throwsA<ErrorType>` as expected.

```dart
void main() {
  group("Exception/Error testing", () {
    test("test method that throws errors", () {
      expect(_testError(fails: false), false);
      expect(() => _testError(fails: true), throwsA(isA<FooError>()));
    });
  });
}

bool _testError({bool fails}) {
  if(fails)throw FooError();
    return fails;
}

class FooError extends Error {}
```

[___`Tips 1-20`___](README.md)
[__`Next >>`__](page2.md)

[__`Tips 41-60`__](page3.md)
[__`Tips 61-80`__](page4.md)
[__`Tips 81-100`__](page5.md)
