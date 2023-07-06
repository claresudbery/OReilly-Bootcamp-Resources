The Google Doc version of this page is [here](https://docs.google.com/document/d/18XsMcFpEaMVboDV34adPQAfoJumMS94Ya3nMOeOpjkc/edit#heading%253Dh.rgjxkentq0vm).

# Table of contents

- [Gilded Rose: Getting Started With Approval Tests in C#](#gilded-rose-getting-started-with-approval-tests-in-c)
- [Gilded Rose and Approval Tests for .Net Core in Rider on a Mac](#gilded-rose-and-approval-tests-for-net-core-in-rider-on-a-mac)
- [Gilded Rose C# Approval testing with nuget ApprovalTests package](#gilded-rose-c-approval-testing-with-nuget-approvaltests-package)
- [Verify Approval Testing Tool](#verify-approval-testing-tool)
- [Gilded Rose: Working in Visual Studio](#gilded-rose-working-in-visual-studio)
- [Gilded Rose C# Approval testing with texttest tool](#gilded-rose-c-approval-testing-with-texttest-tool)

# Gilded Rose: Getting Started With Approval Tests in C#

- There are two ways to run approval tests. The simplest is to use the nuget [ApprovalTests package](https://github.com/approvals/ApprovalTests.Net), as in [ApprovalTest.cs](https://github.com/claresudbery/GildedRose-Refactoring-Kata/blob/csharp-liftup-start/csharp/ApprovalTest.cs). 
    - See below for getting approvals working in .Net Core in Rider on MacOS
    - You might need to install the [ApprovalTests](https://github.com/approvals/ApprovalTests.Net) nuget package: Tools => NuGet Package Manager => Manage Nuget packages for solution
    - You need an approved file - `ApprovalTest.ThirtyDays.approved.txt` - this file has been added to the [`csharp-approval-fixes` branch](https://github.com/claresudbery/GildedRose-Refactoring-Kata/tree/csharp-approval-fixes) of Gilded Rose.  
    - You can use the Resharper test runner or the built-in Visual Studio test runner to run tests: 
        - Resharper test runner:
            - Click the blobs in the gutter on line 13 of [ApprovalTest.cs](https://github.com/claresudbery/GildedRose-Refactoring-Kata/blob/csharp-liftup-start/csharp/ApprovalTest.cs), where the `ApprovalTest` class is defined
            - …or Extensions => Resharper => Unit tests => unit test sessions
        - Built in VS test runner: 
            - Test => Test explorer
- The alternative way to run tests is to use the texttest utility 
    - [Instructions here](https://clare-wiki.herokuapp.com/pages/think/code-princ/Refactoring#gilded-rose-c-approval-testing-with-texttest-tool)
    - You need to edit `config.gr` - see commits in this [dedicated branch](https://github.com/claresudbery/GildedRose-Refactoring-Kata/commits/csharp-approval-fixes)
        - I didn't manage to get this working in `csharpcore` in Rider on a Mac - gave up quite quickly though

## Gilded Rose and Approval Tests for .Net Core in Rider on a Mac

- use the `csharpcore` folder
- `Testtextfixture.cs` contains a `Main` function which is the equivalent of `Program.Main` in .Net framework
    - It currently only tests 2 days, so set the `days` var to 31 instead of 2 
- You need to add an `ApprovalTest.cs`
    - I copied the one from the `csharp` folder - I've also added it to the [`csharp-approval-fixes` branch](https://github.com/claresudbery/GildedRose-Refactoring-Kata/tree/csharp-approval-fixes) of Gilded Rose. 
- You need to install the `NUnit` and [ApprovalTests](https://github.com/approvals/ApprovalTests.Net) nuget packages: 
    - Until you have, the text will be red in the `using` clause at the top of `ApprovalTest.cs`
    - I've added them both to the `csproj` file in the [`csharp-approval-fixes` branch](https://github.com/claresudbery/GildedRose-Refactoring-Kata/tree/csharp-approval-fixes) of Gilded Rose. 
    - If you need to add them yourself...
        - click the icon that appears on the left of this line and it will give you an option to add the nuget package
        - or go to Tools => NuGet => Manage Nuget packages for GildedRoseTests
            - It will search for the package for you
            - Select it on the left, then click the green plus button on the right to add the package
- You need an approved file 
    - `ApprovalTest.ThirtyDays.approved.txt` - this file has been added to the [`csharp-approval-fixes` branch](https://github.com/claresudbery/GildedRose-Refactoring-Kata/tree/csharp-approval-fixes) of Gilded Rose. 
    - To generate your own, do the following:
        - (first add `ApprovalTest.cs` and install `NUnit` and `ApprovalTests` packages - see above)
        - Run the test in `ApprovalTest.cs` - click the green play button at the top of the file (by the class declaration)
        - This will create both an `approved.txt` file and a `received.txt` file
        - The first time I did this, it also opened up a diff tool with the two files side by side
            - but I couldn't work out how to copy the contents from the received file to the approved file
            - and then I lost that window and never saw it again!
        - The `received.txt` file will not be visible in the file explorer by default
            - You have to click the "Show all files" button, which is at top left of the explorer and looks like an eye with a file icon on its bottom right corner
        - Delete the `approved.txt` file, copy the `received.txt` file and rename the copy to `ApprovalTest.ThirtyDays.approved.txt`
        - Now the test in `ApprovalTest.cs` should pass
- Running tests
    - By default, when tests fail you'll just get an error saying the files don't match
    - To see where the mismatches are between expected and actual output:
        - make sure you can see both `approved.txt` and `received.txt` in the file explorer
            - You have to click the "Show all files" button, which is at top left of the explorer and looks like an eye with a file icon on its bottom right corner
        - select both files
        - Right click => Tools = Compare
            - or just Splat + D
    - Note that the `received.txt` file only persists when tests fail
        - The next time the tests pass, it will disappear (I think?)
        - You don't want to check it into source control
        - I've added it to `gitignore` in the [`csharp-approval-fixes` branch](https://github.com/claresudbery/GildedRose-Refactoring-Kata/tree/csharp-approval-fixes) of Gilded Rose. 

## Gilded Rose C# Approval testing with nuget ApprovalTests package

- Note that another C# approvals tool is also available - see [below](#verify-approval-testing-tool). But otherwise...
- If you're running the gilded rose code in C#, there's an approval testing tool which is being used
- It's [this tool](https://github.com/approvals/ApprovalTests.Net)
    - That page linked to above gives an example of verifying an array
    - If you're starting from scratch, you first need to find a way of gathering enough possible outputs to cover your code
    - Then run an `Approvals` test
        - as in the above example, where an array of strings is used as the golden master
        - or as in `ApprovalTest.cs` in Gilded Rose, where Console output is redirected from Program.Main
        - or as in `XmlExporterTest.cs` in the `with_tests` branch of the [Product Export kata](https://github.com/emilybache/Product-Export-Refactoring-Kata), where xml is verified
        - also see my demo code in the `approval-tests` branch of [my fork of the Export Product kata](https://github.com/claresudbery/Product-Export-Refactoring-Kata/tree/approval-tests), where I create a dictionary of objects, call `VerifyAll`, and I implement `ToString` for the relevant class, so that each object can be printed out into the approval file.
        - Then copy the `received` file into a long-lived `approved` file as in the example below
- Find `ApprovalTest.cs` and run the test in this file
- You'll probably find the first time you run it, it fails
    - When it fails, it shows you the correct output and the actual output in a merge tool (my system uses KDiff3), so you can see why it's failing
- The reason for this is that it needs a template to compare output against
- When the tests are run, it creates two files: `ApprovalTest.ThirtyDays.approved.txt` and `ApprovalTest.ThirtyDays.received.txt`
- It then compares the two files, and if they match, the test passes
- What you need to do is copy the `received` file into the `approved` file.
    - This command will do that for you on the command line: `cp csharp/ApprovalTest.ThirtyDays.received.txt csharp/ApprovalTest.ThirtyDays.approved.txt`
- After this when you run the test, it will pass and the `received` file will be deleted as soon as the test is run.

## Verify Approval Testing Tool

- Emily showed us a new tool for Approval Testing. We'd previously been using `Approvals`, but this one is called `Verify`.
- Details [here](https://github.com/VerifyTests/Verify).
- Demo video from Emily [here](https://www.dropbox.com/s/arpaxxqbrcyn0x3/SupermarketReceipt_csharp_verify.mp4?dl=0).
- Annotation is different - looks like this - `[UsesVerify]`
- You can use the `NUnit.Verify` package - others exist for other test frameworks.
- Each test case has to return `Task` (from `System Threading`) instead of `void`
- At the end of the test: `return Verifier.Verify(myStringResult);`
- What's produced is a "verified" file rather than an "approved" file - that you work with at the end
- There's a Resharper plugin that will give you new resharper context menu items for Accept and Compare - makes it easier to work with output files.

## Gilded Rose: Working in Visual Studio

- Enterprise version of VS has Live Unit Testing - green button on right in test explorer (see image below) - equivalent to NCrunch

![gilded-rose-visual-studio-live-unit-testing](/resources/images/gilded-rose-visual-studio-live-unit-testing.png)

- You can do a lot of what Resharper provides just using VS default functionality
    - People without Resharper might need to change target version of project from AnyCPu to x86 (see image below)
    - You can't inline when using VS functionality
        - you only can if it's a one-liner
        - there's a big debate about this online apparently!
    - another one missing from VS is "remove braces"

![gilded-rose-visual-studio-no-resharper-change-target-version](/resources/images/gilded-rose-visual-studio-no-resharper-change-target-version.png)

## Gilded Rose C# Approval testing with texttest tool
    
- Emily uses an approval testing tool from texttest.org which has been implemented in many different languages:
- Full details are [here](https://github.com/emilybache/GildedRose-Refactoring-Kata/tree/main/texttests), but here is a summary:
- `TextTest` is a Python-based tool, 
    - It has to be installed separately (see below).            
    - Once you've installed `TextTest` you need to go to the `texttests` sub-folder in the Gilded Rose repo and find the file `texttests\config.gr` and uncomment the lines that relate to the language you're using.
        - You also need to build the code in whatever language you're using
        - For instance if you're using `C#`, you need to build the executable that's referred to in `config.gr`
        - Note that the default value for `C#` in `config.gr` is incorrect - it should be `/csharp/bin/Debug/csharp.exe` rather than `/GildedRose.exe`
        - Now you can run the approval tests, by running `testtext &` on the command line 
    - You can install the [GUI tool for Windows here](https://sourceforge.net/projects/texttest/)
        - I had to click the Download button a few times before it actually downloaded - I don't know why
        - Then I had to run the tool manually, close it, and restart my bash prompt before I could run the Gilded Rose approval tests
            - Do this by running `texttest &` on the command line in the root Gilded Rose folder - this will bring up the UI
            - (First edit `config.gr`, and build an updated executable - see above)
            - now you have to select ThirtyDays on the left, and press the run button at the top of the screen.
            - This will open a new window with the results of the tests. If they fail, you can click Approve to make the new results be the new master, or you can just close down the window if you don't want to do that.
        - There are also tools for Linux and Mac in the "Installing TextTest Development Tools" section [on this page](https://texttest.org/)
    - ...or you can install the Python command line tool:
    - First install [Python3](https://www.python.org/)
    - For Windows, you can download one of the installers at the [bottom of this page](https://www.python.org/downloads/release/python-3104/) (for most people, it's 64-bit), then just follow instructions. It's recommended to click the final button to allow longer file paths.
        - ! I found I got `command pip not found` after this, so I had to run the installer again, select "modify installation" and make sure that pip was installed
        - Still no joy after that, so I had to modify my path - follow instructions [here](https://medium.com/swlh/solved-windows-pip-command-not-found-or-pip-is-not-recognized-as-an-internal-or-external-command-dd34f8b2938f)
    - After that, you can run `pip install texttest` in Bash prompt or Windows Terminal or Windows Powershell.
    - Full `TextTest` installation instructions are [here](https://texttest.org/) 
    
