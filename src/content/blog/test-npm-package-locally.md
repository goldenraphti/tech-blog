---
title: Testing an npm package locally before deploying it
tags: ["npm", "test"]
pubDate: 2023-11-08
description: Testing an npm package locally before deploying it
---

In my normal work I build a Design System package for our company ([SwedbankPay Design System](https://www.npmjs.com/package/@swedbankpay/design-guide)).
But you often want to make sure you're not breaking anything, making your tests as close as possible to how the projects consuming it are going to experience it.

To do that I've set up a few different projects to test it locally, using different frameworks (Astro, Vue), to test all components, styles, scripts, and that the imports work fine, etc.

But ideally you want to test before deploying it to the world instead of having to rush a patch.

So here's how I do it: `npm pack`

Looking around I found 2 solutions `npm pack` & `npm link`. I went with `npm pack` because it's simpler and I don't need to keep the link between the package and the project.

Here were 2 nice articles to help you get cracking at it:

- [https://snyk.io/blog/best-practices-create-modern-npm-package/](https://snyk.io/blog/best-practices-create-modern-npm-package/)
- [https://flaviocopes.com/npm-local-package/](https://flaviocopes.com/npm-local-package/)

_Disclaimer: I know there is better alternatives, but as the sole dev working on it, this is the quick & efficient way._
