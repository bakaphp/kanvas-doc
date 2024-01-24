## Notification

This is a list of method available in the Kanvas Core JS SDK from Notifications.

## Methods

- [Get Notifications](#get-notifications)
- []

## Get Notifications

The `getNotifications` method is responsible for retrieving all notifications associated with a user. This method takes four parameters:

1. **WhereConditions:** Defined [here](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/leads.ts#L122).
2. **WhereEntity:** Referenced [here](https://github.com/bakaphp/kanvas-core-js/blob/7c8288d93b786f08aabe2d6f16a390ba75b41148/src/types/notification.ts#L44).
3. **WhereType:** Also detailed [here](https://github.com/bakaphp/kanvas-core-js/blob/7c8288d93b786f08aabe2d6f16a390ba75b41148/src/types/notification.ts#L49).
4. The first number.
5. The page number.

The method returns an array of objects conforming to the [NotificationInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/notification.ts#L5) structure.


```ts
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
let notifications = await kanvas.notifications.getNotifications({
  column: "READ",
  operator: "EQ",
  value: 1,
});
```

## Get Notifications Types

The `getNotificationsTypes` method is utilized to retrieve all notification types associated with a user. This method requires three parameters:

1. **WhereConditions:** Defined [here](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/leads.ts#L122).
2. The first number.
3. The page number.

The method returns an array of objects adhering to the [NotificationTypeInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/notification.ts#L5) structure.

```ts
Kanvas.notifications.getNotificationsTypes(
  whereConditions: WhereConditions,
  first: number,
  page: number
): NotificationTypeInterface[]
```

**Example:**

```js
let notificationTypes = await kanvas.notifications.getNotificationTypes({
  column: "NAME",
  operator: "LIKE",
  value: "kanvas%",
});
```

## Read All Notification

The readAllNotification method is employed to mark all notifications associated with the user as read. This method does not require any parameters. It simply performs the action and returns a boolean value indicating the success of the operation.

After calling this method, notifications that were previously unread will be marked as read. The returned boolean value can be used to verify the success of the operation.

```ts
Kanvas.notifications.readAllNotifications(): boolean
```

**Example:**

```js
const readAllNotifications = await Kanvas.notifications.readAllNotifications();
```

## Sent Notification Based on Template

The `sentNotificationBasedOnTemplate` method is utilized to send a notification based on a predefined template. This method takes the following parameters:

1. **template:** A string representing the template to be used.
2. **data:** An object of any type, containing data to be incorporated into the template.
3. **via:** An array of strings specifying the delivery method(s) for the notification.
4. **user:** An array of numbers indicating the user(s) to whom the notification will be sent.

The method executes the notification sending process and returns a boolean value, indicating the success of the operation.

Ensure to provide the necessary values for each parameter to effectively send notifications based on the specified template. The returned boolean can be used to confirm the success of the operation.

```ts
Kanvas.notifications.sentNotificationBasedOnTemplate(
  template: string,
  data: any,
  via: string[],
  user: number[]
): boolean
```

**Example:**

```js
await kanvas.notifications.sendNotificationBaseTemplate(
  "welcome",
  {
    name: "hello",
  },
  "mail",
  [10]
);
```

## Sent Notification By Message

The `sentNotificationByMessage` method serves the purpose of sending a notification through a custom message. This method requires the following parameters:

1. **message:** A string representing the content of the notification message.
2. **via:** An array of strings specifying the delivery method(s) for the notification.
3. **user:** An array of numbers indicating the user(s) to whom the notification will be sent.

Upon execution, the method initiates the notification sending process and returns a boolean value, indicating the success of the operation.

Ensure to provide the necessary values for each parameter to effectively send notifications via custom messages. The returned boolean can be used to confirm the success of the operation.

```ts
Kanvas.notifications.sentNotificationByMessage(
  message: string,
  via: string[],
  user: number[]
): boolean
```

**Example:**

```js
const sentNotificationByMessage =
  await Kanvas.notifications.sentNotificationByMessage("message", ["via"], [1]);
```
