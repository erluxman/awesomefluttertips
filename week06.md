## #Day36 Implicit Interface of class
Did you know you can extend and implement a class in Dart? 

* No need to create `IInterface` to mock a `class`.
* No need to extract `IInterface` as Contract / Protocal

Every class implicitly defines an interface containing all the instance variables, methods getter and setters.

1. extends ->  must override abstract methods, other methods and variables override optional. i.e can inherit parent's behavior.
2. implements -> Every methdos and variables must be overriden. i.e. can't inherit parent behavior
   
                Dart has implicit Interface of every class          

        class A {
            //Optional @override for 'extends' &&  must for 'implements'. 
            var name;
            //Optional @override for 'extends' &&  must for 'implements'.     
            void normalMethod() => print("B -> Normal Method");
        }

        abstract class B{
            //must @override in both 'extends' and 'implements'.
            void abstractMethod();
        }

        //Non abstract 
        class C extends A {} // ✅
        class C implements A {} //❌ Must override name & normalMethod()   
        class C extends B {} //❌ Needs to override `abstractMethod()`
        class C implements B {} //❌ Needs to override `abstractMethod()`

        //Abstract Child
        abstract class C extends A {}  // ✅
        abstract class C implements A {} // ✅
        abstract class C implements B {} // ✅ 
        abstract class C extends B {} // ✅ 



## #Day37 Animated Switcher

Use `Animated Switcher` for smooth transition when a widget is switched with another.

**Provide:**

1. `duration` of transition

2. dynamic `child` &

3. `TransitionBuilder` like `Fade,Scale,Rotation`

Then, Flutter will handle the rest.

        AnimatedSwitcher(
            
            duration: Duration(milliseconds: 800),

            child: shouldShowCard ? CreditCardFront() : CreditCardBack(),

            transitionBuilder: (child, animation) {
                print("Animation asked ${widget.runtimeType}");
                return FadeTransition(
                    child: child,
                    opacity: animation,
                );
            },
          )
[try in codepen](https://codepen.io/erluxman/pen/xxwJRBQ)

![](assets/37animatedswitcher.gif)

## #Day38 GestureDetector widget

Use Gesture Detector to detect gestures like tap, double Tap, press, LongPress, pan, drag, zoom etc.

All those callbacks behave like `onClick(){}` on Button.


    GestureDetector(
        onTap: //Tapped
        onDoubleTap: //"Double Tapped
        onLongPress: //Long Press
        onLongPressEnd: //Long Press ends
        onPanStart: // Pan Started
        onPanUpdate: //"Pan" + paninfo.delta
        onPanEnd: //Pan Ended
        onHorizontalDragStart: //"Drag" + draginfo
        child: Padding(
            padding: const EdgeInsets.all(48.0),
            child: InkWell(
            child: Card(
                child: Center(
                    child: Text(
                    currentGesture.toUpperCase(),
                    style: TextStyle(fontSize: 20, 
                        fontWeight: FontWeight.w700),
                    ),
                ),
            ),
            ),
        ),
    );

[try on codepen]
(https://codepen.io/erluxman/pen/wvKxVrE)

![](assets/38gesture.gif)

## #Day39 Package Animated Text Kit
animated_text_kit provides some cool ways to animate text appearences. 

1. Use built in Widget like 
            
        RotateAnimatedTextKit(), TextLiquidFill(), ColorizeAnimatedTextKit() etc.

2. & Pass a list of text in constructor
   
       TyperAnimatedTextKit( 
           text: ["Colorize","Animated", "TextKit",])

3. Do additional customization if you want. To do that Look into constructor of each Widgets provided.

[sample code](https://gist.github.com/erluxman/821568539592f9ac798172dfffa14540)

[animated_text_kit package](https://pub.dev/packages/animated_text_kit#-installing-tab-)

![](assets/39animatetext.gif)


## #Day40  5 Steps of AnimatedIcon.

We can use AnimatedIcon in 5 simple steps. 

1. Define a Stateful Widget whose state mixins with SingleTickerProviderStateMixin.
2. Define an AnimationController inside state with animation duration and pass this into vsync.
3. Define a variable that stores wheather animation is at start or end.
4. Provide the controller  to AnimatedIcon.
5. Animate  icon by calling `.forward()` or `.reverse()` on AnimationController based on the current state of icon.

[play on codepen](https://codepen.io/erluxman/pen/PoPyNrM)

![](assets/40animatedicon.gif)


## #Day41 Path Provider( `path_provider package`) (common file locations in iOS and Android)

Sometimes we want to get the location of Various common directories like:
### **Download, Cache, Documents, External Storage, External Cache** etc.

The package `path_provider` is build for exact same reason so that we do not have to deal with Platform specific issues by our own. 


1. Add path_provider to pubspect.
   `path_provider: ^verison`
2. Use it

        //Gives download directory
        Directory tempDir = await getTemporaryDirectory();

        //Gives documents directory
        Directory docDir = await getApplicationDocumentsDirectory();

        //Gives external Storages
        List<Directory> externalStorages = await getExternalStorageDirectories();

        //Gives download directory
        Directory downloadDir = await getDownloadsDirectory();

[Download `path_provider`](https://pub.dev/packages/path_provider#-readme-tab-)

## #Day42 Flutter ShapeBorder

We can use ShapeBorder to give outline to widgets or Clip them on it's shape. There are my ShapeBorder like `Border, ContinuousRectangleBorder, StadiumBorder, CircleBorder, BeveledRectangleBorder` etc.

1. Use ShapeBorder to give a Widget outline.
   
        Container(
            decoration: ShapeDecoration(
                color: Colors.white,
                shape: // Any shape border
            ),
        )
2. Use ShapeBorder to clip a Widget.
   
        ClipPath(
            clipper: ShapeBorderClipper(
                shape: // Any shape border
            ),
            child: // Any Child to be clipped
        )

[try in codepen](https://codepen.io/erluxman/pen/vYNQLPx)

![](assets/41shapeborder1.png)
![](assets/41shapeborder2.png)


[___`Tips 1-7`___](README.md)
[__`Tips 08-14`__](week02.md)
[__`Tips 15-21`__](week03.md)
[__`Tips 22-28`__](week04.md)
[__`Tips 29-35`__](week05.md)


[__`<< Previous`__](week05.md)
[___`Tips 36-42`___](week06.md)
[__`Next >>`__](week07.md)


[__`Tips 43-49`__](week07.md)
[__`Tips 50-56`__](week08.md)
[__`Tips 57-63`__](week09.md)