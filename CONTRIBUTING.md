# Contributing

Thank you for taking the time to consider contributing to Labrador. Your assistance and enthusiasm is very appreciated!

Before getting started please ensure you've read over this Contributing guide as well as the guide located in the 
repository you want to contribute to. This guide contains general information applicable to all Labrador packages and 
the individual repositories may have repository-specific guides.

## Embrace asynchrony

Labrador is intended to be different from typical PHP frameworks which operate in a synchronous environment. This requires 
thinking about your software differently and means many I/O related function in PHP's standard library are off-limits.
Some important things to remember:

- Do NOT block the event loop. 

    This is likely the single most important thing to ingrain. Performing blocking operations 
    in your event loop handlers is a sure-fire recipe for an ill-performing application. If your code requires I/O (think 
    interacting with the filesystem or database or making HTTP calls) you should be using a library that supports those 
    operations asynchronously.

- Your objects are long-lived. 

    Particularly with HTTP applications where traditional PHP applications going through their entire bootstrap and 
    object creation process for every request it is important to note that Labrador is **NOT** like this. Bootstrapping 
    happens once and your objects are not re-instantiated for every request.
    
## Coding to an interface and Inversion of Control

Much of the Labrador codebase is powered by well-defined, limited-responsibility interfaces. This has repeatedly proven 
to result in decoupled codebases that are easy to adapt and change over time. Whenever possible you should be creating 
implementations based on an interface and avoid making concrete instances that do not have a well-defined public API.

Combined with our interface-driven approach is our dependence, pun intended, on dependency injection. If your objects
depend on other things that dependency should typically be defined in your constructor. This leads to codebases that are 
easy to test and easy to replace implementations as implementations are only required to adhere to a limited-responsibility
interface.

## Unit testing

Labrador is intended to be a codebase implemented using TDD practices. It is **HIGHLY** recommended that you follow 
the same general pattern of writing your tests first, before you start working on functionality. However, as long as your
contribution includes sufficient unit tests _when_ you write them is up to you. We do not necessarily aim for 100% coverage 
however if sufficient execution branches are not covered your Contributeion may be rejected until sufficient testing is 
in place.

## Coding Standard

Even for projects with the same, single developer, let alone a project with many contributors, it is important that all 
of the contributors use a consistent coding style. Reading and understanding code is often far more time-consuming and 
important than the act of writing the code itself. Having a consistent, easy-to-understand coding style is crucial to 
having an easy-to-understand codebase.

We **HIGHLY** recommend that you install [cspray/labrador-coding-standard] as a developer dependency and run the command
with your unit test suite. For all Labrador packages this command will be run as part of Continuous Integration so your 
code will need to conform to standards before it is allowed to be merged in.

[cspray/labrador-coding-standard]: https://github.com/labrador-kennel/coding-standard