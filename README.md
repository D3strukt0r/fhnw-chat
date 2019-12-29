# Chat

Java project for running the client part of the chat program

## Features

Use a console version or GUI version. When running there are additional options (check the usage part).

### Basic features: Functionality
* ✔ Set server address and port
* ✔ Create new login
* ✔ Change password
* ✔ Delete account
* ✔ Login
* ✔ Logout
* ✔ List chatrooms
* ✔ Join a particular chatroom
* ✔ See messages in the chatroom
* ✔ Send a message to the chatroom
 
### Basic features: Architecture and GUI
* ✔ MVC structure: Separate the UI from the logic
* ✔ Multilingual application: English, German, Italian, French
* ✔ Reasonable user interface
* ✔ Platform independent
* ✔ User errors do not crash the program
* ✔ Controls enable/disable as appropriate

### Optional: Contacts and private messaging
#### Simple: Maintain a list of contacts
* ❌ Display status of contact
* ✔ Be able to send/receive private messages to a contact
* ✔ How will you distinguish private messages from public chat? Different tabs!
#### Advanced: Maintain a block list
* ❌ Users whose private messagaes will be ignored
* ❌ Users whose chat room messages will not be displayed
* ❌ Are these the same users, or two different lists?

### Optional: GUI features
#### Simple: Implement a nice GUI
* ✔ Nice design, good use of color
* ✔ Good error messages
* ✔ Sensible resizing behavior
* ✔ All controls enabled/disabled when it makes sense
#### Advanced: “Wow” factor
* ✔ Subjective…
* ❌ For example: animations for user feedback

### Optional: Chat room usability features
#### Simple
* ❌ Logout / Login – pick up where you left off (Annoying feature)
* ❌ Display list of users in the chatroom

#### Advanced
* ✔ Be able to join multiple chat rooms
* ❌ Manage a private chat room (Add and remove users)

### Optional: Further features
* ✔ Maintain long-term history of chats
* ❌ Be able to select portion of chat to look at
* ❌ Offer search/filter functionality – by user, by content, by date

## Installation

Import to your IDE and run

## Usage

When running you can add following options:

| Short | Long          | Description                                                                   |
|-------|---------------|-------------------------------------------------------------------------------|
| -g    | --no-gui      | Uses the console as interface instead of a window                             |
| -d    | --no-db       | Don't use the internal db. Data will never be saved.                          |
| -l    | --db-location | If using a DB (by default on), use a custom location for the file             |
| -v    | --verbose     | Show more information in the console. Useful for debuggin and finding errors. |

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

# Documentation

 * Official site: http://javaprojects.ch
 * Official ip: 147.86.8.31
 * Official port: 50001

## Client -> Server

| MessageType       | Data               | Notes                                                                                                         |
|-------------------|--------------------|---------------------------------------------------------------------------------------------------------------|
| CreateLogin       | Username, Password | Fails if name already taken (user or chatroom), or invalid After creating an account, you still have to login |
| Login             | Username, Password | Fails if name/password do not match                                                                           |
| ChangePassword    | New password       | Fails only if token is invalid                                                                                |
| DeleteLogin       | -                  | Fails only if token is invalid; after delete, token becomes invalid                                           |
| Logout            | -                  | Never fails; token becomes invalid                                                                            |
| CreateChatroom    | Name, isPublic     | Fails if name already taken (user or chatroom), or invalid After creating a chatroom, you still have to join  |
| JoinChatroom      | Chatroom, User     | User can add themselves to public chatrooms Only the creator can add user to a private chatroom               |
| LeaveChatroom     | Chatroom, User     | You can always remove yourself Chatroom creator can remove anyone                                             |
| DeleteChatroom    | Chatroom           | Only the creator can delete a chatroom                                                                        |
| ListChatrooms     | -                  | Returns a list of all public chatrooms                                                                        |
| Ping              | [Token]            | Without a token: always succeeds With token: succeeds only if token is valid                                  |
| SendMessage       | Target, Message    | Send message to user or chatroom Fails if user not online / Fails if not a member of the chatroom             |
| UserOnline        | User               | Succeeds if the user is currently logged in                                                                   |
| ListChatroomUsers | Chatroom           | Returns a list of all users in the given chatroom You must be a member of this chatroom                       |

## Client <- Server

### Responses to client commands

| MessageType  | Data                               | Notes                                                                                                                                                              |
|--------------|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Result       | Boolean Boolean Token Boolean List | True if the command succeeded, otherwise false After a successful login, also returns the authentication token When a list is requested, also returns list results |
| MessageError | Error message                      | Incorrect commands, wrong number of arguments, etc.                                                                                                                |

### Server initiated messages

| MessageType | Data               | Notes                                                                                                    |
|-------------|--------------------|----------------------------------------------------------------------------------------------------------|
| MessageText | Name, Target, Text | Name of user sending message Target is where the message was sent (chatroom or user) Text of the message |

## License
[MIT](LICENSE.txt)
