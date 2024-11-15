---
title: Should we still use Sass?
tags: ["post", "sass", "css", "stephanie eckles", "smashing magasine"]
pubDate: 2022-07-07
description: Should we still use Sass?
---

Since IE11 died a few weeks back (RIP 🍾 🎉), and because I'll soon(_ish_) start working on design systems ( 🤫 ) I found myself thinking:

_Should we still use Sass? Should I move away from it?_

Is it still necessary today, or has vanilla CSS closed the gap?

**Today we have:**

<div class='bulleted-list mb-6'>

- ✅ custom variables ([great support](https://caniuse.com/css-variables))
- ✅ cascade layers ([well supported](https://caniuse.com/css-cascade-layers))
- 👷‍♀️ scoping & [nesting CSS](https://www.w3.org/TR/css-nesting-1/) coming (but [zero browser support](https://caniuse.com/css-nesting) yet)

</div>

and also

<div class='bulleted-list mb-6'>

- 👷‍♀️ [color mix](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/color-mix) ([not yet](https://caniuse.com/mdn-css_types_color_color-mix))
- 👷‍♀️ [color contrast](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/color-contrast) ([not yet](https://caniuse.com/mdn-css_types_color_color-contrast))
- ✅ color-scheme preferences [light/dark themes](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)

</div>

Before I could actually sit and think this through I fell on this [episode of Smashing Podcast](https://podcast.smashingmagazine.com/episodes/is-sass-still-relevant-with-stephanie-eckles), interviewing [Stephanie Eckles](https://thinkdobecreate.com/). Great stuff. At one point they reached this topic.
She still uses [Sass](https://sass-lang.com/).
Here are her reasons:

**Mostly:**

<div class='bulleted-list mb-6'>

- organization: to compile her stylesheets, keep them separated (as components, ... (shes uses [BEM](https://en.bem.info/methodology/css/)))
- functions: looping through token, spit out different utility classes

</div>

but also:

<div class='bulleted-list mb-6'>

- in design system context, better management of "tokens" of how different customizations enter the stylesheets
- mixins -> but less, custom properties are filling the gap of need

</div>

But she too is using it less and less. Now, for example: `is()` & `where()`: simplify her selectors in a way she was previously using Sass for

I also think that [has](https://developer.mozilla.org/en-US/docs/Web/CSS/:has) `has()` will be key in replacing the `&` used as some kind of [parent selector](https://sass-lang.com/documentation/style-rules/parent-selector) in Sass. Just waiting for its [support](https://caniuse.com/css-has) to improve 😬

So here we are. Getting near a place where we'll be able to let Sass go.
Personally, nesting is something I'm really looking forward, but I am using Postcss to [polyfill it](postcss-nesting), so I don't need Sass for it. And `has()` will be of great use too.
Then the functions can be hard, but how many projects are actually using it?

I guess for a big project, like a production design-system, you might still need to use it. And I clearly think that it is not worth moving away from it now if you're in a project that was using it for years. Not worth the effort to move out of Sass to then move everything back to PostCSS equivalents. But if you're starting new projects, I guess I would not be reaching out for it (and as a matter of fact, this site is not using it) 🚀

# Browser support

<baseline-status featureId="color-mix"></baseline-status>
<baseline-status featureId="nesting"></baseline-status>
