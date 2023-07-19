# Replace conditional with polymorphism - step by step

- [Using interfaces](#using-interfaces)
- [Using inheritance](#using-inheritance)

## Using interfaces

This is the version using interfaces instead of inheritance.

The finished code can be viewed [here](https://github.com/claresudbery/Parrot-Refactoring-Kata/blob/polymorphism-no-inheritance/CSharp/Parrot/Parrot.cs).

- General useful shortcuts:
    - Cmd + Shift + R brings up refactoring menu
        - below I'll just use the shorthand [R] to mean `Cmd + Shift + R`
    - Option/Alt + Enter to bring up lightbulb menu ("intention actions")
        - below I'll just use the shorthand [AE]
- Extract interface
    - Place cursor in name of class
    - [R] => Extract interface
    - Just select `GetSpeed` and `GetCry` for methods
- Move interface to its own file
    - Place cursor in name of interface
    - [AE] => Move to IParrot.cs
- Replace constructor with factory method
    - Place cursor in name of constructor
    - [AE] => To factory method
- Change `CreateInstance` to return `IParrot` instead of `Parrot`
- Remove redundant cast expressions in `ParrotTest.cs` - all at once
    - put cursor in one of the greyed out enum type casts
    - [AE] => right arrow => Remove redundant cast expressions in file
- Change access modifier of constructor
    - Place cursor in access modifier (ie "private")
    - [AE] => To public
        - at this point you'll get a green squiggly - because it's not being accessed by anything yet, so the IDE doesn't think it needs to be public
- Create new parrot class:
    - Create `EuropeanParrot` class
        - Add a switch statement to `CreateInstance` where you switch on `type`
        - add a case for `ParrotTypeEnum.EUROPEAN`
        - type `return new EuropeanParrot();` in the case
        - Give it the same four params as the enclosing method
            - start typing `type` inside brackets and it will give you option to select and auto-complete
            - You're not passing hard-coded values here!
                - Just passing on the data that's already been given to you in your own constructor
            - keep adding commas after each one and it will keep giving you options to select and auto-complete
        - place cursor in name of non-existent class (highlighted in red)
        - [AE] => Create type
        - [AE] => Implement missing members
            - Accept default: Will select both `GetSpeed` and `GetCry` for methods
    - Add `_parrot` member var
        - Remove exception in constructor
        - Type `_parrot = new Parrot()` at top of constructor
        - Place cursor in brackets
            - start typing `type` inside brackets and it will give you option to select and auto-complete
            - keep adding commas after each one and it will keep giving you options to select and auto-complete for each arg
        - Place cursor in `_parrot`
        - [AE] => Create field
    - Implement interrim version of `GetSpeed`
        - Remove exception
        - return `_parrot.GetSpeed();`
    - Implement interrim version of `GetCry`
        - Remove exception
        - return `_parrot.GetCry();`
    - Implement unique version of `GetSpeed`
        - copy code from `Parrot.GetSpeed` for relevant case
        - Prefix call to `GetBaseSpeed` with `Parrot.`
        - This will give you a red squiggly. Use the hints to do the following:
        - Place cursor in method name
        - [AE] => Make public
        - [AE] => Make static
    - Get rid of unnecessary case in `Parrot` version of `GetSpeed`
    - Move class to its own file
        - Place cursor in name of class
        - [AE] => Move to EuropeanParrot.cs
    - Implement unique version of `GetCry`
        - return code from `Parrot.GetCry` for relevant case
        - Remove relevant case from switch statement in `Parrot` version of `GetCry`
    - Remove unnecessary `_parrot` member var
        - delete initialisation in constructor
        - put cursor in var declaration
        - [AE] => Remove unused var
    - Remove constructor params not needed
        - you can tell cos they're greyed out
        - put cursor in param declaration
        - [R] => Safe Delete
    - Remove redundant constructor in `EuropeanParrot` class
        - put cursor in constructor name
        - [AE] => Remove redundant constructor
- Do the same for `AfricanParrot` and finally `NorwegianBlueParrot`
    - Follow same steps as above
    - Some stuff will already be done, eg access modifiers of `GetBaseSpeed`
    - Some `Parrot` methods will still need making public and static
        - Place cursor in method calls
        - [AE] => Make public
        - [AE] => Make static
    - When it comes to `Parrot` member vars, turn them into local member vars:
        - These vars will also be passed into your sub-class constructor
        - Place cursor in name of relevant constructor param in sub-class
        - [R] => Introduce field
    - For `NorwegianBlueParrot` making the method public won't work instantly using shortcut cos it can't tell you mean the overloaded version of `GetBaseSpeed`
        - So go to declaration in base class
        - Place cursor in `private`
        - [AE] => Make public
        - Go back to the call in the sub-class
        - Cursor in method name
        - [AE] => Make static
    - You won't be deleting the constructor as you did with `EuropeanParrot`, because it is actually needed
- Move `GetLoadFactor` from `Parrot` class to `AfricanParrot`
    - put cursor in name of method
    - [R] => Move to another type
    - select `AfricanParrot` only
- Make `GetLoadFactor` private in `AfricanParrot`
    - put cursor in `protected`
    - [AE] => make method private
- Move overloaded `GetBaseSpeed` (with param) from `Parrot` class to `NorwegianBlueParrot`
    - put cursor in name of method
    - [R] => Move to another type
    - select `NorwegianBlueParrot` only
- Make `GetBaseSpeed` private in `NorwegianBlueParrot`
    - put cursor in `protected`
    - [AE] => make method private
- Remove member vars not needed in `Parrot` class
    - you can tell cos it's greyed out
    - put cursor in var declaration
    - [R] => Safe Delete
- Remove constructor params not needed in `Parrot` class
    - you can tell cos they're greyed out
    - put cursor in param declaration
    - [R] => Safe Delete
- Add default case to switch statement in `CreateInstance`
    - `default: throw new ArgumentException($"Invalid type: {type}");`
    - Remove final return statement
        - [AE] => Remove unreachable code
- Stop `Parrot` from implementing `IParrot`
    - just delete `: IParrot` in class declarat
- Get rid of unused `GetSpeed` and `GetCry` methods in `Parrot` class
    - Place cursor in method name
    - [AE] => Remove unused method
- Remove `_type` member var not needed in `Parrot` class
    - you can tell cos it's greyed out
    - put cursor in var declaration
    - [R] => Safe Delete
- Remove `_type` constructor param not needed in `Parrot` class
    - you can tell cos it's greyed out
    - put cursor in param declaration
    - [R] => Safe Delete
- Remove unused `Parrot` constructor
    - put cursor in constructor name
    - [R] => Safe Delete
- Make `Parrot` class static
    - put cursor in class name
    - [AE] => Make static

## Using inheritance

This is the version using inheritance instead of interfaces.

See also [this video](https://vimeo.com/801311948/41a83a3c4e) and [this version of the finished code](https://github.com/claresudbery/Parrot-Refactoring-Kata/blob/LH-demo/CSharp/Parrot/Parrot.cs).

Using Resharper:

- Replace constructor with factory method
    - Place cursor in name of constructor
    - Alt Enter => To factory method
- Change access modifier of constructor
    - Place cursor in access modifier (ie "public")
    - Alt Enter => To protected
- Create class
    - type `return new MyClassName();`
    - place cursor in name of class
    - Alt Enter => Create type
- Change access modifier of GetBaseSpeed
    - Place cursor in access modifier (ie "private")
    - Alt Enter => To protected
- Change Signature of GetSpeed
    - Place cursor in function name
    - Alt Enter => To virtual
- Override method
    - type the word override and then a space
    - as long as there is something you can override, you will be given suggestions
