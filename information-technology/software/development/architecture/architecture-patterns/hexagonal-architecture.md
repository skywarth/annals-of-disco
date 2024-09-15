# Hexagonal Architecture

> AKA Ports & Adapters pattern

## Characteristic

- In concept; it is very similar to `Clean architecture` and `Onion architecture`
- Domain focused architecture
	- Though it adheres to Domain-Driven Design in most aspects, it is not directly related to it. They are distinct concepts.
	- You may say it is inspired by DDD
- `Application` is the application itself, the core application, your app
- Two types, `primary` and `secondary`
	- `Primary` port/adapter **control** the application.
		- **Inbound**
		- Basically the means of Interface: Actors or anything that invokes the application
	- `Secondary` port/adapter is **controlled** by the application. 
		- **Outbound**
		- Basically the infrastructure
	- Each connect to the respective other, `Primary Adapter` is matched with a `Primary Port`, `Secondary Adapter` is matched with `Secondary Port`
- Ports and adapters have various forms of relationships
	- 1-1
	- 1-N (common, one port multiple adapters)
	- N-1
	- N-N (rare)
- In theory, each side is meant to represent a reason/concern for the business logic to communicate with the external services, this is the reason it is not a circle but rather a hexagon. Examples for each side: notification, persistence (data), logging, authentication, authorization.
- Since each side of the hexagon is meant to represent concern (or a communication channel with an external), it doesn't really have to be an hexagon, don't think you're fixed for six externals. It can be quadrant, pentagon, octagon... 

### Comparison with other architectures

#### MVC

By their nature, `MVC` and `hexagonal architecture` are often mutually exclusive due to:

- In MVC frameworks, models and entities usually come coupled with ORM structures, whereas referring to technologies or infrastructure in core business logic (in this case, the models/entities) violate this rule. Hexagonal architecture dictates entities and domain models should be **pure**
	- `Laravel` models are extended from `Model` which is tightly coupled with ORM, and ORM is about data persistence, hence an infrastructural concern bleeds into the core business domain, hence the violation of hexagonal principle
	- If the `MVC` framework or structure you're using doesn't mix domain models with `persistence`, keeps the entities/models pure, then it is compliant with hexagonal.
- MVC controllers usually contain input processing, validation and sometimes even business logic 
- MVC architectures are commonly known for strictly adhering to framework's limitations and principles. MVC architectures are **framework-centric**, meaning: your structure and design tries to accommodate the framework's rules and conventions, which leads to strong dependency on the framework
- Hexagonal dictates a clear separation between business logic and external dependencies, however this line is blurred in MVC. For example, in MVC; a controller may directly call a domain entity's ORM procedures, run queries. Or a model may handle input validations, this is a violation of hexagonal rules.
- MVC is far easier to get started with thanks to well established frameworks and it's `infrastructure-first` approach, though in time it is also easy for it to get messy to maintain. Hexagonal requires immense amount of planning and structuring beforehand.

### Pros

- **Adaptability**:Decouple the business logic from the infrastructural concerns, isolate the core
- **Testability**:Enhance testing capabilities and simplifying it
- Lower risk of regression from changes
- Reduce the refactor cost
- Fostering TDD by making core business logic easier to test
- Goes hand to hand with DDD
- Decontaminate presentation layer (UI, API, Endpoints etc) from business logic

### Cons

- Abundance of classes, packages and modules
- Tedious to keep the separation of concerns in check
- If the business logic is not too extensive, or it is rather a small-sized application; then it is an overkill
- Potential inefficiency


### When to use

- Complex or extensive business logic
- Business logic or core logic is stable, no constant radical changes




## Components


### Core

