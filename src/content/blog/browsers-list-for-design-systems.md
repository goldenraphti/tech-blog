---
title: Deciding the browserslist for a Design System in Scandinavia
tags:
  [
    "design-system",
    "norway",
    "sweden",
    "ios",
    "browserslist",
    "browser support",
    "polyfill",
    "postcss",
    "survivor bias",
  ]
pubDate: 2024-12-13
description: How to decide which browsers to support in a Design System in Scandinavia
---

# Browsers support for a Design System in Scandinavia

## The specificities of Norway

Norway is a country where the usage of iOS is higher than in other countries. Like, way higher.

We could think it makes our life easier. Well it does not. Apple iOS tends to ship features later than the other browsers. It sucks.

And, on top of that, iOS browser does not auto-updates like Firefox and Edge/Chrome. Plus some users get locked on a version unless they can change their device buying a new one. Which means spending a whole lot of money.

All this ends up in this situation: We have to support older versions of iOS for a longer time.

For some reason Sweden and Denmark are actually much more similar to the rest of Europe and the world.

## Technical implications

We want to support older browsers if we can, and if it makes sense. This being said, all the projects using the design-system are also using some sort of JS framework. Which means the browser support will also eventually be limited by that.

### Browser support by the major JS frameworks

The common browser support is

"browserslist": [
"last 2 major versions",
"> 1%",
"not dead"
]

Examples:

- Nuxt: [https://nuxt.com/blog/v3#the-browser-and-nodejs-support](https://nuxt.com/blog/v3#the-browser-and-nodejs-support)
- Angular: [https://angular.dev/reference/versions#browser-support](https://angular.dev/reference/versions#browser-support)
- React: [https://react.dev/reference/react-dom/client#browser-support](https://react.dev/reference/react-dom/client#browser-support) (they actually support all the way to IE9 & 10, although it would imply using polyfills)
- Wordpress: [https://make.wordpress.org/core/handbook/best-practices/browser-support/](https://make.wordpress.org/core/handbook/best-practices/browser-support/)

So, this is the browserslist I use:

```json
"browserslist": [
  "last 3 versions",
  "last 2 major versions",
  "> 0.5%",
  "not dead"
]
```

## Ideas

- A bigger support can always be done a the level of the project consuming the design-system, if one of them needs longer support.
- Remember to check your own analytics to know what's your panorama (Norway !== Sweden, dev blog users !== non techy older age users, etc)
- But beware of the survivorship bias: if you only support the latest versions, you will only get users with the latest versions since the users with older versions will not be able to use your website, and therefore won't appear in your analytics. A great article about this effect here by Simon Hearne: [https://simonhearne.com/2022/survorship-bias-in-webperf/](https://simonhearne.com/2022/survorship-bias-in-webperf/)
