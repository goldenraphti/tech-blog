---
title: Intercept & modify request in Playwright
description: Intercept and modify the request before it's sent in Playwright
pubDate: 2024-11-25
tags: ["javascript", "e2e", "playwright", "tip", "testing"]
draft: true
---

Let's imagine you're like me, you're stuck in a situation where your BE API is not ready to receive some properties in the payload of your request (`payload` = the `body`).
Instead of letting it fail your E2E tests and loose trust in them, let's intercept and modify the request before it's sent:

```javascript
await page.route("**/signup/partners", async (route, request) => {
  const {
    country,
    name,
    companyRegistrationNumber,
    connectionNumber,
    agentId,
  } = request.postDataJSON();
  const modifiedRequest = {
    // country,
    name,
    // companyRegistrationNumber: null,
    connectionNumber,
    agentId,
  };
  await route.continue({ postData: JSON.stringify(modifiedRequest) });
});
```
