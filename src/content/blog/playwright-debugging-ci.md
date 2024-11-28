---
title: Debugging Playwright tests in Github Actions
tags:
  [
    "playwright",
    "ci",
    "github-actions",
    "debugging",
    "e2e",
    "end-to-end",
    "testing",
  ]
pubDate: 2024-11-28
description: How to debug failing or flaky Playwright tests on CI Github Actions
---

# Debugging Playwright E2E tests in CI - Github Actions

I love writing E2E tests since I'm using Playwright. For many reasons.
But one thing can be a pain: tests failing only on CI (e.g. Github Actions).
It can be due to different reasons: the database used when running it on CI is different than running locally so the data moved around is different, the performance of CI is different (faster or slower), ...

I think the default workflow for using Playwright on CI is nice but it could be better regarding debugging.
The default (at the time of writing) is to have `reporter = 'line'` on CI.

I recommend using `reporter = 'html'`. It will make debugging tests much easier since you'll have the ability to visualize the trace for instance.

## The setup

```js
// playwright.config.ts
export default defineConfig({
  // ...
  /* Reporter to use. See https://playwright.dev/docs/test-reporters */
  reporter: "html",
  // ...
});
```

```js
// playwright.config.ts
export default defineConfig({
  // ...
  /* Reporter to use. See https://playwright.dev/docs/test-reporters */
  reporter: "html",
  // ...
});
```

```yaml
# Your yaml file triggering E2E on CI/ Github Actions
e2e:
  runs-on: ubuntu-latest
  needs: [sync]
  steps:
    - uses: actions/checkout@v4
    - uses: actions/setup-node@v4
      with:
        node-version: lts/*
    - name: Install dependencies
      run: npm ci
    - name: Install Playwright Browsers
      run: npx playwright install --with-deps
    - name: Run Playwright tests
      run: npx playwright test
      env:
        CI: true
    - uses: actions/upload-artifact@v4
      if: ${{ !cancelled() }}
      with:
        name: playwright-report
        path: playwright-report/
        retention-days: 30
```
