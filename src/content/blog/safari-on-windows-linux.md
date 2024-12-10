---
title: "How to test Safari (and old Safari versions) on Windows and Linux"
pubDate: 2024-11-28
tags:
  ["safari", "windows", "linux", "playwright", "browser", "testing", "webkit"]
description: How to easily test old versions of Safari on Windows and Linux using Playwright
---

# How to test Safari(including old versions) on Windows and Linux

If you're like me, you're not using a Mac, but you still need to test your website on Safari. This is a guide on how to test Safari on Windows and Linux.
Norway and the norwegian cultural sector is a Mac-users environment. Not always updated versions though. So it was critical fo rme to ensure the webapp worked on old Safari versions. Here I'm talking Safari 15.3 when the current version was 18.0. So supporting a version almost 3 years old.
Client is king (if they're paying for the time spent on it).

So, how do you test Safari on Windows and Linux? The answer is Playwright. The End-to-end testing library I use and loooove.

The trick has already been shared multiple times by Kevin Powell or Wes Box among other, but here it is again, for me to remember.

This first command will run playwright using webkit (the Safari browser engine), using the latest version of Playwright and therefore the latest version of Safari too:

```bash
npx playwright wk https://raphaelferrand.com
```

But what about testing old Safari versions?
Just use old versions of Playwright. It's always shipping the latest-ish versions of the browsers.
This being said you will also have an old version of Playwright. Which is bad if you want to do actual E2E testing. But if it's just to have an in-browser look and debugging then it's plenty enough.

```bash
npx playwright@1.15.2 wk https://raphaelferrand.com
```

## Old Safari versions

And here is a short list of the Playwright versions corresponding to the Webkit (= Safari) versions:

```bash
WebKit 18.2 => Playwright 1.49.0
WebKit 18.0 => Playwright 1.48.2
WebKit 17.4 => Playwright 1.45.3 # I have not tested this version yet
WebKit 17.0 => Playwright 1.38.1 # I have not tested this version yet
WebKit 16.4 => Playwright 1.35.1 # I have not tested this version yet
WebKit 16.0 => Playwright 1.27.1 # I have not tested this version yet
WebKit 15.4 => Playwright 1.23.4 # I have not tested this version yet
WebKit 15.0 => Playwright 1.15.2
WebKit 14.2 => Playwright 1.13.1
WebKit 14.1 => Playwright 1.9.2
```
