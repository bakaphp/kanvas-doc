## Message Types

The message types are used to create, update, and delete messages. However, it's beneficial to perceive this module as a system class or a system entity, akin to the concept introduced in the System Module, though not identical (Note by backend dev: I'm not entirely certain about the meaning, but I'm currently contemplating this; it might undergo changes in the future).

To illustrate, consider the following scenario: your application records user clicks on ads, and you aim to preserve each click within our ecosystem. To achieve this, you would define a message type named 'click.' Subsequently, you can generate a message with the type 'click' and include the pertinent data that you wish to retain.

## Methods

- [Create Message Type](#create-message-type)
- [Update Message Type](#update-message-type)
- [Get Message Types](#get-message-types)

## Create Message Type

The createMessageType method is utilized for the creation of a new message type. It accepts a MessageTypeInput interface as input and yields a MessageType interface as output.


```js
    kanvas.messagesTypes.createMessageType(input: MessageTypeInputInterface): MessageTypeInterface
```

**Example:**

```js
    const input = {
        languages_id: 1;
        name: "name";
        verb: "verb";
        template: "template";
        templates_plura: "template";
    };
    const newMessageType = kanvas.messagesTypes.createMessageType(input);
```

## Update Message Type

The updateMessageType method serves to modify an existing message type. It takes a numerical id and a MessageTypeInput interface as parameters and subsequently returns a MessageType interface.

```js
    kanvas.messagesTypes.updateMessageType(input: MessageTypeInputInterface): MessageTypeInterface
```

**\*Example:**

```js
    const input = {
        languages_id: 1;
        name: "name";
        verb: "verb";
        template: "template";
        templates_plura: "template";
    };
    const updatedMessageType = kanvas.messagesTypes.updateMessageType(id, input);
```

## Get Message Types

The getMessageTypes method is employed to fetch all message types. It accepts the whereConditions as parameters and returns an array of MessageType interfaces.

```js
    kanvas.messagesTypes.getMessageTypes(
        where: WhereConditions,
    ): MessageTypeInterface[]
```

**Example:**

```js
    const messageTypes = kanvas.messagesTypes.getMessageTypes(where);
```