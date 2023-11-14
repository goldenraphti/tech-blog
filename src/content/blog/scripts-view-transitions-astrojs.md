---
title: On-load scripts & view-transitions in Astro
tags: ["astro", "view-transitions", "script"]
pubDate: 2023-11-14
description: Your script running on page load might not run on page navigation after implementing View Transitions in Astro. Here is the solution.
---

I have a script running on page load. It's a simple script for the dark-theme toggle. It runs on every page load (and therefore page navigations). Now, since I added View Transitions, it only runs on first page load. It doesn't run on page navigations anymore. If you need it to run on every page load, here is the solution:

```js
// Runs on view transitions navigation
document.addEventListener("astro:after-swap", setDarkMode);
```

From the great [Astro documentation](https://docs.astro.build/en/guides/view-transitions/#astroafter-swap).

By the way if you want to have something similar, it comes from Adam Argyle's [Dark Mode Toggle](https://web.dev/patterns/theming/theme-switch/).

Also, in the future, once `has()` support is wide enough, I am planning to switch my theme switcher to a script-less solution. Namely, using only an input combined with the `has()` selector on the CSS side. Like the way I implemented it my Web-Experiments example for the`has()` selector: [https://web-experiment.netlify.app/experiments/has-selector/](https://web-experiment.netlify.app/experiments/has-selector/). No more JS. Pure HTML & CSS 😎🚀🔥.
