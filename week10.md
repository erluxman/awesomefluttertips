# Tips 64 - 70

## #Day64 get_it

`get_it` helps you to access :

- Service objects like `RESTClient`, `DB` & their `mocks` from anywhere.
- `(View/UI)Model,BLoCs` etc. from `Widgets`.

**without `BuildContext`.**

### To use `get_it`

1. Add get_it to dependencies

        dependencies:
        get_it: ^4.0.2

2. Provide an object/dependency to get_it

        void main() {
            GetIt.I.registerSingleton(Player.messi());
            runApp(MyApp());
        }

3. Get the dependency from anywhere in app with it's type.

        Player currentPlayer = GetIt.I<Player>();
        print(currentPlayer)  // Player{name: Messi,shirtNumber: 10}

[visit get_it](https://pub.dev/packages/get_it#-readme-tab-)

## #Day65 Setup Linter

Lint helps you to find potential errors, bugs, & code style inconsistancy etc.

__`To setup lint in Flutter :`__

1. Add lint in dev dependencies.

        dev_dependencies:
                lint: ^version

2. Add `analysis_options.yaml` in project root directory.
![lint](assets/65lint.png)

3. Include `package:lint/analysis_options.yaml` inside `analysis_options.yaml` and add your custom rules.

        include: package:lint/analysis_options.yaml

                # Custom Rules
                linter:
                        rules:
                                sort_constructors_first: true
                                prefer_single_quotes: true

4. Done.

### Before Lint

![Before](assets/65lintbefore.png)

### After Lint

![Before](assets/65afterlint.png)

[visit lint package](https://pub.dev/packages/lint)

## #Day66 assert(boolean,messageIfFalse)

If some `conditions` __`must not ever occur`__ on program, we use assert to halt the execution.

Assert condition means that there is no way we can handle exception caused if the condition fails, it must be fixed.

`assert()` statement also help reduce the responsibility of a program as it doesn't need to handle every edge cases.

`assert()` are ignored in release/production.

Some examples :

        updateUser(User user){
                assert(user.id != null) // There is no way to udpate user without id.
                syncUser(user);
        }

        int  getRealSquareRoot(int square){
                assert(square >= 0) //square must be positive to have real root.
                return sqrt(square);
        }

        driveCar(Car car){
                assert(car.hasEngine);
                assert(car.hasFuel);
                assert(car.hasWheels);
                car.drive();
        }

## #Day67 Show build Status badget on Readme

![badge](assets/67cibadge.png)

1. Create `.github/workflows/main.yml` Inside your project's root directory. or Run the command in your **terminal / Powershell** :

        md .github/workflows  && cd "$_" && touch main.yml

2. Put the steps in [this](https://gist.github.com/erluxman/ac4916fedc3b37982181b0a631561d20) file inside `main.yml`
![main.yml](assets/67mainyml.png)

3. Add the build badge on your README.md.

        [![Dart CI]({YOUR_GITHUB_PROJECT_URL}/workflows/Flutter%20CI/badge.svg)]({YOUR_GITHUB_PROJECT_URL}/actions)

4. Commit to Github.

## #Day68 Show code coverage badget on Readme ![codecov](https://codecov.io/gh/erluxman/productive/branch/master/graph/badge.svg)

1. Add the following steps at the end of your Github Actions  main.yml from previous tips.
Find the full `main.yml` file [here](https://github.com/erluxman/productive/blob/master/.github/workflows/main.yml)

       - uses: codecov/codecov-action@v1.0.2
           if: matrix.os == 'ubuntu-latest'
           with:
             token: ${{secrets.CODECOV}} #required
             file: ./coverage/lcov.info #optional 

2. Login/Sign up to [codecov.io](https://codecov.io/)
3. Go to [https://codecov.io/gh](https://codecov.io/gh) > click on your username > search the repo to show codecoverage and select it.
![codecov](assets/68codecov.gif)

4. After that copy the Uplaod token (which should be staring at you at this point/inside setting tab)
5. Go to project's setting(__`not profile setting`__), select "Secrets" from left navigation panel, Add new secret
![github](assets/68gh.gif)

6. Add code Coverage badge to your github repo README file.

        [![codecov](https://codecov.io/gh/USER_NAME/REPO_NAME/branch/master/graph/badge.svg)](https://codecov.io/gh/USER_NAME/REPO_NAME)

7. Git Push and wait for the build to complete, you will have the badges in your github Repo like this:
![result](assets/68result.png)

[See Video](https://www.youtube.com/watch?v=r4NQNSRWgY8)

## #Day69 `factory` constructors

Instead of using `static` methods to `create/return` `new/cached` instance of it's class or it's sub classi.e. __`factory pattern`__, we can use `factory constructors`.

`factory` constructors **behave** like `static methods` but **called** like `normal constructors`. Factory constructors can also be be named & unnamed.

    void main() {
          //❌ static method ❌ 
          var staticUser = User.getUser("John Doe");

          //✅ factory connstructor ✅
          var factoryUser = User("John Doe");
    }
    class User {
          User._(this.name);
          String name;
          
          static Map<String, User> users = {};

          //❌ static method ❌ 
          static User getUser(String name) => users.putIfAbsent(name, () => User._(name));
          
          //✅ factory connstructor ✅
          factory User(String name) =>  users.putIfAbsent(name, () => User._(name));
    }

## #Day70 `AnimatedDefaultTextStyle`

We can animate change in TextStyle with `AnimatedDefaultTextStyle`.

Just give the animation `duration` & the updated `TextStyle`. `AnimatedDefaultTextStyle` will take care of the rest.

        AnimatedDefaultTextStyle(
          duration: Duration(milliseconds: 300),
          child: Text("Flutter"),
          style: newStyle,
        )

[try in codepen](https://codepen.io/erluxman/pen/XWXKBJP)

![animatedtext](assets/70textanim.gif)

[___`Tips 1-7`___](README.md)
[__`Tips 08-14`__](week02.md)
[__`Tips 15-21`__](week03.md)
[__`Tips 22-28`__](week04.md)
[__`Tips 29-35`__](week05.md)
[__`Tips 36-42`__](week06.md)
[__`Tips 43-49`__](week07.md)
[__`Tips 50-56`__](week08.md)
[__`Tips 57-63`__](week09.md)

[__`<< Previous`__](week09.md)
[___`Tips 64-70`___](week10.md)
[__`Next >>`__](week11.md)
[__`Tips 78-84`__](week12.md)

