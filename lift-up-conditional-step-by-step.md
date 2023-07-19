# Lift up Conditional: Step by step

- The code base is here:
  - [Vanilla code base](https://github.com/emilybache/GildedRose-Refactoring-Kata)
  - [at the state it's in at the start of the demo](https://github.com/claresudbery/GildedRose-Refactoring-Kata/blob/csharp-liftup-start/csharp/GildedRose.cs)
  - [at the state it's in at the end of the demo](https://github.com/claresudbery/GildedRose-Refactoring-Kata/blob/csharp-liftup-demo/csharp/GildedRose.cs)

# Table of Contents

- [Step by step: Simple refactor instructions](#step-by-step-simple-refactor-instructions)
- [Step by step: My detailed recreation of the refactor](#step-by-step-my-detailed-recreation-of-the-refactor)

# Step by step: Simple refactor instructions

More detailed version [below](#step-by-step-my-detailed-recreation-of-the-refactor). 

This version has simpler instructions, and a gap in the middle where I skip to the end.

- create a local `item` var
- pull the whole body of the for loop into its own method - `DoUpdateQuality`
  - Ctrl + M + M to collapse regions (Ctrl + M + M again to expand), Shift up/down to select code
- Extract the first expression in the if statement - `Items[i].Name != "Aged Brie"` into a variable `isNotAgedBrie`
- Invert boolean to be positive statement rather than negative: `isAgedBrie`
- take the entire contents of the extracted method and extract into yet another method called `DoEverythingElse`
- Duplicate call to extracted method in an if...else block
  - Duplicate call first
  - Ctrl + K, S
- inline all the code in `DoEverythingElse`
- replace first always-false expression with false
- remove unreachable code
- replace always-false backstage-pass expression (`item.Name == "Backstage passes to a TAFKAL80ETC concert"`) with false
- remove unreachable code
- replace next always-false expression (`!isAgedBrie`) with false
- remove unreachable code and redundant braces
- WE NOW HAVE A FULL BLOCK OF CODE UNDER `if (isAgedBrie)`
- Remove always-true expression `!isAgedBrie`
- Get rid of always-true `!isAgedBrie` and invert if
- remove unreachable code and redundant braces
- Inline `isAgedBrie` variable
- NEW CASE: Create var for `isBackstagePass`
- Extract method: `DoEverythingElse`
- Duplicate call to `DoEverythingElse` in an if...else for backstage passes
- inline all the code in `DoEverythingElse`
- remove unreachable code
  
... Fast forward to the end (see [detailed instructions](#step-by-step-my-detailed-recreation-of-the-refactor) for the middle bit)

- NEW CASE FOR SULFURAS
- Create new `isSulfuras` variable
- Extract `DoEverythingElse` and call in both branches of Sulfuras if statement
- Inline `DoEverythingElse`
- Remove three chunks of unreachable code
- Remove empty if statements
  - Manually delete!
- Simplify three always-true if statements
- Inline `isSulfuras`
  - Ctrl + R, I
- Convert if statement to switch statement
  - Put cursor in very top `if` statement
  - Alt + Enter => Convert to switch statement

# Step by step: My detailed recreation of the refactor

(simpler version [above](#step-by-step-simple-refactor-instructions))

- turn off ncrunch
- turn on autosave
- create a local `item` var to make it easier to extract methods
  - Ctrl + R, V
  - TESTS STILL PASS
- pull the whole body of the for loop into its own method - `DoUpdateQuality`
  - Ctrl + M + M to collapse regions (Ctrl + M + M again to expand), Shift up/down to select code 
  - Ctrl + R, M => extract method => DoUpdateQuality
  - TESTS STILL PASS
- inline the local var just before the call to the extracted method, to make it neater
  - Ctrl + R, I
  - TESTS STILL PASS
- Extract the first expression in the if statement - `Items[i].Name != "Aged Brie"` into a variable `isNotAgedBrie`
  - Ctrl + R, V
  - TESTS STILL PASS
- Invert boolean to be positive statement rather than negative
  - Ctrl + Shift + R - Invert boolean
  - Tick both boxes and RENAME to `isAgedBrie`
  - TESTS STILL PASS
- take the entire contents of the extracted method and extract into yet another method called `DoEverythingElse`
  - Shift + down
  - Ctrl + R, M => extract method (two vars will be passed in - that's fine)
  - TESTS STILL PASS
- Duplicate call to extracted method in an if...else block
  - select the call to the method: Ctrl + K, S => `if` => leave the condition as `true` (to keep tests green)
  - type `e` => press Enter to get autocomplete for `else` block
  - duplicate the first line of code calling the method 
    - Ctrl + C / V without selection will duplicate whole line of code
    - paste into else block
  - change `true` to `isAgedBrie` (just start typing and it will autocomplete)
  - TESTS STILL PASS
- inline all the code in `DoEverythingElse`
  - Ctrl + R, I => Alt + A (inline all usages) => Enter
- use the coverage tool to find dead code
  - for dotCover:
    - Resharper => unit test explorer
    - right-click the tests you're interested in
    - click cover tests
    - now look at the code and you'll see little horizontal rectangles on the left
- replace first always-false expression with false
  - Alt + Enter => Replace expression with false
- remove unreachable code
  - Alt + Enter => Remove unreachable code
- Remove redundant braces
  - Alt + Enter => Remove braces
- replace always-false backstage-pass expression (`item.Name == "Backstage passes to a TAFKAL80ETC concert"`) with false
  - just select expression and type over with false
- remove unreachable code
  - Alt + Enter => Remove unreachable code
- replace next always-false expression (`!isAgedBrie`) with false
  - Alt + Enter => Replace expression with false
- remove unreachable code and redundant braces
  - Alt + Enter => Remove unreachable code
  - Alt + Enter => Remove braces
- WE NOW HAVE A FULL BLOCK OF CODE UNDER `if (isAgedBrie)`
  - Time to handle the `else` clause
- Remove always-true expression `!isAgedBrie`
  - Alt + Enter => Remove expression
- Get rid of always-true `!isAgedBrie`
  - Alt + Enter => Replace expression with true
  - Place cursor inside `if`
  - Alt + Enter => Invert if
- remove unreachable code and redundant braces
  - Alt + Enter => Remove unreachable code
  - Alt + Enter => Remove braces
- Inline `isAgedBrie` variable
  - Ctrl + R, I
- NEW CASE: Create var for `isBackstagePass`
  - Select `item.Name != "Backstage passes to a TAFKAL80ETC concert"`
  - Ctrl + R, V => isNotBackstagePass
  - Select => Ctrl + Shift + R, invert boolean => `isBackstagePass`
- Extract method: `DoEverythingElse`
  - Shift + down
  - Ctrl + R, M => extract method => `DoEverythingElse`
- Duplicate call to `DoEverythingElse` in an if...else for backstage passes
  - duplicate the line of code calling the method
  - select the first one: Ctrl + K, S => `if` => `isAgedBrie` (just start typing and it will autocomplete)
  - select the second one: Ctrl + K, S => `else`
- inline all the code in `DoEverythingElse`
  - Ctrl + R, I => inline all usages
- use the coverage tool to find dead code
- Remove code under always-false if statement
  - Alt + Enter => Replace if statement with respective branch
- And again: Remove code under always-false if statement
  - Alt + Enter => Replace if statement with respective branch
- Simplify always-true if statement
  - Alt + Enter => Replace if statement with respective branch
- And again: Simplify always-true if statement
  - Alt + Enter => Replace if statement with respective branch
- Replace backstage pass name check with `isBackstagePass`
  - Select code, replace with `isBackstagePass`
  - ?? Could I have avoided this somehow when I first created `isBackstagePass`?
- And again: Simplify always-true if statement
  - Alt + Enter => Replace if statement with respective branch
- Replace always-true expression with `true`
  - Select `item.Name != "Sulfuras, Hand of Ragnaros"` - type over with true
- Get rid of redundant `if(true)`
  - Place cursor inside `if`
  - Alt + Enter => Remove unreachable code
  - Alt + Enter => Remove braces
- Inline `isBackstagePass`
  - Ctrl + R, I
- NEW CASE FOR SULFURAS
- Create new `isSulfuras` variable
  - Select `item.Name != "Sulfuras, Hand of Ragnaros"`
  - Ctrl + R, V => isNotSulfuras
  - Select => Ctrl + Shift + R, invert boolean => `isSulfuras`
- Extract `DoEverythingElse` and call in both branches of Sulfuras if statement
- Inline `DoEverythingElse`
- Remove three chunks of unreachable code
  - x3: place cursor next to grey brace => Alt + Enter => Remove unreachable code
- Remove empty if statements
  - Can't find shortcut for this? 
  - Manually delete!
- Simplify three always-true if statements
  - x3: Alt + Enter => Replace if statement with respective branch
- Inline `isSulfuras`
  - Ctrl + R, I
- Convert if statement to switch statement
  - Put cursor in very top `if` statement
  - Alt + Enter => Convert to switch statement
