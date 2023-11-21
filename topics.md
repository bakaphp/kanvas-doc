# Topics

## Method Create Topic

This method allows you to create a topic. It receive as parameters [TopicInputInterface]() and return [TopicInterface]().

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

This method allows you to update a topic. It receive as parameters [TopicInputInterface]() and id string then return [TopicInterface]().

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

This method allows you to get all topics. It receive as parameters [QueryGetTopicsWhereInterface]() and return [TopicInterfacep[]]().

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

This method allows you to follow a topic. It receive as parameters id string.

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

This method allows you to unfollow a topic. It receive as parameters id string.

```js
Kanvas.topics.unFollowTopic(
    id: string
): void
```

**Example:**

```js
Kanvas.topics.unFollowTopic("topic-id");
```
