# Message Types Module

The Message Types module in the Kanvas Core SDK provides functionality for managing and querying different types of messages within the Kanvas ecosystem. This module allows for the creation, updating, and retrieval of message types, enabling a more structured and categorized approach to messaging.

## Key Features

- Create new message types
- Update existing message types
- Retrieve message types with filtering capabilities
- Support for multilingual message templates

## Usage

Access the Message Types module through the `messagesTypes` property on your KanvasCore instance:

```typescript
const kanvas = new KanvasCore({...});
const messageTypes = kanvas.messagesTypes;
```

## Core Methods

### createMessageType(input: MessageTypeInputInterface): Promise<MessageTypeInterface>

Creates a new message type.

```typescript
const newMessageType = await messageTypes.createMessageType({
  languages_id: 1,
  name: 'System Notification',
  verb: 'notify',
  template: 'System: {{message}}',
  templates_plura: 'System: {{message}} ({{count}} notifications)'
});
console.log(newMessageType.id);
```

Parameters:
- `input`: MessageTypeInputInterface object containing message type details

Returns a `MessageTypeInterface` object representing the created message type.

### updateMessageType(id: number, input: MessageTypeInputInterface): Promise<MessageTypeInterface>

Updates an existing message type.

```typescript
const updatedMessageType = await messageTypes.updateMessageType(123, {
  name: 'Updated System Notification',
  template: 'System Update: {{message}}'
});
console.log(updatedMessageType.name);
```

Parameters:
- `id`: Message type ID
- `input`: MessageTypeInputInterface object with updated details

Returns the updated `MessageTypeInterface` object.

### getMessageTypes(where?: WhereCondition): Promise<MessageTypeInterface[]>

Retrieves message types based on specified criteria.

```typescript
const systemMessageTypes = await messageTypes.getMessageTypes({
  column: 'NAME',
  operator: 'LIKE',
  value: '%System%'
});
console.log(systemMessageTypes);
```

Parameters:
- `where`: Optional query conditions for filtering message types

Returns an array of `MessageTypeInterface` objects.

## Interfaces

### MessageTypeInputInterface

```typescript
interface MessageTypeInputInterface {
  languages_id: number;
  name: string;
  verb: string;
  template: string;
  templates_plura: string;
}
```

### MessageTypeInterface

```typescript
interface MessageTypeInterface {
  id: number;
  languages_id: number;
  apps_id: number;
  uuid: string;
  name: string;
  verb: string;
  description: string;
  templates_plura: string;
}
```

## Best Practices

1. Use descriptive names and verbs for message types to ensure clarity.
2. Implement a consistent naming convention for message types across your application.
3. Utilize templates effectively to create dynamic and context-aware messages.
4. Consider internationalization needs when creating message types and templates.
5. Regularly audit and update message types to ensure they remain relevant and effective.
6. Use message types consistently across your application to maintain a unified messaging experience.

## Troubleshooting

- **Duplicate Message Types**: Ensure unique combinations of name and verb to avoid conflicts.
- **Template Rendering Issues**: Verify that all placeholders in templates are properly defined and used.
- **Localization Problems**: Check that language IDs are correct and templates are properly localized.

## Error Handling

Implement try/catch blocks for all message type operations:

```typescript
try {
  await messageTypes.createMessageType(newMessageTypeData);
} catch (error) {
  console.error('Failed to create message type:', error.message);
  // Handle error (e.g., show user feedback, log error)
}
```

Common error scenarios:
- Invalid input data
- Duplicate message type
- Language not found
- Network failures

## Security Considerations

1. Implement proper access controls for message type management.
2. Validate and sanitize all input data, especially template strings, to prevent injection attacks.
3. Be cautious about exposing sensitive information in message templates.
4. Implement logging for message type operations for audit purposes.

## Integration Tips

1. Combine with the Messages module to create a robust messaging system.
2. Utilize message types in conjunction with the Notifications module for structured notifications.
3. Integrate with a localization system for managing multilingual message templates.
4. Use message types to categorize and filter messages in user interfaces.

## Advanced Usage

### Dynamic Template Rendering

Implement a function to render message templates dynamically:

```typescript
function renderMessageTemplate(template: string, data: Record<string, any>): string {
  return template.replace(/\{\{(\w+)\}\}/g, (match, key) => data[key] || match);
}

// Usage
const messageType = await messageTypes.getMessageTypes({ column: 'VERB', operator: 'EQ', value: 'notify' })[0];
const renderedMessage = renderMessageTemplate(messageType.template, { message: 'Server maintenance scheduled' });
console.log(renderedMessage);
```

### Bulk Message Type Operations

Implement bulk operations for efficient management:

```typescript
async function bulkCreateMessageTypes(typesData: MessageTypeInputInterface[]) {
  return Promise.all(typesData.map(data => messageTypes.createMessageType(data)));
}

async function bulkUpdateMessageTypes(updates: Array<{id: number, data: Partial<MessageTypeInputInterface>}>) {
  return Promise.all(updates.map(({id, data}) => messageTypes.updateMessageType(id, data)));
}

// Usage
const newTypes = await bulkCreateMessageTypes([
  { languages_id: 1, name: 'User Welcome', verb: 'welcome', template: 'Welcome, {{username}}!', templates_plura: 'Welcome, new users!' },
  { languages_id: 1, name: 'Order Confirmation', verb: 'confirm_order', template: 'Your order #{{order_id}} is confirmed.', templates_plura: 'Orders confirmed.' }
]);

await bulkUpdateMessageTypes([
  { id: 1, data: { template: 'Updated: Welcome, {{username}}!' } },
  { id: 2, data: { name: 'Updated Order Confirmation' } }
]);
```

### Message Type Analytics

Implement analytics to track usage of different message types:

```typescript
async function getMessageTypeUsage(timeRange: { start: Date, end: Date }) {
  const allTypes = await messageTypes.getMessageTypes();
  const usage = await Promise.all(allTypes.map(async type => {
    const count = await getMessageCountByType(type.id, timeRange); // Implement this based on your data structure
    return { id: type.id, name: type.name, count };
  }));

  return usage.sort((a, b) => b.count - a.count);
}

// Usage
const typeUsage = await getMessageTypeUsage({ start: new Date('2023-01-01'), end: new Date() });
console.log('Most used message types:', typeUsage.slice(0, 5));
```

By effectively utilizing the Message Types module, you can create a structured and flexible messaging system within your Kanvas-powered application. This module enables you to categorize messages, implement dynamic templates, and support multilingual content, enhancing the overall communication capabilities of your platform.
