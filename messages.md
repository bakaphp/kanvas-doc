# Messages Module

The Messages module in the Kanvas Core SDK provides comprehensive functionality for managing messages within the Kanvas ecosystem. This module enables creating, updating, deleting, and querying messages, as well as handling interactions like likes and topic associations.

## Key Features

- Create, update, and delete messages
- Query messages with advanced filtering
- Handle message interactions (like, save, share)
- Attach and detach topics to messages
- Manage message comments

## Usage

Access the Messages module through the `messages` property on your KanvasCore instance:

```typescript
const kanvas = new KanvasCore({...});
const messages = kanvas.messages;
```

## Core Methods

### createMessage(input: MessageInputInterface): Promise<MessagesInterface>

Creates a new message.

```typescript
const newMessage = await messages.createMessage({
  message_verb: 'post',
  message: 'Hello, Kanvas!',
  system_modules_id: 'module123',
  entity_id: 'entity456',
  distribution: {
    distributionType: 'public',
    channels: ['general'],
    followers: []
  }
});
console.log(newMessage.id);
```

Returns a `MessagesInterface` object representing the created message.

### updateMessage(id: string, input: MessageUpdateInputInterface): Promise<MessagesInterface>

Updates an existing message.

```typescript
const updatedMessage = await messages.updateMessage('msg123', {
  message: 'Updated: Hello, Kanvas!'
});
console.log(updatedMessage.message);
```

Returns the updated `MessagesInterface` object.

### deleteMessage(id: string): Promise<Boolean>

Deletes a message.

```typescript
const isDeleted = await messages.deleteMessage('msg123');
console.log(isDeleted); // true if successful
```

### getMessages(where: WhereCondition, hasAppModuleMessageWhere: HasAppModuleMessageWhereConditions, orderBy: Array<OrderByMessage>, search: string, first: number, page: number): Promise<MessagesInterface[]>

Retrieves messages based on specified criteria.

```typescript
const recentMessages = await messages.getMessages(
  { column: 'CREATED_AT', operator: 'GT', value: '2023-01-01' },
  { column: 'ENTITY_ID', operator: 'EQ', value: 'entity456' },
  [{ column: 'CREATED_AT', order: 'DESC' }],
  'search term',
  10,
  1
);
console.log(recentMessages);
```

Returns an array of `MessagesInterface` objects.

### interactionMessage(id: string, type: InteractionTypeInput): Promise<MessagesInterface>

Handles user interactions with a message (like, save, share, report).

```typescript
const interactedMessage = await messages.interactionMessage('msg123', InteractionTypeInput.LIKE);
console.log(interactedMessage.total_liked);
```

Returns the updated `MessagesInterface` object.

### attachTopicToMessage(messageId: string, topicId: string): Promise<void>

Attaches a topic to a message.

```typescript
await messages.attachTopicToMessage('msg123', 'topic456');
```

### detachTopicToMessage(messageId: string, topicId: string): Promise<void>

Detaches a topic from a message.

```typescript
await messages.detachTopicToMessage('msg123', 'topic456');
```

## Message Comments

The Messages module includes a sub-module for managing comments:

```typescript
const comments = messages.comments;
```

### comments.addComment(input: MessageCommentInputInterface): Promise<MessageCommentsInterface>

Adds a comment to a message.

```typescript
const newComment = await comments.addComment({
  message_id: 'msg123',
  message: 'Great post!',
  parent_id: null // for top-level comments
});
console.log(newComment.id);
```

### comments.updateComment(id: string, input: MessageCommentInputInterface): Promise<MessageCommentsInterface>

Updates an existing comment.

```typescript
const updatedComment = await comments.updateComment('comment789', {
  message: 'Updated: Great post!'
});
console.log(updatedComment.message);
```

### comments.deleteComment(id: string): Promise<MessageCommentsInterface>

Deletes a comment.

```typescript
await comments.deleteComment('comment789');
```

### comments.getComments(where: WhereCondition, first: number, page?: number): Promise<MessageCommentsInterface[]>

Retrieves comments for a message.

```typescript
const messageComments = await comments.getComments(
  { column: 'MESSAGE_ID', operator: 'EQ', value: 'msg123' },
  10,
  1
);
console.log(messageComments);
```

## Best Practices

