---
layout: cover
---
# abstractions

<!-- 
- We all learn the DRY principle don’t repeat yourself
- some of you shaking heads saying you should stick to WET principle - write everything twice
- but while you can do a good job of learning about it, it’s also important to know if, how, when to use it
- so let’s talk how abstractions while inherently good can become problematic
 -->
---
layout: two-cols
---
# abstractions

test:
```js {*|3}
it('opens menu', () => {
  cy.visit('/')
  cy.openMenu()
})
```
custom command:
```js
Cypress.Command.add('openMenu', () => {
  cy.get('[data-test="menu"]')
    .click()
    .find('[data-test="menu-item"]')
    .click()
})
```

::right::
<div class="grid items-center h-full">
<img src="/images/board.png" />
</div>

<!-- 
- **three dot button** opens a menu
- used all the time when testing this app
- [click] so we create a custom command to abstract it
- so far so good, but then
 -->

---
layout: two-cols
---
# abstractions

test:
```js {*|3}
it('opens menu', () => {
  cy.visit('/')
  cy.openMenu("Delete board")
})
```

custom command:
```js {*|5}{at:1}
Cypress.Command.add('openMenu', (item) => {
  cy.get('[data-test="menu"]')
    .click()
    .find('[data-test="menu-item"]')
    .contains(item)
    .click()
})
```

::right::
<div class="grid items-center h-full">
<img src="/images/board2.png" />
</div>

<!-- 
- we have multiple items
- [click]
- so to keep this abstraction we add a parameter so that we can pass the name of the item we want to pick from menu
 -->

---
layout: two-cols
---

# abstractions

test:
```js {*|3}
it('opens menu', () => {
  cy.visit('/')
  cy.openMenu("Delete board", true)
})
```

custom command:

```js {*|1|2|1-3}{at:1}
Cypress.Command.add('openMenu', (item, isList = false) => {
  const area = isList ? '[data-test="list-area"]' : '[data-test="header"]'
  cy.get(`${area} [data-test="menu"]`)
    .click()
    .find('[data-test="menu-item"]')
    .contains(item)
    .click()
})
```

::right::
<div class="grid items-center h-full">
<img src="/images/board3.png" />
</div>

<!--
- but now we are introduced to another problem, because the menu component can actually be used for the main panel or in the todo lists
- [click] so we introduce a condition that will enable us to decide which menu we want to click 
- based on that condition [click]
- we fill the selector [click]
- we pass it into get command
-->

---
layout: two-cols
---

# abstractions

test:
```js {*|3}
it('opens menu', () => {
  cy.visit('/')
  cy.openMenu("Delete board", true, 0)
})
```

custom command:

```js {*|1,4|*}{at:1}
Cypress.Command.add('openMenu', (item, isList = false, index = 0) => {
  const area = isList ? '[data-test="list-area"]' : '[data-test="header"]'
  cy.get(`${area} [data-test="menu"]`)
    .eq(index)
    .click()
    .find('[data-test="menu-item"]')
    .contains(item)
    .click()
})
```

::right::
<div class="grid items-center h-full">
<img src="/images/board4.png" />
</div>

<!--
- And now we get to another problem, because there can be multiple todo lists
- [click] so we add an index number
- [click] when we now look at our custom command it has gotten way too complicated and we should probably refactor it
-->

---
layout: two-cols
---

# abstractions
```js
it('opens menu', () => {
  cy.visit('/')
  cy.openMenu()
})
```
::right::

```mermaid {fontSize: 40, scale: 2}
flowchart LR
B(Test) --> A(Abstraction)
C(Test) --> A(Abstraction)
D(Test) --> A(Abstraction)
style A fill:#F02D5E,stroke-width:0px,color:#fff
style B fill:#41B0F6,stroke-width:0px,color:#fff
style C fill:#41B0F6,stroke-width:0px,color:#fff
style D fill:#41B0F6,stroke-width:0px,color:#fff
linkStyle 0,1,2 stroke:#fff,stroke-width:2px,color:white;
```

<style>
.two-columns {
  gap: 1rem;
  grid-template-columns: 3fr 5fr !important;
}

.slidev-code-wrapper {
  padding-top: 35%
}
</style>

<!-- 
- but we have now introduced a problem into our test suite
- because we have all these tests using our abstraction
-->

---
layout: two-cols
---

# abstractions
```js
it('opens menu', () => {
  cy.visit('/')
  cy.openMenu()
})
```
::right::
```mermaid {fontSize: 40, scale: 2}
flowchart RL
A(Abstraction) --> B(Test)
A(Abstraction) --> C(Test)
A(Abstraction) --> D(Test)
style A fill:#F02D5E,stroke-width:0px,color:#fff
style B fill:#41B0F6,stroke-width:0px,color:#fff
style C fill:#41B0F6,stroke-width:0px,color:#fff
style D fill:#41B0F6,stroke-width:0px,color:#fff
linkStyle 0,1,2 stroke:#fff,stroke-width:2px,color:white;
```

<style>
.two-columns {
  gap: 1rem;
  grid-template-columns: 3fr 5fr !important;
}

.slidev-code-wrapper {
  padding-top: 35%
}
</style>

<!--
- but when we change the abstraction, it’s going to affect all oue tests
- and I’m not saying abstraction is a bad thing
- it’s that there are lot of cases of them being used, just because they are a "good pracitce"
- when starting new project:
- "not useful now, but it will be useful in the future" - I just demonstrated it might actually make stuff more complicated
- no one can predict future
- don’t be afraid to write plain commands
-->
