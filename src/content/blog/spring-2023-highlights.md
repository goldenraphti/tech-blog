---
title: 3 things that got me pumped in 2023 so far 🤩 🎁
tags: ["astrojs", "astro", "has()", "has() selector", "View Transitions API"]
pubDate: 2023-07-05
description: 3 things that got me pumped so far in 2023. Astro, the has() selector and the View Transitions API
---

Since I started my new job at PayEx/SwedbankPay last october, I got the privilege to have innovation-days every month.
And with CSS being on fire this year(s), I must say I have given it a lot of this innovation time.

There were a lot of new features that were either:

<div class='bulleted-list'>

- new (or new to me)
- useful
- fun to play with
- easy to use, intuitive

</div>

But only 3 of them stands out from the crowd by combining all those qualities. And they immediately became part of my routines.

## Astro

The [Astro framework](https://astro.build/) is a recent framework, which seems to have learnt from the others.
It's focused on performance and developer experience.

I would say what clicks to me is:

<div class='bulleted-list'>

- it's using the component based approach of modern web development popularized by React
- it's using the file based routing approach of Next.js (and now Svelte, Enhance, ... it seems to become a standar. And for good reason, it's very simple to use)
- it's using the static site generation to output super-fast websites
  - and it's very intuitive (unlike Gatsby)
  - and it's not limited to SSG
- default is to use .html or (better) .astro files to build your pages which are a mix of HTML and JS (like JSX) but outputting HTML
- it's already battery included, no need to choose your build tools etc, unlike framework like 11ty which I was previously using but having to choose and configure everything is tiring (for me)
- you can use any framework you want for your components (React, Vue, Svelte, ...), as easy as adding your React file and adding the Astro plugin for React

</div>

It immediately became my go-to framework for any new project (and I of course re-wrote this blog with it, which every dev do when they start falling in love with a new JS framework, in other word every 2 years 😜).
Simpler and faster than React but with the same DX level and mindset. And a dynamic and positive team behind the project.

## The has() selector

The [has() selector](https://developer.mozilla.org/en-US/docs/Web/CSS/:has) is a masterpiece. CSS just got a new superpower 🦸.

More than just a parent selector like you would get in SASS or LESS.
You can now target any element based on the presence of any other element in the DOM.
It can be _a parent, a sibling, a child, a grand-parent, a cousin, a nephew, a niece, a grand-grand-parent, a grand-grand-grand-parent_, ... you get the idea 😅.

Small things enabled with it:

<div class='bulleted-list'>

- styling a parent based on its children
- styling an element based on siblings _following after_ it
- styling the whole body based on the state of an input in the page

</div>

So much JS will be removed with this. And so much more will be possible.
For instance, I've built this website: [https://humankind-timeline.netlify.app/](https://humankind-timeline.netlify.app/), which is interactive, but can be used without JS (try it). And I'm using the `:has()` selector to style the whole page based on the state of the inputs.

But we could also think for example of theme switcher (light/dark theme) which would be possible without JS. Just add a checkbox, and base you CSS on it to select the corresponding CSS Custom Properties (aka CSS variables). That's what I did there: [https://web-experiment.netlify.app/experiments/has-selector/](https://web-experiment.netlify.app/experiments/has-selector/)

## The View Transitions API

Magical. The Web became cool again 🤩.

We can now have transitions between page navigation.
What I love most about it, beside making the transitions super cool, is that:

<div class='bulleted-list'>

- it's very easy to use (just add a line in the `<head>` & an identificator in the element's style)
- it works out of the box with no customizations (even if no elements are identified to stay in place and transitioned individually, it as bare minimum fade-out fade-in the whole page)
- it's 100% progressive enhancement. If your browser support it, great, you get for free as bonus. If it doesn't, well it's just the exact same experience as it would be without it. Nothing is broken.

I've started using it, on this side-project [Objectif 52](https://objectif-52.netlify.app/), and I'm loving it. Easy as a one-liner, but very efficient visually.

Thanks [Jake Archibald](https://jakearchibald.com/) for this one 🙏.

And to get cracking on it, I highly recommend reading Dave Rupert blog post on it: [https://daverupert.com/2023/05/getting-started-view-transitions/](https://daverupert.com/2023/05/getting-started-view-transitions/)

</div>
