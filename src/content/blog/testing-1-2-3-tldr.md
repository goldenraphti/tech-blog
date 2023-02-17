---
title: Testing with Angie Jones - my notes
tags: ["post", "testing", "podcast", "angie jones"]
pubDate: 2021-09-17
description: Some notes about the interesting podcast episode from Angie Jones interview about testing in web development
---

# {{title}}

[JS Party](https://changelog.com/jsparty) podcast released a [great episode](https://jsparty.fm/181) about Testing with the amazing [Angie Jones](https://angiejones.tech/) as a guest, and hosted by [Emma Bostian](https://twitter.com/EmmaBostian) and [Nick Nisi](https://twitter.com/nicknisi).

Here are my notes:

<div class='bulleted-list'>

- Why implementing automated-test instead of only doing manual test?
  - to avoid regression (so when you refactor, delete, modified code and you need to be sure it did not break your previous work)
    - don't break without noticing
    - you're less hestitant into doing it
- what should be tested?
  - [a talk](https://www.youtube.com/watch?v=VL-_pnICmGY) from Angie Jones about that
  - don't go for 100% coverage
  - people care into writing their feature code and treat tests as if it’s throw-away code. But they're the source of truth about whether it works or not. You can't half-ass that. What tests are, they are guarding your features
  - trying to test everything gives you a lot more stuff to maintain and a lot of noise
  - In this matrix there are 4 different parameters:
    - cost efficiency of writing it
    - the value that it brings
    - historical context around it (spaghetti area or solid area where rarely any issue happens?)
    - is it covered by other things
  - to give you a list of what needs to be automated, and in which order to build those tests (what should be next)
- free online learning platform [Test Automation University](https://testautomationu.applitools.com/) she has built
- since new tools came in (Cypress, React Testing Library) FE testing has shifted, from units test to more intergation E2E tests
- it gives confidence to have a test pass from red (fail) when first written to then green successfull. Else you're not really sure the test is actually working. Maybe that's an argument for TDD
- unit testing
  - unit testing focuses on a small UI element
  - it sually always test first that the component renders / display a text
  - very narrow. What’s the smallest thing that you can target here?
  - no dependencies. So it’s not a whole lot of setup. Very focused
  - If one of those fail, you know exactly what’s wrong
  - what's the smallest unit from a FE perspective ?
    - the smallest unit in FE would be like a button, or an input, or a date picker
    - a component having for example both an input and a button would be an integration test
    - want to test things that are providing real value, not too implementation-specific
- visual testing:
  - works for both unit & E2E testing
  - it takes a picture of your application and its desired state. And it saves that as a baseline. Then when you run your regression test, it will take another screenshot and it will compare those two screenshots together, to determine if there are any differences there
  - can be run at component level (e.g. in Storybook library of components). That would be unit testing in FE.
  - want to test how things display in the browser
  - a lot of testing tool test by looking at the DOM instead of testing what is actually displayed on the screen
  - but beware, it does happen that things are present in the DOM but not visually present
    - text is same color as the background
    - it's bleeding off the edge of the page
    - hidden by other element overlapping
    - it's upside-down
    - especially when you start changing the viewport sizes
  - It's not only “Does it work from a functional perspective?”, it’s like “Does it work visually as well?”
  - can save when subtle visual difference your screen doesn't even properly enable to spot
  - visual changes can be dismissed by engineers saying "It's not pixel-peerfect, big deal". But visual changes can have big impact:
    - reservation buttons in a restaurant were off. No reservation is money lost
    - instagram ad had their text overlapping, making ad message incromprehensible. The company will probably ask refund + lost trust in the product
- Regression testing
  - Emma experience from Spotify:
    - run regression testing at the end of every sprint (2 weeks). When tey're about to release. All of the squads get together with a huge spreadsheet and manually regression-test things
  - regression tests are to make sure what you built didn't break anything that was performing well
  - they are run over and over. They can be unit test, integration, E2E, ... they're run over the old stuff
- Integration test
  - make sure different components are integrated successfully
- mocking
  - if I’m doing some integration with a third-party system. I don’t wanna test their part (BTW this is also true for the unit testing when using a UI component library, don't test the UI library, and don't test React. They've done it already)
  - So you would mock your API request to Twitter essentially focus on your application versus the other part
  - you don’t care necessarily about the API request that’s being sent. You just care about, like, given the response that you get back - is it rendering properly? That’s kind of what a mock does. It’s just giving you this mock data or fake data
- E2E testing:
  - most complex one to write, and the longest to run, and the hardest to maintain, so you try to have very few of those
  - you should have mostly unit tests, some integration tests, and a couple of very critical end to end flows (this is debated by other people though)
  - There’s nothing more painful than having flaky end to end tests. Then you have to retrigger build over and over
  - that's when you test a scenario
    - it can be a process from beginning to end (booking flight tickets from page landing to booking confirmation)
    - it can be scoped to a particular part (testing the checkout)
      - make an API call or something to essentially get my app into the testable
      - Don't try to do too much on FE: that's one cause of flacky tests, and long and fragile. Make an API call to get to the particular state (e.g. adding the item to the cart), and then can reach the UI and test
  - Mocking but also verifying the API call is still returning the data shaped as expected
    - this is critical
    - Mocking has its place, but that cannot be your end-all strategy
- Test Driven Development
  - people love it or hate it
  - you write your tests first. And this officially drives the design and the development of your feature
  - you would develop just enough code to make that test work
  - not many people do TDD on frontend tests. Mostly on backend, very small unit test type of thing
  - you don’t get to write code unless you have a test that is dictating that I need this code in order to pass. So your tests always start out as red, because you don’t have the code yet, and you write only enough code to get that test to pass
  - helps keep code short & focused, not over-engineering
  - an issue when first writing the test is "how identify the element yet" ?
    - it's highlighting a common FE issue: not making things unique enough. Give unique identifiers to elements.
    - a possibility for selecting is to use the accessibility role, so you're also enforcing A11y
- selecting testing tools
  - For the most part, all of them kind of work the same
  - some of them that offer more codeless or low-code:
    - e.g. Cypress has a Recorder, Selenium Web Driver - they also have a Selenium IDE version
    - so your manual testers can write some frontend tests
  - if you have dedicated test automation folks, or your devs are gonna write some tests, then you might wanna go with one of the coded solutions
  - questions to ask yourself:
    - what do I have to cover?
    - test on various browsers?
    - On various devices ?
    - make sure there’s some support. Beware of the new and hot:
      - does it have documentation
      - support
      - history (or is it just the result of a hackaton and people will drop it just after)
    - Open Source
    - where do we contribute if we need to?
    - if it’s a vendor, what do they have over the open source options that would make it worthwhile?
- Angie favourite stack:
  - she's a Java girl, so love Selenium Web Driver
  - For JavaScript: really like Cypress
- Cypress allows you to back-track in time too, to different snapshots
- advice for when starting out: - need more than the tech, it's a culture mindset
  - So I would focus on why you want to do it, and what’s the goal you expect here
    - most common goals = fast feedback. We wanna be able to make sure our application hasn’t regressed, and we want that information very quickly
  - make sure that the team is aware of this, and they’re on board with it
  - Make some launch learning sessions or something for the whole team, where we understand the risks, the value-add that testing brings, and kind of get everybody on board, and then we move into how to implement this

</div>
