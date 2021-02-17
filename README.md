# Purpose
- _To improve remote team building_
- A back-end service for a real-time, turn-based multiplayer game (named `Facts!`) that solves the client's problem of improving remote team building

# How to run
- Install Node.js
- Clone this repo
- `cd` into the `paragon-back-end-mirror` directory and then `npm i`
- `npm run dev-ws` to run the application locally

# Tools used
- Core application:
  - Node.js
  - WebSockets
  - Node.js `http` core module
  - Node package `ws`
  - Node packages: `nanoid`, `uuid`
  - Node package `joi`
  - Node package `jsonwebtoken`
  - Node package `jwk-to-pem`
  - AWS SDK
  - AWS DynamoDB
  - Nodemon (for development only)
  - Prettier, ESLint (for development only)
- Testing:
  - Jest
- Project management:
  - Jira, Confluence, Trello

# What I learned
- Practiced producing and delivering software using agile methodology, whilst working in a fully distributed/remote team.
- Communicating regularly and precisely with team members is key, especially regarding blockers or delays.
- Conducting user research and creating user stories helps keep in mind the original problem throughout the process. User stories can be helpful to refer to, especially when making difficult decisions during the course of the project.
- Using Jira effectively to manage tasks, backlogs and sprints. We each took turns to assume the role of project manager. This helped us ensure the project was managed well and remained on schedule.
- Learned the benefits of a design/approach where the server:
  - is the authoritative, single source of truth for a game's state
  - controls what and when information is delivered to authenticated clients
  - allows authenticated clients to update game state in limited, controlled, validated ways.
- Became more familiar AWS console (particularly AWS CloudWatch for logging) and AWS SDK for Node.js.
- Learned about using WebSockets for bi-directional communication between the client and server. This was extremely useful for this application as it allowed changes in game state to be pushed to the client (as opposed to the client polling the server which can be inefficient).
- Learned about NoSQL databases and the importance of defining access patterns upfront, so that reads/writes remain performant.
- Learned how to use AWS Dynamo DB for:
  - persisting game state
  - the importance of using `ConditionExpressions` to combine a check and write (where the write is dependent on the check) into a single request. Otherwise, if the check and update are done in separate requests, the database's state can change between the check and update -- which can result in non-deterministic behaviour, tricky race conditions or the game being left in an incoherent state.
  - using `UpdateExpressions` to ensure that writes which are relative to the "current value" are done in one request.
- Using Joi for validation (at runtime) of objects being read from or written to the database -- which is more important with NoSQL databases where only the partition key (and sort key if applicable) will be checked by the database service.

# Things to add
- Explore how feasible it would be to make this back-end serverless by using:
  - AWS API gateway (WebSocket API)
  - AWS Lambda
  - AWS SQS (FIFO) to decouple the production and consumption of events
- Introduce concept of achievements e.g. awards for answering questions quickly/correctly/accurately/consistently.

# Created
Dec 2020 - Jan 2021 (4-week deadline)