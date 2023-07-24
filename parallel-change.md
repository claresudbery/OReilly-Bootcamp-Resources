# Table of contents

- [Finding the code](#finding-the-code)
- [Lab Exercise 1](#lab-exercise-1)
- [Lab Exercise 2](#lab-exercise-2)
  - [Step by step C# demo instructions](#step-by-step-c-demo-instructions)

# Finding the code

- [Raw code is here (racing car katas)](https://github.com/emilybache/Racing-Car-Katas)
  - Visit the above url to fork (top right), then clone the code

# Lab Exercise 1

- The Tennis demo code is [here](https://github.com/claresudbery/Tennis-Refactoring-Kata/blob/feature-flags-demo-finished/csharp/Tennis/TennisGame2.cs)
- ...but you will be working with the [racing car katas](https://github.com/emilybache/Racing-Car-Katas)
- Your task is to use parallel change to create `Alarm.Check(bool setAlarm)`
- You have some choices:
  1. Use your code from the earlier [dependency injection exercise](/dependency-injection.md)
  2. Add a call to `alarm.Check` in an existing test (eg Foo)
     - It will pass or fail randomly if you don't have dependency injection yet, but that's not the point of this exercise so can be ignored
     - If you have made no changes to tests yet:
       - Rename the Foo test to AlarmIsSetWhenPressureLow
       - Change Assert.False to Assert.True
       - If you run it repeatedly, the test will pass or fail randomly
  3. Start with the [C# dependency-injection-demo branch](https://github.com/claresudbery/Racing-Car-Katas/blob/dependency-injection-demo):
     - `mkdir racing-car2`
     - `cd racing-car2`
     - `git clone https://github.com/claresudbery/Racing-Car-Katas.git`
     - `cd Racing-Car-Katas`
     - `git checkout dependency-injection-demo`
- Your job is to create a version of `Alarm.Check` with a `setAlarm` flag 
    - add a test that expects alarms not to be set when the flag is set to false
    - create a duplicate method with a flag
    - then gradually change the clients to use the version with the flag
    - and finally get rid of the old version
- If you finish the above exercise, replace `Check(bool setAlarm)` with two methods: `CheckAndSetAlarm` and `CheckWithNoAlarm`
  - Keep the code compiling and tests passing at each tiny change 

# Lab Exercise 2

- Code from the coding demo can be seen [here](https://github.com/claresudbery/Racing-Car-Katas/blob/parallel-change-demo)
- Your task is still the same as in [exercise 1](#lab-exercise-1)
- There are two parts to this exercise (if you have time): First duplicate method with flag, then create two new methods
  
## Step by step C# demo instructions

- Replace `Alarm.Check()` with `Alarm.Check(bool setAlarm)`:
    - Make a new version of `Alarm.Check` that takes a flag: `bool setAlarm`
    - Add a new test: `AlarmNotSet_WhenFlagFalse_ForLowPressure`
        - can be a copy of existing low pressure test
        - Pass false through to Check method (means you'll be calling the new method)
        - Change assertion to expect False instead of true
    - Run test - will fail initially
    - Make test pass
        - Update the new version of Alarm.Check to act on the flag
    - Change other clients
        - In other tests, pass true to method
        - Check tests pass
    - Remove original version of `Alarm.Check()`
        - Check tests pass
- Note: There is an alternative way of doing the parallel change, which is to give a default value
    - Not possible in all languages
    - Can be done like this: Make `Alarm.Check` take a flag: `setAlarm`:
        - Add `bool setAlarm = true`
        - Add a new test: `AlarmNotSet_WhenFlagFalse_ForLowPressure`
            - can be a copy of existing low pressure test
            - Pass false through to `Check` method
            - Change assertion to expect False instead of true
        - Run test - will fail initially
        - Make test pass
            - Update `Alarm.Check` to act on the new flag
        - Change other clients
            - In other tests, pass true to the `Check` method
            - Check tests pass
        - Remove default value in `Check` method
            - Check tests pass
- The main kind of parallel change (where you temporarily have 2 duplicate methods) is also used for "Remove flag argument" refactoring:
    - Create new method: `public void CheckAndSetAlarm()`
        - It will just call `Check(true);`
    - Create new method: `public void CheckWithNoAlarm()`
        - It will just call `Check(false);`
    - Run tests - should still pass
    - Gradually replace calls in AlarmTest.cs to use the two new methods
        - Keep running tests after each change
    - Finally make original method private
        - Run tests!
    - This is parallel change because both versions existed side by side for a while
        - In more straightforward examples, you wouldn't even keep a private method
        - With a straightforward if statement and two code branches, can just move each branch to new method
        - But this example is still helpful because client code is easier to read, and the two public methods effectively document what the flag does in the private method
