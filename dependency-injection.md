# Table of contents

- [Finding the code](finding-the-code)
- [Lab Exercise 1](lab-exercise-1)
- [Lab Exercise 2](lab-exercise-2)
  - [Step by step C# demo instructions](step-by-step-c-demo-instructions)

# Finding the code

- [Raw code is here (racing car katas)](https://github.com/emilybache/Racing-Car-Katas)
  - Visit the above url to fork (top right), then clone the code

# Lab Exercise 1

- Write tests for the “tire pressure monitoring system” without changing the production code.
  - Code is in [Alarm class](https://github.com/emilybache/Racing-Car-Katas/blob/main/CSharp/TirePressureMonitoringSystem/Alarm.cs)
  - Tests are in [AlarmTest class](https://github.com/emilybache/Racing-Car-Katas/blob/main/CSharp/TirePressureMonitoringSystem.Tests/AlarmTest.cs)
  - Examples of tests you might want to add:
    - `Alarm_IsOff_ByDefault`
    - `Alarm_GoesOn_WhenPressureValue_LessThanLowPressureThreshold`
    - `Alarm_GoesOn_WhenPressureValue_HigherThanHighPressureThreshold`
    - `Alarm_StaysOff_WhenPressureValue_BetweenPressureThresholds`
   
# Lab Exercise 2

- This time you can change the production code! Use dependency injection to make the existing code more testable.
- Examples of tests you might want to add:
  - `Alarm_IsOff_ByDefault`
  - `Alarm_GoesOn_WhenPressureValue_LessThanLowPressureThreshold`
  - `Alarm_GoesOn_WhenPressureValue_HigherThanHighPressureThreshold`
  - `Alarm_StaysOff_WhenPressureValue_BetweenPressureThresholds`
- Code from the coding demo can be seen [here](https://github.com/claresudbery/Racing-Car-Katas/blob/dependency-injection-demo)

## Step by step C# demo instructions

- We're going to inject the sensor dependency, so that we can stub it for test purposes
- Create ISensor interface
    - go to Sensor class and extract interface
    - Include `PopNextPressurePsiValue`
- Change Alarm _sensor member var to ISensor: 
    - Put cursor in type, get refactoring menu up (Cmd + Shift + R)
    - Use base type where possible => select ISensor
- Create two parallel constructors
    - One will initialise _sensor member var by newing up Sensor(), one will get sensor injected:
    - First constructor: Initialise `_sensor` in default constructor
        - Use `ctor` to create constructor
        - Copy `_sensor = new Sensor();` into constructor
        - Orange squiggly => Remove field initialiser
    - Second constructor: Initialise `_sensor` from constructor param
        - Comment out first constructor
        - Will give you orange squiggly under `_sensor` member var
        - Alt + Enter => initialise field from constructor
    - Uncomment first constructor
- Create new `StubSensor `class (in test folder) 
    - pass `stubSensor` object into constructor in test
    - Alt + Enter => Create local variable
    - start typing `= new` and autocomplete to `Sensor()`
    - Change Sensor() => StubSensor()
    - Alt + Enter => Create new type
    - Alt + Enter => Implement missing members
- Give `StubSensor` a public property `NextPressurePsiValue` and return from `PopNextPressurePsiValue`
    - add `return NextPressurePsiValue;` to the body of `PopNextPressurePsiValue`
    - Alt + Enter => Create property
    - It will automatically give you `{ get; set; }` which is what you want
- In tests, pass new `StubSensor` to `Alarm` then use tools to create new stuff
    - Rename Foo => Alarm_IsOff_ByDefault
        - Don't actually need to pass `stubSensor` in here - can just use `new Sensor()`
        - Add Arrange / Act / Assert
    - Add a new test - `Alarm_GoesOn_WhenPressureValue_LessThanLowPressureThreshold`
        - copy the other one
        - pass `stubSensor` into Alarm constructor
        - when initialising `stubSensor`, replace `()` with `{}` 
            - ...and initialise `NextPressurePsiValue` to `Alarm.LowPressureThreshold - 1`
            - make `Alarm.LowPressureThreshold` public (can stay const)
        - the constructor moves into `// Arrange` section
        - In `// Act`, call `alarm.Check();`
        - Change the assert from false to true
- Get rid of default constructor





