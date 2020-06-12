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

1. Inside your project's root directory, run the command in your terminal / Powershell :

        md .github/workflows  && cd "$_" && touch main.yml

2. Put the steps in [this](https://gist.github.com/erluxman/ac4916fedc3b37982181b0a631561d20) file inside `main.yml`
![main.yml](assets/67mainyml.png)

3. Add the build badge on your README.md.

        [![Dart CI]({githubProjectURL}/workflows/Flutter%20CI/badge.svg)]({githubProjectURL}/actions)

4. Commit to Github.
