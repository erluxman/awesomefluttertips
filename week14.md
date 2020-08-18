---
title: Flutter Tips 85-91
date: '2020-07-12'
spoiler: 14th batch of 7 tips and tricks on the series 100DaysOfFlutter.
---

## #92 Autocomplete TextField with `flutter_typeahead`

Autocomplete TextField can be implemented with `flutter_typeahead` Package.

1. Add Dependency

```yml
dependencies:
  flutter_typeahead: ^version
```

2. Use `TypeAheadFormField` / `TypeAheadField`

```dart
var platforms = ["Flutter", "Android", "iOS", "Mac", "React", "Cordova"];
final TextEditingController input = TextEditingController();

TypeAheadFormField(
  textFieldConfiguration: TextFieldConfiguration(
    decoration: InputDecoration(labelText: 'City'),
    controller: this.input),

  //Search and return found values
  suggestionsCallback: (pattern) => platforms.where(
    (item) => item.toLowerCase().contains(pattern.toLowerCase()),
  ),
  itemBuilder: (_, item) => ListTile(title: Text(item)),
  onSuggestionSelected: (query) => this.input.text = query,
),
```

[visit flutter_typeahead](https://pub.dev/packages/flutter_typeahead)

[visit demo](https://gist.github.com/erluxman/523818577fa54cb6d0f5e0e8cc1d6a9a)


<img src="assets/92_autocomplete_textfield.gif" height ="600">

## #Day93 Read Network State with `connectivity` package

`connectivity` package makes it easy to read network state of device.

1. Add dependency

```yml
dependencies:
  connectivity: ^version
```

2. Read network states

```dart
class State ...{
  @override
  initState() {
    super.initState();
    subscription = Connectivity()
      .onConnectivityChanged
      .listen((ConnectivityResult result) {
          if (result == ConnectivityResult.mobile) //mobile connected.
          else if (result == ConnectivityResult.wifi) //Wifi Connected.  
          else if(result == ConnectivityResult.none) //No network
    });
  }

  @override
  dispose() {
    subscription.cancel();
    super.dispose();
  }
}
```

[visit connectivity package](https://pub.dev/packages/connectivity)

[visit sample gist](https://gist.github.com/erluxman/7e47f12378e79e0168cca7b6eea1c416)

![](assets/93connectivity.gif)

## #94 ⚡️ `superCharged`⚡️

`supercharged` brings awesome utility features from other languages to dart 🎯. making developers life easier.
### 1. Add Dependency

```yml
dependencies:
  supercharged: ^1.6.0
```  

### 2. Have fun 🎉

```dart
"#ff00ff".toColor();
"red".toColor();
"flutter is cool".allBefore(" is"); // "flutter"
12.between(0, 30); // true
[1, 2, 3].elementAtOrNull(4); // Don't throw, return null
[1, 2, 3].elementAtOrElse(4, () => 0); //Don't throw, return default value
//Create Pages from list
["a", "b", "c"].chunked(2, fill: () => ""); // [ ["a", "b"], ["c", ""] ]

var duration = 5.minutes + 30.seconds;
duration += 0.5.hours

100.0.tweenTo(200.0); // Tween(begin: 100.0, end: 200.0)
Colors.red.tweenTo(Colors.blue); // ColorTween(...)

//Easy for loop
["dog", "cat"].forEachIndexed((index, value) {
    print("$i : $value") // 1 : dog, 2 : cat
});
```

[visit supercharged](https://pub.dev/packages/supercharged)

## #95 DefaultTextStyle Widget

We can apply TextStyle to all the widgets in the hirarchy by wrapping it with DefaultTextStyle.

```dart
 DefaultTextStyle(
    child: Column(
      children: <Widget>[
        Text(
          "DefaultTextStyle With Green text color",
          textAlign: TextAlign.center,
          style: TextStyle(fontSize: 20, color: Colors.black),
        ),
        Text("Title"), //Green color, size 30
        Text("SubTitle", style: TextStyle(fontSize: 25)), //Green color, size 25
        Text("Heading", style: TextStyle(fontSize: 20)), //Green color, size 20
      ],
    ),
    style: TextStyle(fontSize: 30, color: Colors.green),
  );
```

[visit sample](https://codepen.io/erluxman/pen/wvMXJKK)

![defaulttextstyle](assets/95defaulttextstyle.png)

## #96 `flutter_cache_manager`

You can use `flutter_cache_manager` to Download **`and / or`** Cache files.

```dart
//Get file from Cache and download if not cached already.
File file = await DefaultCacheManager().getSingleFile(url);

//Download File without caching
File file = await DefaultCacheManager().downloadFile(url);
```

[visit on pub.dev](https://pub.dev/packages/flutter_cache_manager#-readme-tab-)

## #97 Make link on Text clickable using `flutter_linkify`

`flutter_linkify` is a Text Widget that automatically finds the URL link in the string and makes it clickable.

1. Add dependency

```yml
dependencies:
  flutter_linkify: ^version
```

2. Enjoy

```dart
  Linkify(
    text: "My  twitter https://twitter.com/erluxman",
    onOpen: (LinkableElement url) {
      Scaffold.of(context).showSnackBar(
        SnackBar(content: Text("${url.text} clicked")),
      );
    },
  )
```

![linkify](assets/97linkify.gif)
[visit pacakge](https://pub.dev/packages/flutter_linkify#-installing-tab-)

### #98 Package `flutter_spinkit`

We need to show **`loading/progress`** in almost every apps, but `CircularProgressBar` everywhere is boring.

`flutter_spinkit` provides many awesome Progress indictors that we can use.

1. Add dependency

```yml
flutter_spinkit: ^4.1.2+1
```

1. Start Using
   - #### 🔥Type `SpinKit` and press  `Ctrl+SPACE` to see all possible indicators.
   - Give `color (@required)`, `size(optional)` and `duration(optional)` to SpinKit* widgets.

```yml
SpinKitCircle(size: 90, color: Colors.cyan),
SpinKitChasingDots(size: 190, color: Colors.blue),
SpinKitCubeGrid(size: 90, color: Colors.blue),
SpinKitDualRing(size: 90, color: Colors.blue,),
SpinKitFadingCube(size: 90, color: Colors.red),
SpinKitFadingFour(size: 90, color: Colors.green)
```

[visit flutter_spinkit](https://pub.dev/packages/flutter_spinkit#-readme-tab-)

![spinkit](assets/98spinkit.gif)

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
[__`Tips 75-91`__](week13.md)

[__`<< Previous`__](week13.md)
[___`Tips 82-98`___](week14.md)
