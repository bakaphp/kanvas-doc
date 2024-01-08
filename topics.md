# Topics

## Method Create Topic

This method enables you to create a new topic. It takes TopicInputInterface as parameters and returns TopicInterface.

```js
Kanvas.topics.createTopic(
    topicInput: TopicInputInterface
): TopicInterface
```

**Example:**

```js
const topic = Kanvas.topics.createTopic({
  name: "Topic Name",
  slug: "topic-name",
  weight: 1,
  is_feature: 1, // 1 or 0
  status: true,
});
```

## Update Topic

This method allows you to update an existing topic. It takes the topic's ID as a string and TopicInputInterface as parameters, then returns TopicInterface.

```js
Kanvas.topics.updateTopic(
    id: string,
    topicInput: TopicInputInterface
): TopicInterface
```

**Example:**

```js
const topic = Kanvas.topics.updateTopic("topic-id", {
  name: "Topic Name",
  slug: "topic-name",
  weight: 1,
  is_feature: 1, // 1 or 0
  status: true,
});
```

## Get Topics

This method allows you to retrieve all topics. It takes QueryGetTopicsWhereInterface as parameters and returns TopicInterface[].

```js
Kanvas.topics.getTopics(
    where: QueryGetTopicsWhereInterface
): TopicInterface[]
```

**Example:**

```js
const topics = Kanvas.topics.getTopics();
```

## Follow Topic

This method allows you to follow a specific topic. It takes the topic's ID as a string.

```js
kanvas.topics.followTopic(
    id: string
): void
```

**Example:**

```js
Kanvas.topics.followTopic("topic-id");
```

## Unfollow Topic

This method allows you to unfollow a specific topic. It takes the topic's ID as a string.

```js
Kanvas.topics.unFollowTopic(
    id: string
): void
```

**Example:**

```js
Kanvas.topics.unFollowTopic("topic-id");
```
