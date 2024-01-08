# Topics

## Methods
- [Method Create Topic](#method-create-topic)
- [Update Topic](#update-topic)
- [Get Topics](#get-topics)
- [Follow Topic](#follow-topic)
- [Unfollow Topic](#unfollow-topic)

## Method Create Topic

This method allows you to create a new topic. It takes the [TopicInputInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/topics.ts#L14) as parameters and returns a [TopicInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/topics.ts#L3).

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

This method enables you to update an existing topic. It takes the topic's ID as a string and [TopicInputInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/topics.ts#L14) as parameters, returning a [TopicInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/topics.ts#L3).
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

This method enables you to retrieve all topics. It takes [QueryGetTopicsWhereInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/topics.ts#L22) as parameters and returns an array of [TopicInterface](https://github.com/bakaphp/kanvas-core-js/blob/main/src/types/topics.ts#L3).
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

This method enables you to follow a specific topic by providing the topic's ID as a string parameter.

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

This method allows you to unfollow a specific topic by providing the topic's ID as a string parameter.

```js
Kanvas.topics.unFollowTopic(
    id: string
): void
```

**Example:**

```js
Kanvas.topics.unFollowTopic("topic-id");
```
