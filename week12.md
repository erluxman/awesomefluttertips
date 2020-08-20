# Tips 78-84

## Day 78 Easy navigation

Have you been navigating to different screen like this?

 ❌ Dont do this anymore ❌

    Navigator.of(this).push(
          MaterialPageRoute(builder: (context) => NextScreen()),
        );

   
 ✅ Do this ✅

1. Define a simple extension on `BuildContext`.

        extension NavigationExtension on BuildContext {
          
          navigateTo(Widget destination) {
            Navigator.of(this).push(
              MaterialPageRoute(builder: (context) => destination),
            );
          }
        }
2. 🎉 Celebrate 🎉 🎉

        context.navigateTo( NextScreen());
        context.navigateTo( SeventhScreen());
        context.navigateTo( SettingPage());

## #Day 79 Just import every folders inside assets rather than every files

**It's too much of work 😰🥱 to import every assets like image 🏞, json , audio 🎵into `pubspec.yml`**

**But sadly 😢, you can't import just the `assets` folder.**

**Just import all the folders, it will work 🎉🍾.**

<img src="assets/79assets.png" height ="650">

## #Day 80 Make a class of Resources like R.string, R.svg,R.images, R.flare etc instead of direct asset path

Instead of using raw string, path & URLs, we can organize them in Resource classes.

 __`Group constants, paths and strings by their types`__

    class Strings {
      String appName = "Productive";
      String privacyURL = "https://blabla.com";
    }
    class SVGImages { String homeIcon = "assets/images/home.svg";}
    class LottieFiles { String paperPlane = "assets/lottie/paper_plane.json";}    

__`Organize all resource into one class`__

    class R {
      static Strings strings = Strings();
      static SVGImages svgImages = SVGImages();
      static LottieFiles lottieFiles = LottieFiles();
    }

__`Use resources instead of raw strings and path`__

    // ❌ Don't use raw Strings & Paths ❌
    Text("Productive"),
    Image.asset("assets/images/home.svg"),
    Lottie.asset("assets/lottie/paper_plane.json"),   

    // ✅ Acess String & Pathsfrom Resource ✅
    Text(R.strings.appName),
    Image.asset(R.svgImages.homeIcon),
    Lottie.asset(R.lottieFiles.paperPlane),

## #Day81 use [https://app.quicktype.io/](https://app.quicktype.io/) to generate serializer/deserializer for dart

Convert a `JSON` into `Dart class` with `fromJSON()` and `toJSON()` methods easily with  [quicktype.io](http://quicktype.io) 

Just **paste your JSON** and select `dart` from languages (right-top), you will get the `dart class`.

 try quicktype

[app.quicktype.io](app.quicktype.io)

Alternative:

Or [json to dart](https://javiercbk.github.io/json_to_dart/)

![quicktype](assets/81quicktype.gif)

## #Day82 Loading PDF

You can display PDF easily with `pdf_flutter`

1. Add `pdf_flutter` on pubspec.yml

        dependencies:
          pdf_flutter: ^version

2. On `iOS` enable **PDF preview** like by adding this on ios/Runner/info.plist:

        <key>io.flutter.embedded_views_preview</key>
        <true/>
3. Start Using

        //Load PDF from Network
        PDF.network(
            'https://raw.githubusercontent.com/FlutterInThai/Dart-for-Flutter-Sheet-cheet/master/Dart-for-Flutter-Cheat-Sheet.pdf',
            height: 500,
            width: 300,)
        
        //Load PDF from Assets
        PDF.assets("assets/pdf/demo.pdf",height:400,width:300)
        
        //Load PDF from file
        File fileName;
        PDF.file(fileName,height:400,width:300)

Visit [pdf_flutter](https://github.com/erluxman/pdf_flutter)

<img src="assets/82pdf_flutter.gif" height ="850">

## #Day83 `flutter clean`

An obvious but underappreciated tip:

More than half of the unexpected/strange build errors can be solved by `flutter clean`

The first step towards fixing any build errors in Flutter should be:

    flutter clean 

__`🤡Remember this command, it will save you hours of frustration`__

## #Day 84 Use `Alice` plugin to inspect network requests like chuck

Alice records Http request,payload & response which can be viewed in simple UI (notification or widget). Alice can work with http:http, dart:io/HttpClient, Chopper & Dio.

### Steps

1. Add dependency.
2. Create Alice instance (global is OK)

        Alice _alice = Alice(showNotification: true, showInspectorOnShake: true);

3. Pass  `_alice.getNavigatorKey()` as NavigatorKey of Material/Cupertino App.

        MaterialApp(
            navigatorKey: _alice.getNavigatorKey(),
            child:....
        )

4. Start logging (using http:http for sample)

        import 'package:http/http.dart' as http;

        http
            .post('https://jsonplaceholder.typicode.com/posts', body: body)
            .interceptWithAlice(_alice, body: body);

        http
            .get('https://jsonplaceholder.typicode.com/posts')
            .interceptWithAlice(_alice);

        http
            .put('https://jsonplaceholder.typicode.com/posts/1', body: body)
            .then((response) {
          _alice.onHttpResponse(response, body: body);
        });

5. See the HTTP call details  
  Simply call `_alice.showInspector();`  

    **or**

    `Just shake the phone`

    **to**

    open the **Http call details** screen.

[get alice](https://pub.dev/packages/alice)

<img src="assets/84inspector.gif" height ="650">

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

[__`<< Previous`__](week11.md)
[___`Tips 78-84`___](week12.md)
[__`Next >>`__](week13.md)

[__`Tips 92-98`__](week14.md)
