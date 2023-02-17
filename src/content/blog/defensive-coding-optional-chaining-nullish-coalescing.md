---
title: Defensive coding in Javascript
tags:
  [
    "post",
    "email dev",
    "js",
    "javascript",
    "code reviews",
    "nullish coalescing operator",
    "optional chaining",
    "best practice",
    "defensive coding",
    "default value",
  ]
pubDate: 2021-12-01
description: Defensive coding in javascript, learn to use optional chaining and nullish coalescing operator
---

Recent evolutions of Javascript have brought some real cool and useful features, actionable every day.

One that I keep using lately and I've been recommanding a few times in my code review is the combination ["optional chaining ( ?. )"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) + ["Nullish coalescing operator ( ?? )"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator):

For example I've seen in our codebase something like:

I've stumbled upon this today whith some deeply nested objects.
A potential issue happening when we want to use the value of a property located deep within a chain of connected objects, like in our example.
We do have to check (as we did in our example using a ternary operator), to avoid it to throw an error

```bash
Error: can't access property "unsavedChanges", component.emailLocalizationComponent is undefined`.
```

So let's see 3 possibilities:

<div class='bulleted-list'>

- ☠️ The one that could potentially throw an error like mentionned above if `emailLocalizationComponent` does not exists as a property of the `component` object:

```javascript
let unsavedEmailLocalization =
  component.emailLocalizationComponent.unsavedChanges;
```

- 👍 Now what I saw in our codebase (it works, but it could be better):

```javascript
let unsavedEmailLocalization = component.emailLocalizationComponent
  ? component.emailLocalizationComponent.unsavedChanges
  : false;
```

- 🏆 But as I said in intro, modern JS offers great new features to combine checking for `null` or `undefined` and assigning a default value, all in an easy 1 liner:

```javascript
let unsavedEmailLocalization =
  component?.emailLocalizationComponent?.unsavedChanges ?? false;
```

</div>

This way we have a concise way to both:

<div class='bulleted-list mb-6'>

- Be on the safe side and future proof by avoiding the script to break when trying to assign the value of a property that might be missing
- Yet if this happens, assigning `undefined` is useless, so let's be ahead of it and give it a default value with the nullish coalescing operator, which assign a value if the left side evaluates to `null` or `undefined`
- Note that a similar thing exist with the ["Logical OR (||) operator"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR), the big difference is that the logical OR (||) does assign a default value as well, _but_ it will check for truthy and nut nullish, which means that it would not assign values such as `false` or `0` or even an empty string `''`. But those values are often useful values. This is why my goto is the nullish operator `??`

</div>

What about support: if you don't need to support IE then you're fine. If you do ... well ...that's a pity 😅
