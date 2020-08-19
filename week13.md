# Tips 85-91

## #Day85 Neumorphic Design with `clay_containers`

`clay_containers` makes it easy to build Neumorphic UI.

1. Add dependency

    dependencies:
      clay_containers: ^version

2. Start using

        ClayContainer(
                color: baseColor,
                height: 200,
                width: 200,
                child:Center(child:newChild) //Put child inside Center to align it centrally.
                depth:45, // negative elevation(both +ve & -ve)
                curveType: CurveType.convex, //Curve of surface (concave, convex, plane)
                borderRadius: 200,
              )

![clay](assets/85claycontainer.png)

[see xbox controller demo](https://github.com/erluxman/clay_container_demo)

[visit clay_containers](https://pub.dev/packages/clay_containers#-readme-tab-)

## #Day 86 `provider`

Passing an object/bloc from a parent widget to it's children across the widget tree by passing it through every Widget constructor between parent and the reciever child is hard.

With `provider` you can easily pass object/bloc from parent to any widget below it in widget tree.

1. Add dependency
  
```dart
provider: ^4.1.3
```

2. Pass object/model/bloc from Parent Widget by wrapping any widget with Provider.

```dart
  @override
  Widget build(BuildContext context) {
    return Provider(
      create:(_)=> User("erluxman"),
      child: ScreenA(
        child:ScreenB(
          child:ScreenC(),
        ),
      ),
    );
  }

  class User{
    String name;
    User(this.name);
  }
```

3. Recieve object/model/bloc/ by calling `Provider.of<ObjectType>(context)`

```dart
class ScreenC extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    User user = Provider.of<User>(context);
    print(user.name); //erluxman
    return Container(
      child: Center(
        child: Text(user.name), //erluxman
      ),
    );
  }
}
```

[visit provider](https://pub.dev/packages/provider)

## #Day87 Flutter Sinppets

Using Flutter snippets helps gain speed and become productive by eliminating the time typing the boilerplate code by autocompleting various snippets.

[for android studio](https://plugins.jetbrains.com/plugin/12348-flutter-snippets)

[for vscode](https://marketplace.visualstudio.com/items?itemName=Nash.awesome-flutter-snippets)


<img src="assets/87snippets.gif" height ="650">

## #Day88 Create Emoji FloatingActionButton

When we get too used to using Icon in FloatingActionButton, we tend to forget that we can use various types of widget as FloatingActionButton's child.

We can use emoji Text as Child to FloatingActionButton to get wonderful colorful Fabs without any image.

```dart
FloatingActionButton(
  backgroundColor: Colors.white,
  child: Text(
    "🚀",
    textAlign: TextAlign.center,
    style: TextStyle(fontSize: 30),),
)
```

[try in codepen](https://codepen.io/erluxman/pen/vYLpgBo)



<img src="assets/88emojifab.gif" height ="800">

## #Day89  Run any task in a periodic interval  with `Timer.periodic()`

You can run any task repeatedly in a certain time period like this:

```dart
Timer.periodic(const Duration(seconds: 1), (Timer time) {
    setState(() {
        // Your code that runs periodically
        secondsPast += 1;
    });
});
```

[try on codepen](https://codepen.io/erluxman/pen/pogpqxX)


<img src="assets/89periodic.gif" height ="650">

## #Day90 Launcher Icon with ease

 **Don't want to create launcher Icons for platform and put them in place manually?**

 use `flutter_launcher_icons`

 1. Add dev dependency (__`remember dev_dependencies`__).

```yml
dev_dependencies:
  flutter_launcher_icons: ^0.7.5
```

 2. Configure flutter_icons (**`no spaces before flutter_icons:`**)

```yml
flutter_icons:
  android: "launcher_icon"
  ios: true
  image_path: "assets/images/ic_launcher.png" #use your image path
```

3. Generate Icons

```shell
flutter pub run flutter_launcher_icons:main
```

4. Run app

| Android icon |iOS icon|
|--|--|
|![](assets/90_android.png)| ![](assets/90_ios.png) |

[visit flutter_launcher_icons](https://pub.dev/packages/flutter_launcher_icons)

## #91  `dough` package

Want to make Flutter widgets smooshy like Jelly or Dough? Use the package `dough`

1. Add `dough` to dependency
```yml
dependencies:
  dough: ^version
```

2. Wrap any widget with `PressableDough()`. 

```dart
PressableDough(
  child: FloatingActionButton(
    onPressed: () {},
    child: Text("🧠",style: TextStyle(fontSize: 40)),
  ),
)
```

3. **Sorry to disappoint but you are already done 😜**

[sample gist](https://gist.github.com/erluxman/1e102548403db046872d7db530e73594)

[visit dough](https://pub.dev/packages/dough#-installing-tab-)

<img src="assets/91doughh.gif" height ="800">

[___`Tips 1-7`___](README.md)
[__`Tips 08-14`__](week02.md)
[__`Tips 15-21`__](week03.md)
[__`Tips 22-28`__](week04.md)
[__`Tips 29-35`__](week05.md)
[__`Tips 36-42`__](week06.md)
[__`Tips 43-49`__](week07.md)
[__`Tips 50-56`__](week08.md)
[__`Tips 57-63`__](week09.md)
[__`Tips 64-70`__](week10.md)
[__`Tips 71-77`__](week11.md)
[__`Tips 78-84`__](week12.md)

[__`<< Previous`__](week12.md)
[___`Tips 85-91`___](week13.md)
[__`Next >>`__](week14.md)
