---
layout: cover
---
# data management

---
layout: default
---
# data management

<!-- 
- data management can be hell, because we are all moving on this spectrum when testing
- and there are problems on both sides of this spectrum
- on the left, we deal with parallelization, data cleanup, making sure that data structures are up to date
- on the right, we deal with data mocking, complicated data setup, usually done with UI
- and it can all become this weird entangled spaghetti of a system
- to clean this up, usually a model us proposed:
 -->

```mermaid {fontSize: 40, scale: 2.4}
flowchart LR
A(Full control) -. data .- B(No control)
style A fill:#41B0F6,stroke-width:0px,color:#fff
style B fill:#41B0F6,stroke-width:0px,color:#fff
linkStyle 0 stroke:#fff,stroke-width:2px,color:white;
```

<!-- 
- data management should be added at the beginning
 -->

<style>
.mermaid {
  margin-top: 12%;
}

</style>

---
---
# data management

```mermaid {fontSize: 40, scale: 2.4}
flowchart LR
A(Arrange) --> B(Act) --> C(Assert)
style A fill:#41B0F6,stroke-width:0px,color:#fff
style B fill:#41B0F6,stroke-width:0px,color:#fff
style C fill:#41B0F6,stroke-width:0px,color:#fff
linkStyle 0,1 stroke:#fff,stroke-width:2px,color:white;
```

<!-- 
- but it’s oftentimes added into the "act" part
- if you are starting with test automation, you might run into trouble with parallelization later
- couple of recommendations
 -->
<style>
.mermaid {
  margin-top: 12%;
}

</style>

---
---
# data management

```mermaid {fontSize: 40, scale: 2.4}
flowchart LR
A(Arrange) --> B(Act) --> C(Assert)
style A fill:#41B0F6,stroke-width:0px,color:#fff
style B fill:#F02D5E,stroke-width:0px,color:#fff
style C fill:#41B0F6,stroke-width:0px,color:#fff
linkStyle 0,1 stroke:#fff,stroke-width:2px,color:white;
```
<style>
.mermaid {
  margin-top: 12%;
}

</style>

---
layout: two-cols
---
# data management
✅
```js
before()
beforeEach()
```

:logos-playwright
```js
const authFile = 'playwright/.auth/user.json';
await page.context().storageState({ path: authFile });
```

:vscode-icons-file-type-cypress
```js
cy.session(id, setup, options)
```

::right::
<div class="pt-23">
&nbsp;
</div>
❌
```js
// cleanup
after()
afterEach()
```

```js
beforeEach(() => {
  cy.visit('/login')
  cy.get('[data-test=name]').type(name)
  cy.get('[data-test=password]').type('s3cr3t')
  cy.get('form').contains('Log In').click()
  cy.url().should('contain', '/login-successful')
})
```

<!-- 
- not after each, because if you have two tests, faulty cleanup will fail the test after
- there also might be problem with data created during tes
 -->

<style>
.two-columns {
  gap: 4rem;
  grid-template-columns: 1fr 1fr !important;
}
</style>