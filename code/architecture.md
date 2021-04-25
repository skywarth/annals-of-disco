### Concurrency vs Parallelism

> **"Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once."**
>
> A system is said to be concurrent if it can support two or more actions in progress at the same time. A system is said to be parallel if it can support two or more actions executing simultaneously.
> 
> Using the term “parallel” when the simultaneous execution is assured or expected, and to use the term “concurrent” when it is uncertain or irrelevant

### Stateful & state-management
_Let's see who is under this hood... *reveals good ol' mutators_

So i know you guys love the glorify state management and therefore support the modern frameworks but are you aware that you can do state management rather easily ?

might add the code later

### Webhook vs WebSocket
- Webhook is for server-to-server in essence. One way communication. One receiver, one sender. Kinda like a reverse API
- Websocket is intended for server-to-browser. Long-polling, different than http protocol.
