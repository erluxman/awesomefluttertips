# Tips 29-35

## #Day29 Wrap widget

When you are making responsive UIs, you need to wrap contents dynamically.

Wrap comes to the rescue. Wrap is like Column/Row but wraps it's children to next row or column.

Use Wrap like you use Column or Row just give it's direction (either vertical or horizontal)

    Wrap(
        direction: Axis.vertical/Axis.horizontal,
        children: [Widgets],
        runAlignment: WrapAlignment.start,
        spacing: 20, //space between previous and next item
        runSpacing: 20, //space between new row or column
        );
[try in codepen](https://codepen.io/erluxman/pen/YzyENpR)
![wrap](assets/29wrap.gif)

## #Day30 Blur a Widget in Flutter

To blur a widget, put it below a BackdropFilter widget in stack.

1. Adjust Gussian blur level with sigmaX, and sigmaY.
2. Must provide child to Backdrop it needs a layer to act as blur.

        Stack(
            fit: StackFit.loose,
            children: <Widget>[
            FlutterLogo(size: 300),
            Positioned.fill(
                child: BackdropFilter(
                filter: ImageFilter.blur(sigmaX: 5, sigmaY: 5),
                child: Container(
                    color: Colors.transparent,
                ),),
            ],
        )

You will a blur like this.
[play in codepen](https://codepen.io/erluxman/pen/xxwPJrY)
![blur](assets/30blur.png)

## #Day31 Changing Theme Dynamically

Theme of the application is nothing but argument in MaterialApp or CupertinoApp.

Just create a StreamController of bool to represent it's theme.

With the use of StreamBuilder, set the theme of inside Material/Cupertino App and boom 🚀 your app will be able to change it's theme dynamically.

    //Define a Inherited Widget
    class SettingsStore extends InheritedWidget {
        final ValueNotifier<ThemeData> theme = ValueNotifier(ThemeData.light());

        SettingsStore({@required Widget child}) : super(child: child);

        static SettingsStore of(BuildContext context) =>
        context.dependOnInheritedWidgetOfExactType<SettingsStore>();
    
        void updateTheme(ThemeData theme) => this.theme.value = theme;

        @override
        bool updateShouldNotify(SettingsStore oldWidget) => oldWidget.theme != this.theme;
    }


    //Listen to it
    class App extends StatelessWidget {
        @override
        Widget build(BuildContext context) {
            return ValueListenableBuilder(
                valueListenable: SettingsStore.of(context).theme,
                builder: (context, theme, child) => MaterialApp(
                theme: theme,
                home: SettingsView(),),
            );
        }
    }



    //Change the theme from any build method.
    SettingsStore.of(context).updateTheme(ThemeData.light())
Credit: [u/Kounex's](https://www.reddit.com/user/Kounex/)

[try on dartpad](https://dartpad.dartlang.org/ccac4c4dff07d69deb6fcacbdeebaa3c)

![dynamicTheme](assets/32dynamictheme.gif)

## #Day32 Dart Extension

We can extend functionality to existing class/API/Library without inheriting it to a child class.

Extensions can have method, getter and setter.

Here we add function to DateTime class without subclassing it.

Define extension like this :

    extension DateExtensions on DateTime{
        
        printYYYYMMdd(String seperator) {
            var dateString = "${this.year}$seperator${getTwoDigit(this.month)}$seperator${getTwoDigit(this.day)}";
            print(dateString);
        }
        
        String getTwoDigit(int number){
            return (number < 10)? "0$number" :number.toString();
        }
        
        DateTime get  nextYear => this.add(Duration(days:365));
        
        DateTime previousYear() => this.subtract(Duration(days:365));
    }

Then Just Call those extensions

    void main() {
        var now = DateTime.now();
        var nextYear = now.nextYear;
        var lastYear = now.previousYear();

        now.printYYYYMMdd("-");
        nextYear.printYYYYMMdd("/");
        previousYear.printYYYYMMdd(".");
    }

[try on dartpad](https://dartpad.dartlang.org/45e30e5208b39123053f2408624d641c)

## #Day33 ToastBadge (toast_badge) package

If you want to show notification that auto dismisses anywhere in the screen, use `toast_badge`.

Just wrap any widget with `ToastBadget` or call `.enableBadge()` on any widget, you will be able to show notification on that widget without the need of BuildContext object.

i.e. You use it like toast but in the place you desire.

1. Wrap

        child: ToastBadge( child: SettingPage(),),


        //OR 

        child: SettingPage().enableBadge(),

2. Call

        ToastBadge.show("Hello Toast");


        //With more options

        ToastBadge.show("Hello Toast",  
        mode: ToastMode.INFO, 
        duration: Duration(milliseconds: 500));

[use this package](https://github.com/erluxman/toast_badge)

![toast](assets/33toastbadge.gif)

## #Day34 Making Reorderable list

Create ReorderableListView just like normal ListView.

1. Give Key to each child
2. Handle onReorder: (oldIndex, newIndex)

        ReorderableListView(
              onReorder: (oldIndex, newIndex) {
                setState(() {
                  if (oldIndex < newIndex) {
                    newIndex -= 1;
                  }
                  var previous = names.removeAt(oldIndex);
                  names.insert(newIndex, previous);
                });
              },
              children:[
                child(key:ObjectKey(item)),.....
              ]
        )

[try in codepen](https://codepen.io/erluxman/pen/Yzyabpz)

![reorderable](assets/34reorderable.gif)

## #Day35 Dart Dev tools

Dart dev tool is powerful set of debugging and performance tools like Layout Inspector,Timeline, Memory, App Performance,Debugger,Logging & Network monitor.

Android Stidio : You can open it by clicking dart icon on Run tab when app is runnin in Anadroid Studio

VSCode: typing Open Dev Tools in command Pallet.

Learining to use Dart Dev tool  is very 🚨important skill🚨 to have as a Flutter/dart developer.

![Opening in Android Studio](assets/35as.png)
_Opening in Android Stuido_

![vscode](assets/35vscode.png)
_Opening in VSCode_

![as](assets/35devtools.png)
_Dev tools page_

[See amazing dart dev tool gifs](https://www.google.com/search?q=dart+devtools+gif&tbm=isch&rlz=1C5CHFA_enNP896NP896&hl=en&ved=2ahUKEwjG5J75pqjpAhW8A7cAHTFmCdYQBXoECAEQKA&biw=1920&bih=1066)

[___`Tips 1-7`___](README.md)
[__`Tips 08-14`__](week02.md)
[__`Tips 15-21`__](week03.md)
[__`Tips 22-28`__](week04.md)

[__`<< Previous`__](week04.md)
[___`Tips 29-35`___](week05.md)
[__`Next >>`__](week06.md)

[__`Tips 36-42`__](week06.md)
[__`Tips 43-49`__](week07.md)
[__`Tips 50-56`__](week08.md)
[__`Tips 57-63`__](week09.md)
[__`Tips 64-70`__](week10.md)
[__`Tips 71-77`__](week11.md)
