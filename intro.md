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
- hope not, if you are, I hope this presentation is positive
- although we love our jobs, there’s parts that feel like hell
-->

---
layout: section
background: /images/Dante_Domenico_di_Michelino.png
---

# Divine comedy
Dante Alighieri

<!--
- in this presentation I decided to make a small parallel
- divine comedy - story of the underworld, in first part roman poet Virgil guides Dante across circles of hell
- I’m going to play Virgil here
- if the presentation is not divine, at least let’s hope it’s a comedy
- also - I have to come clear about something - I have promised 9 rings of hell in the abstract of this talk, but then I realized I’m only alowed to talk for 30 minutes and not half a day, so I included a QR code at the end of this presentation, where I included some of the slides that didn’t make it to this talk and I plan to add some more
-->

---
layout: image
image: /images/9_circles.png
---
<!-- 
- the picture you are looking at is Botticelli’s depiction of circles of hell
- does it remind you of anything?
-->

---
layout: image
image: /images/9_circles_flipped.png
---

---
layout: default
---

# Testing pyramid
<img src="/images/pyramid.png" class="h-70 m-auto mt-10" />

<!--
- good old testing pyramid
- showing this will probably result in about half of the room leaving
- today, focusing on the top triangle - e2e tests
- e2e tests are slow and costly and yet, we can’t help but write them - why?
- two main reasons:
-->

---
layout: default
---
# Business value

<Tweet id="977018512689455106" class="w-150 m-auto pt-10" />

<!-- 
- the other one is business value
- the more your tests reseble the way your software is used, the more confidence they can give you [click]
 -->

---
layout: image-right
image: /images/code_coverage.png
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
- [click]
- writing the automation in a way that it actually saves time
- because let’s face it, if it takes longer to write and maintain automation script than to manually test it’s a waste of time and money
-->

---
layout: center
---
<h1>1. putting human behavior into code</h1>
<h1>2. making automation worth it</h1>
<!--
- but I want to say something about this presentation testing is no easy tasks
- I’m not here to tell you that you are doing your job wrong, or laugh at mistakes
- believe me, I made many of the mistakes I mention as well
- I hope to provide solutions for problems that are way too common in life of a tester
- because I truly and genuinely believe, that we can do things better
- and honestly, with rise of AI, we have to do things better - But Miroslav Bureś will be talking about that one
-->
