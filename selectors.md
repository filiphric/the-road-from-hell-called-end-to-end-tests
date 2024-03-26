---
layout: cover
---
# selectors
<!-- 
- another pain point
- I still find it kinda wild that selectors are still a problem
- but it is still something I see people struggling with, and it can indeed be a hellish nightmare
- good news is that approach is evolving
 -->

---
layout: default
---

# selectors

:logos-selenium{class="w-20 h-20 block my-10"} 
```java
_driver.FindElement(By.Id("layout"));
_driver.FindElement(By.ClassName("menu-item"));
_driver.FindElement(By.CssSelector(".menu-item a"));
_driver.FindElement(By.LinkText("Click me!"));
_driver.FindElement(By.Name("password"));
_driver.FindElement(By.PartialLinkText("Click"));
_driver.FindElement(By.TagName("a"));
_driver.FindElement(By.XPath("//*[@id='panel']/div/h1"));
```

<!--
- id, className, css, selector, link text, tag, xpath
-->

---
layout: two-cols
---

# selectors

:vscode-icons-file-type-cypress {class="w-20 h-20 block my-10"} 
parent:
```js
cy.get('[data-cy="menu-item"]')
cy.contains('Click me!')
```
::right::
child:
```js
cy.children()
cy.closest()
cy.eq()
cy.filter()
cy.find()
cy.first()
cy.focused()
cy.last()
cy.next()
cy.nextAll()
cy.nextUntil()
cy.not()
cy.parent()
cy.parents()
cy.parentsUntil()
cy.prev()
cy.prevAll()
cy.prevUntil()
cy.root()
cy.shadow()
cy.siblings()
```

<style>
.two-columns {
  gap: 4rem;
  grid-template-columns: 1fr 1fr !important;
}
</style>

<!--
- cypress threw all this away parent/child, two step approach
- select by text or query - then filter out stuff
-->
---
---
<img src="/images/cypress_selectors.png" class="w-5/6 m-auto" />

<!-- 
- came with suggestion - add your own data-cy attributes
- I think adding your own data-cy selectors was a very good push
- it makes tests more stable, forces developers and testers to work together
- I strongly believe that more collaboration the better
 -->


---

# selectors

:logos-playwright {class="w-20 h-20 block my-10"} 

```js
page.getByRole()
page.getByText()
page.getByLabel()
page.getByPlaceholder()
page.getByAltText()
page.getByTitle()
page.getByTestId()
```

<!--
- Playwright came with this opinionated approach
- Michal Drajna is going to have a great talk on all things Playwright, make sure to stay in the room after this one
- really great IMO, pushed the community to use accessibility selector
- I think this might probably be the best approach, not because you are killing two birds with one stone, but for two reasons
  - tests should resemble user behavior
  - frameworks we use should inspired good practices
- accessibility will be a requirement soon, some directives from EU are already in place
-->

---
layout: section
---

# Tests should be easy to read. Selectors are a big part of that

<!--
- using such selectors will make tests more readable
- I’m pushing a lot for test readability
- good selectors are a big part of that
- The reason for this is debugging
-->
