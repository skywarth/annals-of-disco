# Chain of Responsibility pattern
> AKA Chain of Command, CoR

- Behavioral design pattern
- TL;DR: Passing an object/structure through various hoops and phases, each coming after another. These chains/hoops may be dependent on the previous one.
- Often confused or disregarded when compared to Decorator pattern
  - Simple difference between Chain of Responsibility and Decorator is: in CoR you can break the chain at any point
  - Each decorators in Decorator pattern is meant to be completely independent of one another, wher in CoR it is usually the opposite
  - One argument is that CoR is a subset of Decorator pattern, it is true to some extent
  - Decorator is a **structural** design pattern whereas the CoR is **behavioral** design pattern
- You can conceptualize the CoR as a chain made up of links, or a linked-list. Each link/chain connects the the previous one to this one, and the next. They can handle, process, manipulate data and pass it to next, or pass it altogether to the next.

> "Chain of Responsibility is a behavioral design pattern that lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain."

## Use cases

### Request classes/controllers/DTOs

Request; validation, parsing, authentication, autherization, formatting, sanitization, logging, caching, notification, triggers, rollbacks, merging, analysis etc.

- Because usually you have dozen of these if/else statements in your controllers or handlers.
- Some depend on each other, some are independent but wouldn't make sense to run it regardless
- Ordering is crucial
- If-else statements are nested, hard to follow, coming after one another
- Ordering becomes hard to follow and complicated

Or middlewares in general basically.

### Support ticket escalation

Escalating a support ticket through levels of escalation via assertions, if the current escalation level handlers fail, it is passed on to the next one.

### ATM withdrawl scenario

When dispensing banknotes from ATM, assuming we always want to dispende highest marked bill when possible, we can use CoR pattern. 

Dispense 100$ bills first, then if leftover is less than 100$ then dispense 50$, then if leftover is less than 50$ then dispense 20$ so on so forth.


## Guideline

- Any chain or handler shall stop the flow at any point, preventing it from passing to the next chain/handler.
- [!] Two schools of thought for the usage of CoR
  1. First pass: Handlers are meant to break the flow if it can handle/process the data. If it can't process, only then it passes the data to the next chain
  2. All or nothing: Handlers are meant to continue the flow based on assertion as long as the assertion/check is true. Only if the checks fail, handler doesn't pass to the next chain, and effectively breaks the process
- Handler classes (chains) must implement a common interface, or extend from an abstract class 