- `Application` core, the center of hexagon
- Domain Logic
- Business logic
- Also known as `domain classes`
- `User`, `Car`. Models/entities basically. And also use-cases.
- It is **not** limited to the codebase, or defined by it. Something that exists in the codebase or the repository may certainly fall out of the limits of the [[#Core]], **so don't think it as your codebase**.
- It shouldn't depend on anything, ports can depend on it but it shouldn't depend on anything. Direction of dependencies are from outside of the core to inside.
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
 //////////////////////////////// <-- Hexagon side, boundary of the core
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



### Port

- Inner sides of the hexagon represents the ports
- Ports interact with external services and dependencies that are called [[#Adapter]]
- In essence, they are `interface`s, software/programming interfaces (not UI)
- **Part of the [[#Core]]**, they are considered as [[#Core]] in a way

#### Primary port

- Entry point into the application
- AKA `Provided Port`
- Defines how actions procured by an external agent (or rather a primary adapter) are going to interact with the [[#core]] business logic
- Communicates with the respective [[#Primary adapter]]
- `AuthHandler`, `CheckoutStrategy`, `UserRegistrationService`, `UserActionHandler`, `FileUploadService`
- Ports can also be established in forms of CQRS. In CQRS, ports are `Command and Query`


#### Secondary port

- Exit point or an interface to access external services
- AKA `Required Port`
- Defines a contract, an interface for means of communication with the external world
- Communicates with the [[#Secondary adapter]]
- `UserRepository`, `MessagePublisher`, `EmailFacade`, `FileStorage`, `PaymentGatewayAdapter`



### Adapter

- Outer side of the hexagon
- External service/system/dependency method
- Interfaced/accessed by a [[#Port]]
- Don't be confused: an adapter can still actually reside inside the application. For example, `MySQLUserRepository`. This is because they interact with external services.
- Usually they are realized by `Adapter Design Pattern`

#### Primary adapter

- Adapters that wants to access the application and/or it's data
- Implementation for the [[#Primary port]]
- For example another app that relies on your data for its operations, some external that **consumes** your API
- `UserRegistrationController` (REST API) handling HTTP requests for user registration operations, `UserRegistrationGraphQL`, `UserRegistrationCLI`. Or `DesktopUserActionHandler`, `MobileUserActionHandler`. Or `RESTFileUploadController`, `FormFileUploadController`


#### Secondary adapter

- Connects the application to external systems
- Outbound communication
- Implementations for [[#Secondary port]], conforming to its contract
- `MySQLUserRepository`, `MongoUserRepository`, `RabbitMQMessagePublisher`, `MailgunEmailSender`, `LocalFileStorage`, `S3FileStorage`, `StripePaymentGateway`, `PayPalPaymentGateway`



## Flow

Flow can originate from one of two origins:
1. Originate from the core itself
	- This is not a recommended practice, it is anti-pattern per Hexagonal Architecture principles
2. Originate from an external agent and go through **Primary channels** (primary adapter into primary port into core)

- Flow cannot originate from **secondary channels**, I mean duh.


Below is an example flow that originates from external agent/system to primary channels then out of secondary channels.

```
External Agent: Mobile app user (initiates the flow by an action/request)
      |
      |
Primary Adapter: UserRegistrationController (REST API)
      |
      |
//////////////////// Hexagon side, boundary of the core
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
//////////////////// Hexagon side, boundary of the core
      |
      |
Secondary Adapter: MySQLUserRepository
      |
      |
External System: MySQL Database

```


## Examples

### Library management system


Using Node.js, Typescript, MongoDB, AWS S3, REST, gRPC.

File paths might be messed up a bit, don't mind it.

Maybe I should move it to a repository/folder, it looks a bit messy.


#### Core (business logic) components


```ts
//src/core/Book.ts
//Domain Model for Book.
export class Book {
  constructor(
    public id: string,
    public title: string,
    public author: string,
    public ebookUrl: string
  ) {}
}
```

```ts
//src/core/BookProcessingFacade.ts
//Core business logic
import { BookRepository } from './BookRepository';
import { EBookStorage } from './EBookStorage';
import { Book } from './Book';
import { BookManager } from './BookManager';

export class BookProcessingFacade implements BookManager {
  constructor(
    private bookRepository: BookRepository,
    private ebookStorage: EBookStorage
  ) {}

  async addBook(id: string, title: string, author: string, fileStream: Buffer): Promise<Book> {
    await this.ebookStorage.upload(id, fileStream);
    const ebookUrl = this.ebookStorage.getUrl(id);
    const book = new Book(id, title, author, ebookUrl);
    await this.bookRepository.save(book);
    return book;
  }

  async getBook(id: string): Promise<Book | null> {
    return await this.bookRepository.getById(id);
  }

  async downloadBook(id: string): Promise<Buffer> {
    return await this.ebookStorage.download(id);
  }
}

```

#### Ports

##### Primary ports

```ts

//src/core/ports/primary/BookManager.ts 
//Primary Port
import { Book } from './Book';

export interface BookManager {
  addBook(id: string, title: string, author: string, fileStream: Buffer): Promise<Book>;
  getBook(id: string): Promise<Book | null>;
  downloadBook(id: string): Promise<Buffer>;
}


```


##### Secondary ports

```ts
//src/core/ports/secondary/EBookStorage.ts
//Port Interface (Secondary Port for book storage)
export interface EBookStorage {
  upload(bookId: string, fileStream: Buffer): Promise<void>;
  getUrl(bookId: string): string;
  download(bookId: string): Promise<Buffer>;
}
```

```ts
//src/core/ports/secondary/BookRepository.ts
//Port Interface (Secondary Port for book repository)
import { Book } from './Book';

export interface BookRepository {
  save(book: Book): Promise<void>;
  getById(id: string): Promise<Book | null>;
}
```


#### Adapters

##### Primary adapters

```ts
// src/adapters/BookManagementController.ts
// Primary Adapter for BookManager Primary port
import { Request, Response } from 'express';
import { BookManager } from '../core/ports/primary/BookManager';

export class BookManagementController {
  constructor(private bookManager: BookManager) {}

  async addBook(req: Request, res: Response): Promise<void> {
    const { id, title, author } = req.body;
    const fileStream = req.file.buffer;
    const book = await this.bookManager.addBook(id, title, author, fileStream);
    res.status(201).json(book);
  }

  async getBook(req: Request, res: Response): Promise<void> {
    const book = await this.bookManager.getBook(req.params.id);
    if (book) {
      res.json(book);
    } else {
      res.status(404).json({ error: 'Book not found' });
    }
  }

  async downloadBook(req: Request, res: Response): Promise<void> {
    const fileBuffer = await this.bookManager.downloadBook(req.params.id);
    res.type('application/pdf').send(fileBuffer);
  }
}

```

##### Secondary adapters

```ts
//FileSystemEBookStorage.ts
//Secondary adapter for EBookStorage secondary port
import * as fs from 'fs';
import * as path from 'path';
import { EBookStorage } from '../core/ports/secondary/EBookStorage';

export class FileSystemEBookStorage implements EBookStorage {
  constructor(
    private basePath: string,  // Physical directory path
    private baseUrl: string    // Base URL for accessing files
  ) {}

  async upload(bookId: string, fileStream: Buffer): Promise<void> {
    const filePath = path.join(this.basePath, `${bookId}.pdf`);
    await fs.promises.writeFile(filePath, fileStream);
  }

  getUrl(bookId: string): string {
    return `${this.baseUrl}/ebooks/${bookId}.pdf`;
  }

  async download(bookId: string): Promise<Buffer> {
    const filePath = path.join(this.basePath, `${bookId}.pdf`);
    if (!fs.existsSync(filePath)) {
      throw new Error('File not found');
    }
    return fs.promises.readFile(filePath);
  }
}


```

```ts
//src/adapters/S3EBookStorage.ts
//Secondary adapter for EBookStorage secondary port
import { EBookStorage } from '../core/ports/secondary/EBookStorage';
import S3 from 'aws-sdk/clients/s3';

export class S3EBookStorage implements EBookStorage {
  private s3: S3;

  constructor() {
    this.s3 = new S3();
  }

  async upload(bookId: string, fileStream: Buffer): Promise<void> {
    await this.s3.upload({
      Bucket: 'library-ebooks',
      Key: `${bookId}.pdf`,
      Body: fileStream,
    }).promise();
  }

  getUrl(bookId: string): string {
    return this.s3.getSignedUrl('getObject', {
      Bucket: 'library-ebooks',
      Key: `${bookId}.pdf`,
      Expires: 60 * 60, // 1 hour expiration
    });
  }

  async download(bookId: string): Promise<Buffer> {
    const result = await this.s3.getObject({
      Bucket: 'library-ebooks',
      Key: `${bookId}.pdf`,
    }).promise();

    return result.Body as Buffer;
  }
}

```

```ts
//src/adapters/MongoDBBookRepository.ts
//Secondary adapter for BookRepository secondary port
import { Book } from '../core/Book';
import { BookRepository } from '../core/ports/secondary/BookRepository';
import { MongoClient, Db } from 'mongodb';

export class MongoDBBookRepository implements BookRepository {
  private db: Db;

  constructor(mongoClient: MongoClient, dbName: string) {
    this.db = mongoClient.db(dbName);
  }

  async save(book: Book): Promise<void> {
    const collection = this.db.collection('books');
    await collection.insertOne(book);
  }

  async getById(id: string): Promise<Book | null> {
    const collection = this.db.collection('books');
    const book = await collection.findOne({ id });
    return book ? new Book(book.id, book.title, book.author, book.ebookUrl) : null;
  }
}

```

#### Misc

```ts

// src/index.ts
import express from 'express';
import { BookManagementController } from './adapters/BookManagementController';
import { BookProcessingFacade } from './core/BookProcessingFacade';
import { MongoDBBookRepository } from './adapters/MongoDBBookRepository';
import { S3EBookStorage } from './adapters/S3EBookStorage';

const app = express();
app.use(express.json());

// Instantiate adapters (could be MongoDB, S3, etc.)
const bookRepository = new MongoDBBookRepository();
const ebookStorage = new S3EBookStorage();

// Instantiate core business logic (BookProcessingFacade)
const bookManager = new BookProcessingFacade(bookRepository, ebookStorage);

// Inject bookManager into the controller
const bookController = new BookManagementController(bookManager);

// Define routes
app.post('/books', (req, res) => bookController.addBook(req, res));
app.get('/books/:id', (req, res) => bookController.getBook(req, res));
app.get('/books/:id/download', (req, res) => bookController.downloadBook(req, res));

// Start the server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

## Resources

- [x] https://craftbettersoftware.com/p/hexagonal-architecture-with-tdd
	- IMHO, slightly incorrect and a bit misleading, I can't agree wholeheartedly on the architecture of the case. But still a decent post, concise.
	- Demonstrates on an example warehouse case
- [x] https://scalastic.io/en/hexagonal-architecture/#:~:text=Hexagonal%20architecture%20is%20an%20architectural,communicate%2C%20using%20ports%20and%20adapters
	- Comprehensive explanation with more focus on principles
	- Compares it with Clean Architecture
- [x] https://softengbook.org/articles/hexagonal-architecture
	- Deviates from other tutorials and elaborations, uses different terms
	- Diagrams are good
	- Contains questions at the and that make you think and reinforce your learning, I liked these questions
- [ ] https://github.com/JonathanM2ndoza/Hexagonal-Architecture-DDD
	- Hexagonal Arch with DDD and microservice using Java Spring
- [x] https://www.geeksforgeeks.org/hexagonal-architecture-in-java/
	- Simple application in Java, it is basic with there are some mistakes or possible confusion points, don't see it unless you understand the concept fully, or it will confuse you further
- [ ] https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/
- [x] https://en.wikipedia.org/wiki/Hexagonal_architecture_(software)
	- Explains the relation to Clean and Onion architectures
	- Has a really good diagram to grasp the concept