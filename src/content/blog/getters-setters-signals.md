---
title: Getters and Setters in javascript
description: What are get / set useful for in javascript
pubDate: 2024-11-25
tags: ["javascript", "get", "set", "signals", "computed"]
draft: true
---

I feel like getters and setters are under-discussed in basic FE field, compared to how it explain how e.g. signals and computed reactive values work

## Signals by get/set

```javascript
const signal = {
  privateValue: undefined,

  get value() {
    return this.privateValue;
  },

  set value(newValue) {
    this.privateValue = newValue;
  },
};

console.log("before", signal.value);
signal.value = "13";
console.log("after", signal.value);
```

# Computed by get/set

```javascript
const user = {
  firstName: "Noam",
  lastName: "Chomsky",

  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },

  set fullName(newValueArray) {
    this.firstName = newValueArray[0];
    this.lastName = newValueArray[1];
  },
};

console.log("before", user.fullName);
user.fullName = ["Raphaël", "Ferrand"];
console.log("after", user.fullName);
```
