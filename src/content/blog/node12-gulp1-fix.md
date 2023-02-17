---
title: Fix gulp 3 & node 12 compatibility issues
tags: ["post", "gulp", "node", "tip", "fix"]
pubDate: 2021-09-13
description: How to fix the issue in Gulp3 & Node 12 "primordials is not defined"
---

# {{title}}

Jumping between projects I faced a problem.
To build my react-native app we needed to get on "Node v12". Once upgraded to it, and getting back on some Episerver development at the moment of building with Gulp I got some error thwon in the console:

```bash
ReferenceError: primordials is not defined
```

Turns out the issue is that Node 12 and Gulp 3 have compatibility issues.

- Upgrading Gulp version wasn't a solution at the time (it's a significant amount of work to solve all the breaking changes it involves. We did it later, but we needed a quicker a solution on the moment)
- we couldn't downgrade Node since we needed this for our React-Native app

So, the solution at the moment was found in Tim Kamanin [blog post](https://timonweb.com/javascript/how-to-fix-referenceerror-primordials-is-not-defined-error/):

> 1. In the same directory where you have package.json create an npm-shrinkwrap.json file with the following contents:
>
> ```js
> {
>  "dependencies": {
>    "graceful-fs": {
>      "version": "4.2.2"
>    }
>  }
> }
> ```
>
> 2. Run `npm install`

That's it, problem solved 😉 (at least for now. You should probably think about upgrading your Gulp version by now. At least that's what we did).
