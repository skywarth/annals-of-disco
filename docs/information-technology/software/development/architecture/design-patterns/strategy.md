# Strategy Pattern

- Behavioral design pattern
- TL;DR: Doing things in different ways, alternative algorithms


>"The Strategy pattern suggests that you take a class that does something specific in a lot of different ways and extract all of these algorithms into separate classes called strategies"

- Original class (the one that contains a strategy instance) is called `context`
- Each alternative/different algorithm or approach is called `strategy` (concrete strategy), each is a class that derives from a single interface/abstract class
- **`Context` doesn't choose `strategy`**, it is not `context`'s responsibility. Strategy is chosen by outer layer, the one that initiates/initializes the `context`
- `Context` doesn't know which strategy it'll proceed with
- Strategy classes **must** have a common method for the execution, defined in the interface/abstract class
