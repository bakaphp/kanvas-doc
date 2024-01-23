## Notification

This is a list of method available in the Kanvas Core JS SDK from Notifications.

## Methods

- [Get Notifications](#get-notifications)

## Get Notifications

The getNotifications method fetches all notifications associated with the user. This method has 4 params,
 [WhereConditions](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/leads.ts#L122),
 [whereEntity](https://github.com/bakaphp/kanvas-core-js/blob/7c8288d93b786f08aabe2d6f16a390ba75b41148/src/types/notification.ts#L44),[whereType](https://github.com/bakaphp/kanvas-core-js/blob/7c8288d93b786f08aabe2d6f16a390ba75b41148/src/types/notification.ts#L49), first number, page number.
 It returns an array of [NotificationInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/notification.ts#L5)


```js
Kanvas.notification.getNotifications(
  whereConditions: WhereConditions,
  whereEntity: whereEntity,
  whereType: whereType,
  first: number,
  page: number
): NotificationInterface[]
```

**Example:**

```js
const notifications = Kanvas.notifications.getNotifications();
```

## Get Notifications Types

The getNotificationsTypes method fetches all notifications types associated with the user.
The method has 3 params,  [WhereConditions](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/leads.ts#L122),first number, page number.
It returns an array of [NotificationTypeInterface]()

```js
Kanvas.notifications.getNotificationsTypes(
  whereConditions: WhereConditions,
  first: number,
  page: number
): NotificationTypeInterface[]
```

**Example:**

```js
const notificationsTypes = Kanvas.notifications.getNotificationsTypes();
```

## Read All Notification
The readAllNotification method is used to read all notifications associated with the user.
It returns a boolean.

```js
Kanvas.notifications.readAllNotifications(): boolean
```

**Example:**

```js
const readAllNotifications = Kanvas.notifications.readAllNotifications();
```

## Sent Notification Based on Template
The sentNotificationBasedOnTemplate method is used to send a notification based on a template.
It receives a template string, data as any, via as array of string and user as array of number.
It returns a boolean.

```js
Kanvas.notifications.sentNotificationBasedOnTemplate(
  template: string,
  data: any,
  via: string[],
  user: number[]
): boolean
```

**Example:**

```js
const sentNotificationBasedOnTemplate = Kanvas.notifications.sentNotificationBasedOnTemplate(
  'template',
  'data',
  ['via'],
  [1]
);
```

## Sent Notification By Message
The sentNotificationByMessage method is used to send a notification by message.

It receives a message string, via as array of string and user as array of number. 
It returns a boolean.

```js
Kanvas.notifications.sentNotificationByMessage(
  message: string,
  via: string[],
  user: number[]
): boolean
```

**Example:**

```js
const sentNotificationByMessage = Kanvas.notifications.sentNotificationByMessage(
  'message',
  ['via'],
  [1]
);
```