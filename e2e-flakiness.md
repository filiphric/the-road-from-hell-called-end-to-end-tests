---
layout: cover
---

# e2e flakiness

<!--
- flaky test is when we run a test and at some point it gives us a different result, without an obvious change in the code
- how does flakiness happen?
- let’s do the clap again
- what takes bigger part of your day? writing or debugging?
-->

---
layout: default
---

# e2e flakiness

```mermaid {fontSize: 40, scale: 2.4}
flowchart LR
A(Test script) -. commands .-> B(Application)
style A fill:#41B0F6,stroke-width:0px,color:#fff
style B fill:#41B0F6,stroke-width:0px,color:#fff
linkStyle 0 stroke:#fff,stroke-width:2px,color:white;
```

<style>
.mermaid {
  margin-top: 12%;
}

</style>

<!--
- what are we trying to do?
- run script that automates application
- integrating two systems - leads to integration hell
- and we all know what happens when a test fails 
- we get a test failure that looks like this
-->

---
layout: two-cols
---
# e2e flakiness

```plain
❌ Timed out retrying: Expected to find element, but never found it.
```

```plain
❌ failed because the element cannot be interacted with
```

```plain
❌ failed because the element is covered by another element
```

```plain
❌ failed because the page updated
```

```plain
❌ ...
```

<!-- 
- The main problem when dealing with e2e tests is the lack of context
- e2e test usually copies a user story
- when element is not found, it tells us nothing about what exactly failed
- this is especially problematic when dealing with flaky tests
- good news is that tools have gotten better at providing this context
 -->

---
layout: default
---

# e2e flakiness

:vscode-icons-file-type-cypress {class="w-20 h-20 block"}
<img src="/images/cypress-runner.png" />

<!--
- cypress timeline shows DOM snapshots and network communication
-->

---
layout: default
---

# e2e flakiness

:logos-playwright {class="w-20 h-20 block"}
<img src="/images/trace-viewer.png" />

<!--
- playwright trace-viewer also does snapshots and some other information
-->

---
layout: default
---

# e2e flakiness

<img src="/images/timeline.png" class="mt-30" />

<!--
- the way they function is like this
- everytime a command is called, a snapshot is made
- snapshot on get, click, xhr request,...
- same for playwright
- these are connected to a report
- but application is still doing stuff inbetween
-->

---
layout: default
---

# e2e flakiness

<img src="/images/timeline_2.png" class="mt-30" />

<!--
- the application under test is still doing stuff
- thes gaps is where flakiness happens - in these gaps
- input type - lost part of text
- clicked too soon
- lost an element,...
- so how do we fill these gaps?
-->

---
layout: default
---

# e2e flakiness

<img src="/images/timeline_3.png" class="mt-30" />

<!--
- more screenshots? video? - way too big
- 25 frames per second - apps are way faster
-->

---
layout: section
---
# fun fact:
<br>

The V8 engine that powers Node.js and Google Chrome can perform<br>
more than 1 billion operations per second.

If you tried capturing a video with such frequency, 1 second of such video<br>
would have 6 milliion terabytes.

<!-- 
- The V8 engine that powers Node.js and Google Chrome can perform more than 1 billion operations per second.
- If you tried capturing a video with such frequency, 1 second of such video would have 6 milliion terabytes.
- more than the fastest phantom camera
- so bad news is that to create something that would capture every test flake seems pretty impossible
- ok so this is what I do for living now 
- but not really like this
- I work with some of the best engineers in the world
- we don’t do snapshots
-->

---
layout: default
---
# e2e flakiness

<div class="grid grid-cols-2 gap-8">
<div>
  <img src="/images/replay_logo.png" class="mt-20 mb-10 w-20" />

  ```bash
  npx cypress run --browser replay-chromium
  ```
  ```bash
  npx playwright test --project replay-chromium
  ```
  <logos-playwright  class="mx-2 mt-4"/>
  <vscode-icons-file-type-cypress  class="mx-2 mt-4"/>
  <logos-webdriverio class="mx-2 mt-4"/>
  <logos-selenium class="mx-2 mt-4"/>
  <logos-puppeteer class="mx-2 mt-4"/>
  <vscode-icons-file-type-jest class="mx-2 mt-4"/>
