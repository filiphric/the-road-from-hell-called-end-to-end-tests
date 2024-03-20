---
theme: the-unnamed
background: ./images/Dante_Domenico_di_Michelino.jpg
class: 'text-center'
highlighter: shiki
info: |
  ## The road from hell called end-to-end tests
title: The road from hell called end-to-end tests
mdc: true
themeConfig:
  color: "#F3EFF5"
  background: "#161C2C"

  code-background: "#0F131E"
  code-border: "#242d34"

  accents-pink: "#F02D5E"
  accents-red: "#FE4A49"
  accents-lightblue: "#41B0F6"
  accents-blue: "#5EADF2"
  accents-vulcan: "#0E131F"

  header-shadow: rgba(0, 0, 0, 0.15) 1.95px 1.95px 2.6px;

  default-headingBg: var(--slidev-theme-accents-pink)
  default-headingColor: var(--slidev-theme-color)
  default-background: var(--slidev-theme-background)

  center-headingBg: var(--slidev-theme-accents-blue)
  center-headingColor: var(--slidev-theme-color)
  center-background: var(--slidev-theme-background)

  cover-headingBg: var(--slidev-theme-accents-pink)
  cover-headingColor: var(--slidev-theme-color)
  cover-background: var(--slidev-theme-background)

  section-headingBg: var(--slidev-theme-accents-lightblue)
  section-headingColor: var(--slidev-theme-color)
  section-background: var(--slidev-theme-background)

  aboutme-background: var(--slidev-theme-color)
  aboutme-color: var(--slidev-theme-background)
  aboutme-helloBg: var(--slidev-theme-accents-pink)
  aboutme-helloColor: var(--slidev-theme-background)
  aboutme-nameColor: var(--slidev-theme-accents-red)
---

# The road from hell
# called end-to-end tests

<!--
- Before we start, I want to do a little voting so I can get a feel of the room
- I have a feeling that I may be biased when I talk about e2e tests as something that’s from hell
- let’s try a single clap
-->
---
layout: center
---
# Are you writing e2e tests?

---
layout: center
---
# Has your e2e test ever failed?

---
layout: center
---
# Has your test failed and you weren’t sure why?

---
layout: center
---
# Have you ever spent more than 1 hour debugging?

---
layout: center
---
# More than two hours?

---
layout: center
---
# More than a day?

---
layout: center
---
# Are you sad right now?

<!-- 
- although we love our jobs, there’s parts that feel like hell
- ✅
 -->

---
layout: section
background: ./images/Dante_Domenico_di_Michelino.jpg
---
# Divine comedy
Dante Alighieri
<!-- 
- in this presentation I decided to make a small parallel
- divine comedy - story of the underworld, in first part roman poet Virgil guides Dante across 9 circles of hell
- I’m going to play Virgil here
- if the presentation is not divine, at least let’s hope it’s a comedy
-->

---
layout: image
image: ./images/9_circles.jpg
---
<!-- 
- the picture you are looking at is Botticelli’s depiction of 9 circles of hell
- does it remind you of anything?
-->

---
layout: image
image: ./images/9_circles_flipped.jpg
---

---
layout: default
---
# Testing pyramid
<img src="/images/pyramid.png" class="h-70 m-auto mt-10" />
<!-- 
- good old testing pyramid
- focusing today on the top triangle - e2e tests
- there’s something that this pyramid shows us
- e2e tests are slow and costly and yet, we can’t help but write them - why?
- ⏸️
- I’m sure some of you may sit here and be like "please don’t make me loose my job"
-->

---
layout: default
---
# Business value

<Tweet id="977018512689455106" class="w-150 m-auto pt-10" />

<!-- 
- the other one is business value
- the more your tests reseble the way your software is used, the more confidence they can give you
 -->

---
layout: image-right
image: ./images/code_coverage.png
---
# Efficiency
```js
it('opens the page', () => {
  cy.visit('/')
})
```

<style>
  .slidev-code-wrapper {
   padding-top: 35%
  }
</style>

<!-- 
- one of the main reasons is efficiency
- simply opening an application will result in roughly 25% of the app being tested
- So there are two main problems with e2e test automation

 -->

---
layout: center
---
<h1>1. putting human behavior into code</h1>
<h1 v-click>2. making automation worth it</h1>

<!-- 
- the challenge of writing code that acts like a human
- writing the automation in a way that it actually saves time
- because let’s face it, if it takes longer to write and maintain automation script than to manually test it’s a waste of time and money
- but don’t get me wrong, these are no easy tasks
 -->

---
layout: default
---



