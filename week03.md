# Tips 15-21

## #Day15 Flexible vs Expanded

Expanded() is nothing more than Flexible() with

    Flexible (fit: FlexFit.tight) = Expanded()

but, Flexible uses `fit :FlexFit.loose` by default.

**FlexFit.tight** = Wants to fit tight into parent taking as much space as possible.

**FlexFit.loose** = Wants to fit loose into parent taking as little space as possible for itself.

**flex** = The factor of space taken from parent. Mostly not fully used if `flex: FlexFit.loose` used i.e. `Flexible`.

<img src="assets/15flexibleexpanded.png" height ="800">

If you fully read the following image, you will fully understand the difference between `Flexible` and `Expanded`
![expanded](assets/15expandedvsflexible.png)

[try in codepen](https://codepen.io/erluxman/pen/JjYKZGG)

## #Day16 Bulk declaration

If you have been declaring each member separately all the time, you can declare members of same types at once.

I wouldn't declare `age` and `shoeSize` at once because they are not related.

With great power comes great responsibility, Use this wisely.
![singleline](assets/16singlelinedeclartion.png)

## #Day17 SliverAppBar / Collapsable AppBar / ParallaxHeader

Remember CollapsableAppBar (android) / ParallaxHeader (ios)? We have SliverAppBar in Flutter to do exactly that.

To use it, you will have to have a CustomScrollView as parent.

then you add two slivers of it.

1. SliverAppBar
2. SliverFillRemaining

You can play with values of snap, floating, pinned etc to get desired effect

[try on dartpad](https://dartpad.dartlang.org/6874032a7a1ea129640b8f617f7ffed3)

[see various types of SliverAppBars here](https://api.flutter.dev/flutter/material/SliverAppBar-class.html#snippet-container)

![sliverappbar](assets/17sliverappbars.gif)

## #Day18 What the Key

<img src="assets/18keys.gif" height ="600">

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

## #Day19 Amazing Library Time.dart

If you are tired to long and verbose DateTime and Duration calculation `Time.dart` comes to your rescue.

    //Before
    var 3dayLater = DateTime.now().add(Duration(days: 3)).day;

    //After
    var 3dayLater = 3.days.fromNow.day;


    //Before
    var duration = Duration(minutes: 10) +Duration(seconds: 15) -
        Duration(minutes: 3) +Duration(hours: 2);

    //After
    var duration = 10.minutes + 15.seconds - 3.minutes + 2.hours;

    //Before
    await  Future.delayed(Duration(seconds: 2))

    //After
    await 2.seconds.delay

[visit time.dart](https://github.com/jogboms/time.dart)

## #Day20 Testing errors

You can simply test if two values are equal in dart with `expect(actual, expected)`

But if you want to test errors use the `function closure` that throws error as actual and check with `throwsA<ErrorType>` as expected.

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

## #Day21 Concisely add collection into collection with `Spread(...)` operator

We normally use addAll() on collection to add one collection to another.

But From dart 2.3 and above, we can use Spread Operator (`...`) to add collection inside collection.

![nullsfae](assets/21nullsafecollectioninsert.png)

[try in dartpad](https://dartpad.dev/98c2ab9d41fb2c20cc67c94956972721)

[___`Tips 1-7`___](README.md)
[__`Tips 08-14`__](week02.md)

[__`<< Previous`__](week02.md)
[___`Tips 15-21`___](week03.md)
[__`Next >>`__](week04.md)

[__`Tips 22-28`__](week04.md)
[__`Tips 29-35`__](week05.md)
[__`Tips 36-42`__](week06.md)
[__`Tips 43-49`__](week07.md)
[__`Tips 50-56`__](week08.md)
[__`Tips 57-63`__](week09.md)
[__`Tips 64-70`__](week10.md)
[__`Tips 71-77`__](week11.md)
[__`Tips 78-84`__](week12.md)
[__`Tips 85-91`__](week13.md)
[__`Tips 92-98`__](week14.md)