</div>
<img src="/images/replay_devtools.png" class="mt-20 " />
</div>
<!-- 
- instead we created a browser - it’s essentially chrome, but it can record everything
- not only things you see, but also those you don’t see
- every line of code, functions, their parameters and outputs, react components and their props
- the recording that is created can be inspected in devtools
- So let’s take a look at a flaky test
-->

---
layout: default
---
# e2e flakiness

<div class="grid grid-cols-2 gap-8 items-center pt-14">
<div>

```js {*|2|3-5|6-7|*}
it('adds a product to cart', () => {
  cy.visit('/');
  cy.contains('Add to Cart')
    .should('be.visible')
    .click();
  cy.contains('Product added to cart!')
    .should('be.visible');
});
```

</div>
<div class="relative h-full w-full">
  <img class="absolute top-0 left-0" v-click="[0, 5]" src="/images/flaky.png" />
  <img class="absolute top-0 left-0" v-click="5" src="/images/flaky_failed.png" />
</div>
</div>

---
layout: section
---
# demo: debugging a flaky test

<!-- 
- https://app.replay.io/recording/4f19c5cc-50e2-490c-832b-9fa4d1cd64dc
- I got the recording here - play like a video both tests
- side panel two tests - see failed
- but as I mentioned, this recording can be examined with devtools
- jump to code - indication how many times a line of code was called
- xhr - let’s look at network & compare
- add to cart threw 400 - our first clue
- not sure what you do when I want to understand my code but I add console logs
- I can add console.logs to this recording
- add print statement - quantity in request (add color)
- where does quantity come from? - react app - print out the state variable
- there’s a certain lifecycle of our app 
- our test clicked too fast, our app wasn’t ready
- i need to make sure that I don’t click too soon
- end demo

-->

---
layout: default
---
# e2e flakiness

add wait:
```js {*|3|none}
it('adds a product to cart', () => {
  cy.visit('/');
  cy.wait(1000);
  cy.contains('Add to Cart').should('be.visible').click();
  cy.contains('Product added to cart!').should('be.visible');
});
```

add intercept:
```js {none|2,4}
it('adds a product to cart', () => {
  cy.intercept('/api/check-availability').as('availability')
  cy.visit('/');
  cy.wait('@availability');
  cy.contains('Add to Cart').should('be.visible').click();
  cy.contains('Product added to cart!').should('be.visible');
});
```

<!-- 
- how do we fix the test?
- but there is problem - flakes reveal hidden problems
- this could happen to a real user - they just need slow network and check availability response will take longer, they’ll click on that button too soon
- AND I actually don’t like the term "flaky test"
- guess what - if your app is flaky, your tests aren’t going to be stable either
-->

---
layout: default
---

<img src="/images/cory.png" class="w-150 m-auto pt-6" />

---
layout: default
---

<!-- 
- so let’s do exactly that
-->

parent component:
````md magic-move
```tsx
<Counter quantity={quantity} setQuantity={setQuantity} />
<AddToCartButton onClick={addToCart} />
```
```tsx
<Counter quantity={quantity} setQuantity={setQuantity} />
<AddToCartButton onClick={addToCart} isDisabled={quantity === 0} />
```
````

button component:
````md magic-move
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
}

const AddToCartButton = ({ onClick }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4'
    onClick={onClick} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
  isDisabled: boolean;
}

const AddToCartButton = ({ onClick, isDisabled }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4'
    onClick={onClick} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
  isDisabled: boolean;
}

const AddToCartButton = ({ onClick, isDisabled }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4'
    onClick={onClick}
    disabled={isDisabled} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
```tsx
interface AddToCartButtonProps {
  onClick: () => void;
  isDisabled: boolean;
}

const AddToCartButton = ({ onClick, isDisabled }: AddToCartButtonProps) => (
  <button 
    className='bg-pink-500 text-white font-semibold text-2xl px-4 py-2 rounded-sm my-4 disabled:opacity-20'
    onClick={onClick}
    disabled={isDisabled} >
    Add to Cart
  </button>
);

export default AddToCartButton;
```
````

<!--
- let’s add a new property
- [click] when the number is anything else than 0, isDisabled will be false
- [click] add it to our button as well
- [click] we’ll add an html attribute
- [click] and then add some styling so it’s semi transparent
-->

---
layout: default
---

<img src="/images/disabled_button.gif" class="w-200 m-auto" />

<!--
- you can see that click actually waits, until button is enabled
- it is enabled, when response comes back
-->
