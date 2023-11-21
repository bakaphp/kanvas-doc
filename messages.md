## Messages

The Messages class in the Kanvas Core JS SDK provides methods for interacting with messages.

## Create Message

This method allows you to create a new message. It receive a [MessageInputInterface]() interface and returns a [MessageInterface]() interface.

```js
Kanvas.messages.createMessage(messageInput: MessageInputInterface): MessageInterface
```

**Example:**

```js
let message = {
  message_types_id: 1, // 1 is a single message
  message: "This is a test message", // this can be a string or a json object encoded as a string
  system_modules_id: 1, // this is the system module id for the memos
  entity_id: 1, // this is the entity is from the serverless server
  distribution: {
    distributionType: "ALL",
  },
};
const newMessage = Kanvas.messages.createMessage(message);
```

## Get Messages

This method allows you to get messages from the server. It receive the parameters

- where: [MessageWhereConditions]()
- hasAppModuleMessageWhere: [HasAppModuleMessageWhereConditions](),
- orderBy: [OrderByMessage[]](),
- search: [string](),
- first: [number](),
- page: [number]()

and returns a [MessageInterface[]]() interface.

```js
Kanvas.messages.getMessages(
    where: MessageWhereConditions,
    hasAppModuleMessageWhere: HasAppModuleMessageWhereConditions,
    orderBy: OrderByMessage[],
    search: string,
    first: number,
    page: number
): MessageInterface[]
```

**Example:**

```js
const messages = Kanvas.messages.getMessages({
    where: MessageWhereConditions,
    hasAppModuleMessageWhere: HasAppModuleMessageWhereConditions,
    orderBy: OrderByMessage[],
    search: string,
    first: number,
    page: number
});
```

## Interact with Messages

This method allows you to interact with messages. Send likes, share, unlike and report. It receive the parameters ID of the message and [InteractionType]() interface.

```js
Kanvas.messages.interactWithMessage(
    id: string,
    type: InteractionType
): MessageInterface
```

**Example:**

```js
const message = Kanvas.messages.interactWithMessage(
    id: string,
    type: InteractionType
);
```

## Attach Topic to Message

This method allows you to attach a topic to a message. It receive the parameters ID of the message and ID of Topic.

```js
Kanvas.messages.attachTopicToMessage(
    messageId: string,
    topicId: string
): MessageInterface
```

**Example**

```js
Kanvas.messages.attachTopicToMessage(
    messageId: string,
    topicId: string
);
```

## Detach Topic from Message

This method allows you to detach a topic from a message. It receive the parameters ID of the message and ID of Topic.

```js
Kanvas.messages.detachTopicFromMessage(
    messageId: string,
    topicId: string
): MessageInterface
```

**Example**

```js
Kanvas.messages.detachTopicFromMessage(
    messageId: string,
    topicId: string
);
```
