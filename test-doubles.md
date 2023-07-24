# Table of contents

- [Finding the code](#finding-the-code)
- [Lab Exercise 1](#lab-exercise-1)
- [Lab Exercise 2](#lab-exercise-2)
  - [C# demo notes](#c-demo-notes)

# Finding the code

- [Raw code is here (delivery controller refactoring kata)](https://github.com/emilybache/DeliveryController-Refactoring-Kata)
  - Visit the above url to fork (top right), then clone the code
  - For .Net Core, you might need to go into the two csproj files and change TargetFramework to net6.0

# Lab Exercise 1

- Your task is to test the DeliveryController.UpdateDelivery method
- If you create the simplest test you possibly can, the test won't run
  - You get an error: "Failure sending mail."
  - There is a C# example of such a test [here](https://github.com/claresudbery/DeliveryController-Refactoring-Kata/tree/first-failing-test)
- There are two collaborators - `EmailGateway` and `MapService`. 
  - Should you replace both with test doubles? 
  - What kind of test doubles?
- The first test - `Test_UpdateDelivery_UpdatesDelivery_ToArrived` - can be made to work if you inject email gateway
  - There is a C# demo of this [here](https://github.com/claresudbery/DeliveryController-Refactoring-Kata/tree/test-start)
    - In here, both email gateway and map service are injected
    - But they are not stubbed, so you still get an error when you run the test
  - By switching to a stub of email gateway, you can make the first test pass: 
      - In call to constructor, replace `new EmailGateway()` with `stubGateway`
      - Alt + Enter => Create local variable
      - Add `= new StubEmailGateway();`
      - Alt + Enter => create new type
      - Remove body of unimplemented method in new class
      - Run test again - will pass
  - You don't need a stub of map service to make this test pass
      - The question is, when might you need a test double for map service?

# Lab Exercise 2

- Your task is still to test the DeliveryController.UpdateDelivery method
- Code from the coding demo can be seen [here](https://github.com/claresudbery/DeliveryController-Refactoring-Kata/blob/bootcamp-scratch)
- You have two choices:
  1. Continue where you left off
  2. ...or Use the [C# test-start branch](https://github.com/claresudbery/DeliveryController-Refactoring-Kata/tree/test-start) and...
    a. Get the test to pass by creating and passing a stub email gateway
    b. Decide when a map service double might be needed 

## C# demo notes

- [This code](https://github.com/claresudbery/DeliveryController-Refactoring-Kata/blob/bootcamp-scratch) creates a test double for map service as well as email gateway
    - It actually creates many different types of test double for different jobs in different types of test
- Examples
    - DUMMY: `dummyDeliveryEvent` in `Test_UpdateDelivery_SendsEmail`
    - STUB: `stubMapService` (returns data from `CalculateEta` for the email gateway)
    - MOCK: `mockEmailGateway` (also a spy)
    - SELF SHUNT (also mock/spy): the test class implements `IMapService`
    - SPY: (not exactly shown) If you used a mocking framework, it would probably have spies available - but the self shunt code also acts as a spy
    - FAKE: (not shown) If your email service wrote email content out to a log file
- How to do self shunt using IDE tools:
    - Replace `new MockEmailGateway()` with `this` in `Test_UpdateDelivery_UpdatesDelivery_ToArrived`
    - Let the automated tools guide you through the rest 
- The terminology doesn't matter as much as the ideas
- Stubs and Fakes are simpler than Mocks and Spies - the latter will fail the test if they are not called correctly.
- You don’t need to replace a value object with a test double.
- You might not even need to replace a more complex collaborator with a double. 
- Usually only need a stub if the real collaborator is slow, unreliable or otherwise difficult to use in a unit test. 
- Only need a mock if you need to check the collaborator received correct calls or data.
- There are two main schools of TDD 
    - this advice is from the ‘classic’ or ‘Chicago’ school. 
    - Other TDD practitioners may prefer to use doubles for all collaborators even if they are not slow or unreliable
        - to isolate the unit under test.
