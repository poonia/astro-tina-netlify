---
title: Throttling and debouncing in JavaScript
description: Understanding throttling and debouncing techniques in JavaScript
pubDate: 2021-03-04T05:00:00.000Z
---

Throttling and debouncing are two techniques that can be used to optimize resource usage by reducing the frequency of trigger events. While these techniques can help conserve resources, they also involve a trade-off between the resolution of tracking user actions and optimal resource usage. The good news is that these techniques can be applied and unapplied without requiring changes to the event listener code.

Throttling is a straightforward reduction of the trigger rate. It will cause the event listener to ignore some portion of the events while still firing the listeners at a constant (but reduced) rate. One very common example is scrolling where you want your interface to react in response to the scroll position (e.g., real and fake parallax effects, sticky menus, etc). Throttling can be implemented several ways. You can throttle by the number of events triggered, or by the rate (number of events per unit time), or by the delay between two handled events.

Let’s first hear it in plain English:

1. I will take a function and the minimal timing between two events
2. I will return a stand-in function that will be throttled
3. The stand-in function will record the time of each call to the original listener
4. The stand-in will compare the time of the current event with the last time it invoked the original handler, and will neglect to invoke the handler if the time difference is less than the delay

```javascript
// ES6 code
function throttled(delay, fn) {
  let lastCall = 0;
  return function (...args) {
    const now = (new Date).getTime();
    if (now - lastCall < delay) {
      return;
    }
    lastCall = now;
    return fn(...args);
  }
}
const myHandler = (event) => // do something with the event
const tHandler = throttled(200, myHandler);
  domNode.addEventListener("mousemove", tHandler);
```

debouncing is a technique of keeping the trigger rate at exactly 0 until a period of calm, and then triggering the listener exactly once.Debouncing is used when you don’t need to track every move user makes as long as you can make a timely response.

Debouncing can be implemented using setTimeout() and clearTimeout(). It normally takes a value in milliseconds that represents the wait period before the listener is triggered.

Here it is in plain English:

1. Take a delay in milliseconds and a handler function
2. Return a stand-in debounced function
3. When the stand-in is invoked, schedule the original listener to be invoked after the specified delay
4. When the stand-in function is invoked again, cancel the previously scheduled call, and schedule a new one after the delay
5. When calls to the stand-in function do not happen for a while, the scheduled call to the listener will finally go through

```javascript
// ES6
function debounced(delay, fn) {
  let timerId;
  return function (...args) {
    if (timerId) {
      clearTimeout(timerId);
    }
    timerId = setTimeout(() => {
      fn(...args);
      timerId = null;
    }, delay);
  }
}

const myHandler = (event) => // do something with the event
const dHandler = debounced(200, myHandler);
  domNode.addEventListener("input", dHandler);
```
