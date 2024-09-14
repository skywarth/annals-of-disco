# Hexagonal Architecture

> AKA Ports & Adapters pattern


- Domain focused architecture
- Idea is to decouple the business logic from the infrastructural concerns
- `Application` is the application itself, the core application, your app
- Two types, `primary` and `secondary`
	- `Primary` port/adapter **control** the application. **Inbound**
	- `Secondary` port/adapter is **controlled** by the application. **Outbound**
	- Each connect to the respective other, `Primary Adapter` is matched with a `Primary Port`, `Secondary Adapter` is matched with `Secondary Port`
- Ports and adapters have various forms of relationships
	- 1-1
	- 1-N (common, one port multiple adapters)
	- N-1
	- N-N (rare)

## Core

- `Application` core, the center of hexagon
- Domain Logic
- Business logic
- It is **not** limited to the codebase, or defined by it. Something that exists in the codebase or the repository may certainly fall out of the limits of the [[#Core]], **so don't think it as your codebase**.
- Strictly domain/business logic, nothing else; no service that directly interacts with external dependency and services
- It should be free of infrastructural concerns
- It shouldn't ask the question of **how**, it should ask the question of **what**
- [[#Port]]s are part of the Core


```
Core:
   +----------------------------+
   | SomeBusinessLogicService   | <-- Uses UserRepository
   |                            |
   +----------------------------+
             |
   +----------------------------+
   | UserRepository (Port)      | <-- Secondary Port (Interface)
   +----------------------------+
             |
             |
 //////////////////////////////// <-- Hexagon side, boundary of the core)
			 |
			 |
Secondary Adapter (Outside of Core, outer area of the hexagon):
   +-----------------------------+
   | MySQLUserRepository         | <-- Implements UserRepository (Adapter)
   |                             |
   +-----------------------------+
             |
   +-----------------------------+
   | MySQL Database              | <-- External System
   +-----------------------------+

```


## Flow

Flow can originate from one of two origins:
1. Originate from the core itself
2. Originate from an external agent and go through **Primary channels** (primary adapter into primary port into core)

- Flow cannot originate from **secondary channels**, I mean duh.

```
External Agent: Mobile app user (initiates the flow by an action/request)
      |
      |
Primary Adapter: UserRegistrationController (REST API)
      |
      |
Primary Port: UserRegistrationService
      |
      |
Core Application: SomeBusinessLogicService
      |
      |
Secondary Port: UserRepository
      |
      |
Secondary Adapter: MySQLUserRepository
      |
      |
External System: MySQL Database

```
## Port

- Inner sides of the hexagon represents the ports
- Ports interact with external services and dependencies that are called [[#Adapter]]
- **Part of the [[#Core]]**, they are considered as [[#Core]]

### Primary port

- Entry point into the application
- Defines how actions procured by an external agent are going to interact with the [[#core]] business logic
- Communicates with the respective [[#Primary adapter]]
- `AuthHandler`, `CheckoutStrategy`, `UserRegistrationService`, `UserActionHandler`, `FileUploadService`


### Secondary port

- Exit point or an interface to access external services
- Defines a contract, an interface for means of communication with the external world
- Communicates with the [[#Secondary adapter]]
- `UserRepository`, `MessagePublisher`, `EmailFacade`, `FileStorage`, `PaymentGatewayAdapter`



## Adapter

- Outer side of the hexagon
- External service/system/dependency method
- Interfaced/accessed by a [[#Port]]
- Don't be confused: an adapter can still actually reside inside the application. For example, `MySQLUserRepository`. This is because they interact with external services.

### Primary adapter

- Adapters that wants to access the application and/or it's data
- Implementation for the [[#Primary port]]
- For example another app that relies on your data for its operations, some external that **consumes** your API
- `UserRegistrationController` (REST API) handling HTTP requests for user registration operations, `UserRegistrationGraphQL`, `UserRegistrationCLI`. Or `DesktopUserActionHandler`, `MobileUserActionHandler`. Or `RESTFileUploadController`, `FormFileUploadController`


### Secondary adapter

- Connects the application to external systems
- Outbound communication
- Implementations for [[#Secondary port]], conforming to its contract
- `MySQLUserRepository`, `MongoUserRepository`, `RabbitMQMessagePublisher`, `MailgunEmailSender`, `LocalFileStorage`, `S3FileStorage`, `StripePaymentGateway`, `PayPalPaymentGateway`




## Resources

- https://craftbettersoftware.com/p/hexagonal-architecture-with-tdd
- https://scalastic.io/en/hexagonal-architecture/#:~:text=Hexagonal%20architecture%20is%20an%20architectural,communicate%2C%20using%20ports%20and%20adapters
- https://softengbook.org/articles/hexagonal-architecture
- https://github.com/JonathanM2ndoza/Hexagonal-Architecture-DDD
- https://www.geeksforgeeks.org/hexagonal-architecture-in-java/
- https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/
- https://en.wikipedia.org/wiki/Hexagonal_architecture_(software)