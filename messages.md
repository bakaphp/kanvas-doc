## Messages
The Messages class within the Kanvas Core JS SDK offers methods designed for interacting with messages.

## Methods
- [Create Message](#create-message)
- [Get Messages](#get-messages)
- [Interact with Messages](#interact-with-messages)
- [Attach Topic to Message](#attach-topic-to-message)
- [Detach Topic from Message](#detach-topic-from-message)


## Create Message

This method enables the creation of a new message. It recievess a [MessageInputInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/messages.ts#L19) interface as input and returns a [MessageInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/messages.ts#L2) interface.

```js
Kanvas.messages.createMessage(messageInput: MessageInputInterface): MessageInterface
```

**Example:**

```js
let message = {
  message_verb: "verb", // 1 is a single message
  message: "This is a test message", // this can be a string or a json object encoded as a string
  system_modules_id: 1, // this is the system module id for the memos
  entity_id: 1, // this is the entity is from the serverless server
  distribution: {
    distributionType: "ALL",
  },
};
const newMessage = Kanvas.messages.createMessage(message);
```

## Update Message
This method enables the update a existing message. It recievess a id string input and a  [MessageUpdateInputInterface](https://github.com/bakaphp/kanvas-core-js/blob/6321d44a068674efa0f68c6161a1ed32d5dbcf62/src/types/messages.ts#L28) interface as input then it returns a [MessageInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/messages.ts#L2) interface.

```js
Kanvas.messages.updateMessage(id: string, messageInput: MessageUpdateInputInterface): MessageInterface
```

**Example:**

```js
let message = {
  message: "You only can update the message verb", // 1 is a single message
};
const message = Kanvas.messages.updateMessage(id: 21, message);
```


## Get Messages

This method facilitates the retrieval of messages from the server. It accepts the following parameters

- where: [WhereCondition](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/leads.ts#L122)
- hasAppModuleMessageWhere: [HasAppModuleMessageWhereConditions](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/messages.ts#L42),
- orderBy: [OrderByMessage[]](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/messages.ts#L48),
- search: string,
- first: number,
- page: number

and returns a [MessageInterface[]](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/messages.ts#L2) interface.

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

This method allows you to interact with messages, such as sending likes, sharing, unliking, and reporting. It takes the message ID and [InteractionTypeInput interface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/messages.ts#L53) as parameters.

```js
Kanvas.messages.interactWithMessage(
    id: string,
    type: InteractionTypeInput
): MessageInterface
```

**Example:**

```js
const message = Kanvas.messages.interactWithMessage(
    id: string,
    type: InteractionTypeInput
);
```

## Attach Topic to Message

This method enables you to associate a topic with a message. It requires the message ID and topic ID as parameters.

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

This method allows you to detach a topic from a message. It requires the message ID and topic ID as parameters.

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
