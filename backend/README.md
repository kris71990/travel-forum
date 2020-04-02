# Travel Forum - server

**Author:** Kris Sakarias

**Version** 1.0.0


## Overview

This is the API used to serve as the backend to a travel forum where users can interract with eachother about travel topics, concerns, advice, etc.

It is built with *Node* and *Express*, data is structured in a relational database using *PostgreSQL* and handled with *Sequelize*. *Mocha* and *Chai* are used for unit testing. *Socket.io* is used to authenticate user activity in the Chat Room.


## Database Models

```
Account - (1:1) -> Profile
```

```
Country - (1:many) -> Thread - (1:many) -> Comment
```

```
Profile - (1:many) -> Thread
        - (1:many) -> Comment
```

Data is stored in a relational database because of strict relationships between models.

Each user account is associated with a profile. Each country can have zero or many threads, and each thread can have zero or many comments. Each profile can have zero or many threads (threads started by user) and zero or many comments (comments posted by user to any existing thread).


## Documentation

*Account Router*
1. POST /signup
  - User signup with `username`, `password`, `email`
  - Creates user account and authenticates user with token returned by cookie

2. GET /login
  - User login with `username` and `password`
  - Logs user in if credentials are validated by returning token by cookie


*Profile Router*
1. POST /profile - AUTH
  - Always called immediately after user signup
  - with `username`, profile is created and `totalThreads`, `totalComments`, and `totalPosts` initialized to zero`

2. GET /profile/me - AUTH
  - Finds and returns user profile associated with user account (`accountId`)

3. PUT /profile/:profileId - AUTH
  - Called after user posts a thread or comment
  - When thread is posted...
    - `totalThreads` and `totalPosts` is incrememnted
  - When comment is posted...
    - `totalComments` and `totalPosts` is incremented


*Country Router*
1. POST /country - AUTH
  - User can add a country repository to the forum
  - Must accept `name` and `continent`
  - Initializes `threadCount` to zero

2. GET /countries - PUBLIC
  - Finds and returns all countries with specified `continentId`
  - Called on homepage of forum to display list of country subforums organized by region

3. PUT /country/:countryId - AUTH
  - Called after user posts a thread in a country subforum
  - Increments `threadCount`


*Thread Router*
1. POST /thread - AUTH
  - User can post a thread in a country subforum
  - Must accept `title` and `text`, `commentCount` initialized to zero
  - Thread is associated with a user profile (`profileId`) and country (`countryId`)

2. GET /threads - PUBLIC
  - Finds and returns all threads in a country (`countryId`)
  - Called when user opens country subforum

3. PUT /thread/:threadId - AUTH
  - Called on two separate occasions...
    1. On user edit of thread `title` or `text`
    2. When a comment for the thread is submitted, `commentCount` is incremented


*Comment Router*
1. POST /comment - AUTH
  - User can submit a comment for a thread
  - Must accept `text`
  - Comment is associated with user profile (`profileId`) and thread (`threadId`)

2. GET /comments - PUBLIC
  - Called when user navigates to thread
  - Finds and returns all comments associated with thread (`threadId`)

3. PUT /comment/:commentId - AUTH
  - Called when user updates `text` of comment

4. DELETE /comment/:commentId - AUTH
  - Called when user requests to delete a comment


*Message Router*
1. POST /message - AUTH
  - User can send a private message to another user
  - Must accept `text`, user profileId and recipient profileId

2. GET /messages - AUTH
  - User can get all messages that have been sent to them

3. PUT /message/:messageId
  - Called when user reads a message for the first time, `read` flag set to true

  

## Testing

Unit testing is done with *Mocha* and *Chai* - 96% coverage of server code.


