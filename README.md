# OReilly-Bootcamp-Resources
Links etc to be shared with bootcamp participants. The Google doc version of this page is [here](https://docs.google.com/document/d/1-R4NSu679ymbXBneWmib8HC4viaGqmkLzGGPu9ITSOE/edit?usp=sharing).

# Table of contents
- [Links from Day 1](#links-from-day-1)
- [Day 2](#day-two)
  - [Code coverage tools](#code-coverage-tools)
  - [Using coverage to add tests - exercise](#using-coverage-to-add-tests---exercise)
  - [Links from Day 2](#links-from-day-2)
- [Day 3](#day-three)
  - [KEYBOARD SHORTCUTS for “Replace conditional with polymorphism”](#keyboard-shortcuts-for-replace-conditional-with-polymorphism)
  - [Links from Day 3](#links-from-day-3)
- [Day 4](#day-four)
  - [Links from Day 4](#links-from-day-4)
- [Links to find Clare Sudbery](#links-to-find-clare-sudbery)

# LINKS FROM DAY 1
- [DORA reports](https://www.devops-research.com/research.html)
- [Accelerate - book by the people behind DORA](https://itrevolution.com/book/accelerate/)
- [The DevOps Handbook](https://learning.oreilly.com/library/view/the-devops-handbook/9781457191381/)
- [Article on relationship between Flow and Slack](https://www.sitepoint.com/we-simulated-waterfall-kanban-scrum-which-works-best/)
- [Slack - book by Tom DeMarco](https://www.penguinrandomhouse.com/books/39276/slack-by-tom-demarco/)
- [Martin Fowler on Kent Beck’s 4 rules of design](https://martinfowler.com/bliki/BeckDesignRules.html)
- [Dave Farley - Continuous Compliance](https://www.davefarley.net/?p=285)
- [Dragan Stepanovic - Async Code Review](https://www.infoq.com/articles/co-creation-patterns-software-development/)
- [“YAGNI” (You Ain’t Gonna Need It) - article by Ron Jeffries](https://ronjeffries.com/xprog/articles/practices/pracnotneed/)
- Exercise instructions - [Fizzbuzz requirements](https://www.sammancoaching.org/kata_descriptions/fizzbuzz.html)
- Sample FizzBuzz designs:
  - [Design 1](https://github.com/emilybache/FizzBuzzKata-Samples/blob/master/java/src/main/java/codingdojo/Fizzbuzz1.java)
  - [Design 2](https://github.com/emilybache/FizzBuzzKata-Samples/blob/master/java/src/main/java/codingdojo/Fizzbuzz2.java)
  - [Design 3](https://github.com/emilybache/FizzBuzzKata-Samples/blob/master/java/src/main/java/codingdojo/Fizzbuzz3.java)
  - [Design 4](https://github.com/emilybache/FizzBuzzKata-Samples/blob/master/java/src/main/java/codingdojo/Fizzbuzz4.java)
  - [Design 5](https://github.com/emilybache/FizzBuzzKata-Samples/blob/master/java/src/main/java/codingdojo/Fizzbuzz5.java)
  - [Design 6](https://github.com/emilybache/FizzBuzzKata-Samples/blob/master/java/src/main/java/codingdojo/Fizzbuzz6.java)
- [FizzBuzz Coding Demo](https://vimeo.com/813994444/d6a81e4275)
- Prepping for Day 2: 
  - The code you'll need is [here](https://github.com/emilybache/GildedRose-Refactoring-Kata)
  - [Getting approval tests working](/gilded-rose-approvals.md)
    - I'm aware this link won't work for some - I'll move it over to GitHub asap and update this page.
 
# DAY TWO 

## CODE COVERAGE TOOLS
- .Net:
  - [NCrunch](https://www.ncrunch.net/)
  - [Visual Studio](https://learn.microsoft.com/en-us/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested?view=vs-2022&tabs=csharp)
  - [DotCover](https://www.jetbrains.com/dotcover)
  - [Rider - DotCover](https://www.jetbrains.com/help/rider/Settings_DotCover.html)
- Other:
  - [IntelliJ - IDEA](https://www.jetbrains.com/help/idea/code-coverage.html)

## USING COVERAGE TO ADD TESTS - EXERCISE 
- Code is [here](https://github.com/emilybache/GildedRose-Refactoring-Kata) 
- Requirements are in the readme
- Run this command to clone the code: git clone https://github.com/emilybache/GildedRose-Refactoring-Kata.git
- Choose your language
- Instructions [here](/gilded-rose-approvals.md) on getting approval tests working with the Gilded Rose kata

## LINKS FROM DAY 2
- Code coverage tools - see above
- [Gilded Rose kata](https://github.com/emilybache/GildedRose-Refactoring-Kata)
  - My [demo C# code of approval tests with 100% code coverage](https://github.com/claresudbery/GildedRose-Refactoring-Kata/tree/coverage-demo-complete)
- [Lift kata](https://github.com/emilybache/Lift-Kata/)

# DAY THREE

## KEYBOARD SHORTCUTS for “Replace conditional with polymorphism”

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

## Links from Day 3

- Many more much smaller steps:
    - Geepaw Hill’s [MMMSS idea](https://www.geepawhill.org/2021/09/29/many-more-much-smaller-steps-first-sketch/)
    - [Benefits of MMMSS](https://www.geepawhill.org/2021/11/16/mmmss-the-intrinsic-benefit-of-steps/)
    - [Rework avoidance theory](https://www.geepawhill.org/2020/07/17/the-rat-rework-avoidance-theory/) 
- Refactoring vocabulary / extract method:
    - Martin Fowler’s [refactoring catalog](https://refactoring.com/catalog/)
    - Code base: [Tennis refactoring kata](https://github.com/emilybache/Tennis-Refactoring-Kata)
    - [Video demo](https://www.youtube.com/watch?v=8G0Y4kDdqNY)
- Replace conditional with polymorphism:
    - Code base: [Parrot refactoring kata](https://github.com/emilybache/Parrot-Refactoring-Kata)
    - [Video demo](https://drive.google.com/file/d/1-0jeMv9jg3Tpr_4ln13-8e1cVbIRshBh/view?usp=sharing)
    - [Martin Fowler’s page on this technique](https://refactoring.com/catalog/replaceConditionalWithPolymorphism.html)
    - [Emily Bache demos the technique on Gilded Rose](https://www.youtube.com/watch?v=NADVhSjeyJA)
- Lift up conditional:
    - Code base: [Gilded rose refactoring kata](https://github.com/emilybache/GildedRose-Refactoring-Kata)
    - [Video demo](https://vimeo.com/801311948/41a83a3c4e)
    - [Lift up conditional - start point](https://github.com/claresudbery/GildedRose-Refactoring-Kata/blob/csharp-liftup-start/csharp/GildedRose.cs) 
    - [Lift up conditional - end point](https://github.com/claresudbery/GildedRose-Refactoring-Kata/blob/csharp-liftup-demo/csharp/GildedRose.cs)
    - My fork of the GildedRose repo - [the branch with all the commits demoing the lift-up conditional technique](https://github.com/claresudbery/GildedRose-Refactoring-Kata/tree/csharp-liftup-demo)
    - [Emily Bache's Gilded Rose videos](https://clare-wiki.herokuapp.com/pages/think/code-princ/Refactoring#emilys-gilded-rose-demo-videos) (including a "lift up conditional" demo) 

# DAY FOUR

## Links from Day 4



# LINKS TO FIND CLARE SUDBERY

- [Clare's LinkedIn](https://www.linkedin.com/in/clare-sudbery-she-her-35939540/)
- [Clare on Twitter](https://twitter.com/ClareSudbery)
- [The Making Tech Better podcast (season one hosted by Clare)](https://www.madetech.com/podcast/)  
  - [Interview with Emily Bache on Refactoring](https://www.madetech.com/podcast/episode-19-emily-bache/)
  - [Interview with Geepaw Hill on Test Driven Development](https://www.madetech.com/podcast/episode-15-geepaw-hill/)
  - [Interview with Meri Williams on Changing legacy systems](https://www.madetech.com/podcast/episode-10-meri-williams/)
- [Quality Code Bootcamp delivered by Clare for O’Reilly Learning](https://learning.oreilly.com/live-events/quality-code-boot-camp/0636920086483/)
- [Fundamentals of Refactoring](https://learning.oreilly.com/live-events/fundamentals-of-refactoring/0636920069707/0636920069705/), delivered by Clare for O'Reilly learning
- [Refactoring for Continuous Delivery](https://learning.oreilly.com/live-events/refactoring-for-continuous-delivery/0636920074785/0636920074784/), delivered by Clare for O'Reilly learning
- [Clare's other upcoming events](https://medium.com/a-woman-in-technology/events-28336c2586df)

