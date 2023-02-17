---
title: How to fix Outlook breaking the charset
tags: ["post", "email dev", "outlook", "unicode", "charset", "utf8"]
pubDate: 2021-09-16
description: Hot to fix Outlook bug breaking the charset setting it automatically to arabic charset
---

Outlook Desktop yet found a new way to trick me. And it did cost me several hours to debug this one.

We build emails that get translated in different languages. But then I found out Outlook Desktop broke the email styling.
After several hours of debugging, trying to identify where the issue was coming from, I found a new Oulook magic:

It was deleting the `charset` I had set up in the email's `<head>`

```html
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
```

was becoming

```html
<meta http-equiv="Content-Type" content="text/html; charset=windows-1256" />
```

Yes. Somewhere the charset I set get stripped off and replaced (here by arabic).
It seems like I'm not the only one: [https://litmus.com/community/discussions/6375-meta-charset-utf-8-whatever-charset-i-use-in-my-emails-outlook-strips-them-out](https://litmus.com/community/discussions/6375-meta-charset-utf-8-whatever-charset-i-use-in-my-emails-outlook-strips-them-out)

This error of encoding resulting in breaking the style of the email:

Yet for some reason when writing the email in spanish it would respect the encoding.
It seems like when Outlook detect some spanish characters such as `á` then it would not automatically set the encoding on arabic anymore.
hence the small hack:

```html
<!-- START hack to force charset utf-8 automatic picking from Outlook Desktop  -->
<div
  style="display:none; font-size:1px; color:#333333; line-height:1px; max-height:0px; max-width:0px; opacity:0; overflow:hidden;"
>
  é á
</div>
<!-- END hack to force charset automatic picking from Outlook Desktop  -->
```

it ain't pretty but it works. One Outlook problem solved at a time 😉
