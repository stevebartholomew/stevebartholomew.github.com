The concept of start, analyse, rework is everywhere. It's the core of Agile. The lean startup movement advocates it. Writers create drafts. Painters draw in pencil then slowly fill out and refine as they go. Musicians write a song then edit and refine it.

Coding is no different from any other creative process.


As I start writing this post I already know that my first draft wont be the final version. 

I have a vauge structure in mind.  I might list out some bullet points or even create a basic mind map outlining the key elements but the truth is that until I've written the post, I'll not really know how the end product should be.

## Editing == Refactoring

I've heard it said many times that editing is the most important part of most creative processes. With writing you dump out words and ideas around a vauge structure and then you edit.  Relentlessly.

In the same way our first pass at code is rarely the best implementation. 

Attempts to improve this often result in guessing abstractions and interactions upfront - "I know I'm going to need this code elsewhere so I'd better make an abstract class...".

Forgot this. Embrace the draft and write code until you have something that passes a test - *then* you can start tidying it up.

## Guided by principals

We all know that merely implementing a pattern or idiom will not produce expressive, maintainable code. Instead, patterns should be used as tools to make code fit principals that we deem important.

For example, your principals may be:

1. Code's primary task should be to communicate with developers, using the domain's language & logic
2. Objects should communicate over simple interfaces rather than digging into each other's internal implementation

These are largely subjective but the alternative of hiding behind patterns is far worse. 

Whatever your principals are, pass code through them and refactor until you're happy. This is where patterns can really shine.

## Avoiding a ball of mud

The biggest criticsium of this approach is that over time you'll end up with a mess. This would be the case if it weren't for relentless refactoring. 

If you figure out that a whole chunk of code that you've already implemented needs ripping out, you do it. If you realise "oh man - we really just need an MVC structure here" - you do it.

A more experienced programmer will naturally spot patterns and code appropriately but even then, the risk that you'll over engineer is great.

What you should end up with are minimal impementations where necessary ("we didn't actually duplicate that functionality") and clean abstractions ("we only created an abstraction for what we actually needed").

Coding is *not* like building a house. It's 
