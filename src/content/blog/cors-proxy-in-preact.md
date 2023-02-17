---
title: Adding a local proxy in Preact to avoid CORS issues
tags:
  [
    "post",
    "preact",
    "preactjs",
    "proxy",
    "cors",
    "config",
    "webpack",
    "build",
    "error",
    "dev",
    "server",
    "local server",
    "proxy server",
    "corsanywhere",
  ]
pubDate: 2022-02-14
description: How to add a local proxy in Preact in order to avoid CORS issues when fetching an third-party API
---

For a small side-project I wanted to start a small Preact app to filter & visualize the results of a third-party API I don't have the control of.

Of course ...🥁... CORS problem 🤦‍♂️

Possible solutions:

<div class='bulleted-list mb-6'>

- ~~cors-anywhere~~ -> this is basically the result you'll find everywhere on internet. But it's not a possible anymore (perpetual error "too many requests")
- modify the CORS on the api server -> not an option
- throw some local proxy ✅

</div>

There was no real example for Preact. And since this was the actual very first time I was using Preact it meant that many things I needed to do were actually not obvious at all. That's why I hope this can help more people:

1- preact.config.js

- If you don't have it yet, create a "preact.config.js" file at the root of your project.
- paste this in it:

```js
module.exports = function (config) {
  if (config.devServer) {
    config.devServer.proxy = [
      {
        // proxy requests matching a pattern:
        path: "/api/**",

        // where to proxy to:
        target: "https://theAPIyouWantToProxyTo",

        // optionally change Origin: and Host: headers to match target:
        changeOrigin: true,
        changeHost: true,
        secure: false,

        // optionally mutate request before proxying:
        pathRewrite: function (path, request) {
          // you can modify the outbound proxy request here:
          // delete req.headers.referer;

          // common: remove first path segment: (/api/**)
          return "/" + path.replace(/^\/[^\/]+\//, "");
        },

        // optionally mutate proxy response:
        // onProxyRes: function(proxyRes, req, res) {
        // you can modify the response here:
        // proxyRes.headers.connection = 'keep-alive';
        // proxyRes.headers['cache-control'] = 'no-cache';
        // }
      },
    ];
  }
};
```

2- the fetch

You will need to adapt your fetch function so it uses the Proxy you've just enabled in your preact config file, by fetching it through the `/api/` route:

```js
const getBooking = (urlToFetch) => {
  fetch(`/api/${urlToFetch}`)
    .then((response) => response.json())
    .then((data) => console.log("🎁", data))
    .catch((error) => console.log("🔫", error));
};
```

3- avoid the build error

You might have found somewhere an example looking like that:

```js
config.devServer.proxy = [
    {
      // proxy requests matching a pattern:
      path: '/api/**',
```

Well, this will cause you an error thrown at build time for prod since in prod environment config.devServer is `undefined`.
That's why it's important to add a condition before such as:

```js
if (config.devServer) {
  config.devServer.proxy = [
    {
      // proxy requests matching a pattern:
      path: '/api/**',
```

You can also use a condition based on the environment used.
