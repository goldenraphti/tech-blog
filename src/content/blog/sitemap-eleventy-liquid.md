---
title: Adding a sitemap in Eleventy using .liquid format
tags: ["post", "liquid", "eleventy", "11ty", "sitemap"]
pubDate: 2022-03-16
description: How to add a sitemap in .liquid in an eleventy website
---

I am using this blog without any starter, the point being to build every part of it and understand the mechanism as much as possible.

Which is why I faced this issue: the sitemap.
And the ones I found were all written in .njk, but I am using .liquid all over. I thought now I fixed it let's offer it to the others.

## Create the sitemap file

Create the sitemap.xml.liquid at the root of your website.

```liquid
---
permalink: /sitemap.xml
eleventyExcludeFromCollections: true
---
<?xml version="1.0" encoding="utf-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
{%- for page in collections.all %}
  {% capture mappedUrl %}{{ metadata.url}}{{ page.url | url }}{% endcapture %}
    <url>
      <loc>{{ mappedUrl }}</loc>
      <lastmod>{{ page.date | htmlDateString }}</lastmod>
    </url>
  {%- endfor %}
</urlset>
```

In here you might see the small differences with .njk from the sitemap file on the [blog-starter repo](https://github.com/11ty/eleventy-base-blog/blob/master/sitemap.xml.njk):

<div class='bulleted-list'>

- `set` become `capture`
- `endset` becomes `endcapture`

</div>

That's all for the language conversion between njk and liquid. Quick and easy.

Pages referring to the corresponding nunjucks & liquid languages:

<div class='bulleted-list'>

- [nunjucks](https://mozilla.github.io/nunjucks/templating.html#set)
- [liquid](https://shopify.github.io/liquid/tags/variable/)

</div>

## Dependencies

Some parts of the sitemap file require some filter and some dependencies:

### eleventy.js

in you file "eleventy.js", add this:

```js
// other imports you migh have already
const { DateTime } = require("luxon");

module.exports = function (eleventyConfig) {
  //  eleventyConfig.addPassthroughCopy("css");
  //  eleventyConfig.addPlugin(abc);

  eleventyConfig.addFilter("readableDate", (dateObj) => {
    return DateTime.fromJSDate(dateObj, { zone: "utc" }).toFormat(
      "dd LLL yyyy"
    );
  });

  // https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#valid-date-string
  eleventyConfig.addFilter("htmlDateString", (dateObj) => {
    return DateTime.fromJSDate(dateObj, { zone: "utc" }).toFormat("yyyy-LL-dd");
  });

  //    return {
  //     passthroughFileCopy: true,
  //  };
};
```

### package.json

install [luxon package](https://www.npmjs.com/package/luxon) so you'll be able to use "DateTime".

## Metadata

Make sure you have a file called "metadata.json" for example in our case, inside "\_data/" folder, in which you specify the URL of the website

```json
{
  // "title": "Your Blog Name",
  "url": "https://example.com/"
  // "language": "en",
  // "description": "I am writing about my experiences as a naval navel-gazer.",
  // "feed": {
  //   "subtitle": "I am writing about my experiences as a naval navel-gazer.",
  //   "filename": "feed.xml",
  //   "path": "/feed/feed.xml",
  //   "id": "https://example.com/"
  // },
  // "jsonfeed": {
  //   "path": "/feed/feed.json",
  //   "url": "https://example.com/feed/feed.json"
  // },
  // "author": {
  //   "name": "Your Name Here",
  //   "email": "youremailaddress@example.com",
  //   "url": "https://example.com/about-me/"
  // }
}
```
