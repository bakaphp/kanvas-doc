# usePusher Hook

## Description

`usePusher` is a custom React hook that facilitates integration with Pusher for real-time event reception. It allows subscribing to a specific channel and listening to particular events.

## Installation

Ensure you have the necessary dependencies installed:

npm install pusher-js

## Usage

### usePusher Hook
```javascript
import { usePusher } from "@/services/pusher";

const { eventData, isSubscribed, subscribe, unsubscribe, pusherInstance } = usePusher(channelName, eventName);
```
#### Parameters

- `channelName` (string): Name of the Pusher channel to subscribe to.
- `eventName` (string): Name of the event to listen for.

#### Returns

- `eventData` (object | null): Data from the last received event.
- `isSubscribed` (boolean): Subscription status to the channel.
- `subscribe` (function): Function to subscribe to the channel.
- `unsubscribe` (function): Function to unsubscribe from the channel.
- `pusherInstance` (Pusher): Pusher instance.

Note: pusher-js only works in the client side

### Example Usage using Nextjs

```javascript
"use client";

import { useEffect } from "react";
import { usePusher } from "@/services/pusher";

export default function PusherComponent() {
  const { eventData, isSubscribed, subscribe, unsubscribe, pusherInstance } = usePusher(
    "my-channel",
    "my-event"
  );

  useEffect(() => {
    console.log("Pusher instance:", pusherInstance);
    console.log("Is subscribed:", isSubscribed);
    console.log("Event data:", eventData);
  }, [pusherInstance, isSubscribed, eventData]);

  return (
    <div>
      <h1>Pusher Test</h1>
      <pre>{JSON.stringify(eventData, null, 2)}</pre>
      <p>Subscribed: {isSubscribed.toString()}</p>
      <button onClick={subscribe}>Subscribe</button>
      <button onClick={unsubscribe}>Unsubscribe</button>
    </div>
  );
}
```
## Configuration

Make sure to configure the Pusher credentials correctly in the hook:

const pusherInstance = useMemo(() => new Pusher("YOUR_APP_KEY", { cluster: "YOUR_CLUSTER" }), []);

Replace "YOUR_APP_KEY" and "YOUR_CLUSTER" with your actual Pusher credentials.

## Notes

- The hook automatically subscribes to the specified channel when the component mounts.
- Use `subscribe()` to re-subscribe if you've manually unsubscribed.
- `unsubscribe()` cancels the subscription and clears the event data.
- Ensure that the channel and event name match those configured in your backend.

## Debugging

If you encounter issues:

1. Check the browser console for logs and possible errors.
2. Verify Pusher's connection state with `pusherInstance.connection.state`.
3. Make sure there are no CORS or connection errors.
4. Confirm that events are being published correctly from your backend.

## Full Hook Implementation
```typescript
import { useEffect, useState, useCallback, useMemo } from "react";
import Pusher from "pusher-js";

type PusherEventData = Record<string, any>;

export const usePusher = (channelName: string, eventName: string) => {
  const [eventData, setEventData] = useState<PusherEventData | null>(null);
  const [isSubscribed, setIsSubscribed] = useState(false);

  const pusherInstance = useMemo(() => new Pusher("YOUR_APP_KEY", { cluster: "YOUR_CLUSTER" }), []);

  const subscribe = useCallback(() => {
    const channel = pusherInstance.subscribe(channelName);
    channel.bind(eventName, (data: PusherEventData) => {
      console.log("Event received:", data);
      setEventData(data);
    });
    setIsSubscribed(true);
  }, [channelName, eventName, pusherInstance]);

  const unsubscribe = useCallback(() => {
    pusherInstance.unsubscribe(channelName);
    setIsSubscribed(false);
    setEventData(null);
  }, [channelName, pusherInstance]);

  useEffect(() => {
    subscribe();
    return () => {
      unsubscribe();
    };
  }, [subscribe, unsubscribe]);

  return { eventData, isSubscribed, subscribe, unsubscribe, pusherInstance };
};
```
This hook provides a simple and efficient way to integrate Pusher into your React applications for real-time updates.