1. Use pagination when fetching messages to optimize performance.
2. Implement proper error handling for all message operations.
3. Use meaningful message verbs to categorize different types of messages.
4. Regularly clean up or archive old messages to maintain system performance.
5. Implement rate limiting for message creation to prevent spam.
6. Use topics effectively to organize and categorize messages.

## Troubleshooting

- **Message Creation Failures**: Ensure all required fields are provided and valid.
- **Interaction Issues**: Verify that the user has permission to interact with the message.
- **Query Performance**: Use appropriate filters and pagination for large message sets.
- **Comment Threading**: Be mindful of deeply nested comment threads and their potential impact on performance.

## Error Handling

Implement try/catch blocks for all message operations:

```typescript
try {
  await messages.createMessage(messageData);
} catch (error) {
  console.error('Failed to create message:', error.message);
  // Handle error (e.g., show user feedback, log error)
}
```

Common error scenarios:
- Invalid input data
- Unauthorized access
- Network failures
- Rate limiting

## Security Considerations

1. Implement strict access controls for message operations.
2. Sanitize message content to prevent XSS attacks.
3. Implement spam detection and prevention mechanisms.
4. Use rate limiting to prevent abuse of message creation or interaction APIs.
5. Regularly audit message interactions for suspicious activity.

## Integration Tips

1. Combine with the Users module for user-specific message feeds.
2. Utilize the Topics module for better message categorization and discovery.
3. Integrate with a notification system to alert users of new messages or interactions.
4. Use webhooks to sync important messages with external systems.

## Advanced Usage

### Custom Message Feed

Implement a custom message feed with filtering and personalization:

```typescript
async function getPersonalizedFeed(userId: string, interests: string[], page: number = 1, pageSize: number = 20) {
  const userTopics = await getUserTopics(userId); // Implement this based on your user-topic association
  
  return messages.getMessages(
    { 
      OR: [
        { column: 'USER_ID', operator: 'EQ', value: userId },
        { column: 'IS_PUBLIC', operator: 'EQ', value: true }
      ]
    },
    { 
      column: 'TOPIC_ID', 
      operator: 'IN', 
      value: [...userTopics, ...interests] 
    },
    [{ column: 'CREATED_AT', order: 'DESC' }],
    '',
    pageSize,
    page
  );
}

// Usage
const feed = await getPersonalizedFeed('user123', ['technology', 'science'], 1, 10);
console.log(feed);
```

### Message Analytics

Implement analytics for message engagement:

```typescript
async function getMessageEngagement(messageId: string) {
  const message = await messages.getMessages(
    { column: 'ID', operator: 'EQ', value: messageId },
    {},
    [],
    '',
    1,
    1
  );

  if (message.length === 0) throw new Error('Message not found');

  const comments = await messages.comments.getComments(
    { column: 'MESSAGE_ID', operator: 'EQ', value: messageId },
    1000 // Adjust as needed
  );

  return {
    messageId,
    likes: message[0].total_liked,
    shares: message[0].total_shared,
    comments: comments.length,
    engagementRate: calculateEngagementRate(message[0], comments.length)
  };
}

function calculateEngagementRate(message, commentCount) {
  // Implement your engagement rate calculation logic
  // For example: (likes + shares + comments) / viewCount
  return ((message.total_liked + message.total_shared + commentCount) / message.view_count) * 100;
}

// Usage
const engagement = await getMessageEngagement('msg123');
console.log(engagement);
```

### Bulk Message Operations

Implement bulk operations for efficient message management:

```typescript
async function bulkCreateMessages(messagesData: MessageInputInterface[]) {
  return Promise.all(messagesData.map(data => messages.createMessage(data)));
}

async function bulkDeleteMessages(messageIds: string[]) {
  return Promise.all(messageIds.map(id => messages.deleteMessage(id)));
}

// Usage
const newMessages = await bulkCreateMessages([
  { message_verb: 'post', message: 'Bulk message 1', system_modules_id: 'mod1', entity_id: 'ent1' },
  { message_verb: 'post', message: 'Bulk message 2', system_modules_id: 'mod1', entity_id: 'ent2' }
]);

await bulkDeleteMessages(['msg1', 'msg2', 'msg3']);
```

By effectively utilizing the Messages module, you can create a robust messaging system within your Kanvas-powered application. This module enables you to build complex social features, implement engagement tracking, and create personalized content experiences for your users.
