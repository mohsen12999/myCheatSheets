# Testing React

- why test
  - Goal: check whether an application behave as expected
  - Safeguard against unwanted behavior when changes are made
  - Automated, and efficient on the long-term
- test priority
  - High value features
  - Edge case in high value features
  - Things that are easy to break
  - Basic React component testing: User interface, Conditional rendering, Utils/Hooks

## writing test

### Unit test

- name test file `ComponentName.test.js`, for layout.tsx -> layout.test.js

```js
import { render, screen } from "@testing-library/react";

test("check testing", () => {
  render(<ComponentName />);
  screen.debug();
});
```

- we can pass data for component.
- first assert

```js
expect(screen.getByRole("button", { name: /pay/i })).toBeEnabled();
```

- sometime, we need time to evaluate, we can use async method

```js
test("pay button at initial must be disable", async () => {
  render(<ComponentName />);
  expect(await screen.findByRole("button", { name: /pay/i })).toBeDisabled();
});
```

- in form better use `getByLabelText`, if not can use`getByPlaceHolder` or `getByTitle`
- more info [Testing Library - About Queries](https://testing-library.com/docs/queries/about)

```js
import userEvent from "@testing-library/user-event";

test("pay button enable after fill form", async () => {
  render(<ComponentName />); // Arrange

  userEvent.type(screen.getByPlaceholderText(/amount/i), "500"); // Act

  expect(await screen.findByRole("button", { name: /pay/i })).toBeEnabled(); // Assert
});
```

### integration test

- testing a functionality like combine of some unit testing, like user use our application (user flow)

```js
test("testing btn behavior", async () => {
  render(<ComponentName />);

  expect(await screen.findByRole("button", { name: /pay/i })).toBeDisabled();

  userEvent.type(screen.getByPlaceholderText(/amount/i), "500");

  expect(await screen.findByRole("button", { name: /pay/i })).toBeEnabled();
});
```

### end to end test

- install `cypress` -> `npm i -D cypress @testing-library/cypress`
- open cypress with `npm run cypress open`
- for supporting cypress go to `cypress/support/commands.js`

```js
import "cypress @testing-library/cypress/add-commends";
```

- make test folder in cypress folders like integration folder -> payment_spec.js

```js
const { cy } = require("data-fns/locale");
const { v4: uuidv4 } = require("uuid");

describe("payment", () => {
  it("user can make payment", () => {
    // login
    cy.visit("/login"); // go to login page

    cy.findByRole("textbox", { name: /username/i }).type("johnDou"); // type username
    cy.findByLabelText("password").type("s3cret"); // type password
    cy.findByRole("checkbox", { name: /remember me/i }).check(); // check remember me

    cy.findByRole("button", { name: /sign in/i }).click(); // click button

    // check balance
    let oldBalance;
    cy.get("[data-test=sidebar-user-balance]").then($balance => oldBalance=$balance.text());

    // click on new button
    cy.findByRole("button", { name: /new/i }).click();

    // search for user
    cy.findByRole("textbox").type("devon backer");
    cy.findByText(/devon backer/);.click();

    // add payment and note and click pay button
    const paymentAmount = "5.00";
    cy.findByPlaceholderText(/amount/i).type(paymentAmount);
    const note = uuidv4() // make random note
    cy.findByPlaceholderText(/add a note/i).type(note);
    cy.findByRole("button", { name: /pay/i }).click();

    // return to transaction page
    cy.findByRole("button", { name: /return to transaction page/i }).click();

    // go to personal payment
    cy.findByRole("tab", { name: /mine/i }).click();

    // click on payment
    // cy.findByText(note);.scrollIntoView(); // for show in scroll list but sometime not work
    // cy.findByText(note);.click(); // find base on our random note
    cy.findByText(note);.click({force:true}); // work if the component was not visible

    // verify if payment was made
    cy.findByText("-$${paymentAmount}").should('be.visible'); //-$5.00
    cy.findByText(note).should('be.visible'); //-$5.00

    // verify if payment amount was deducted
    cy.get("[data-test=sidebar-user-balance]").then($balance => {
      const convertedOldBalance = parsFloat(oldBalance.replace(/\$|,/g,""));
      const convertedNewBalance = parsFloat($balance.text().replace(/\$|,/g,""));

      expect(convertedNewBalance-convertedNewBalance).to.equal(parsFloat(paymentAmount));
    });

  });
});
```

- can use `testing playground` plugin for chrome to find query for element
- if element is dynamic, can add `data-test` property for element to find easier

## Reference

[React Testing Crash Course | Traversy Media](https://www.youtube.com/watch?v=OVNjsIto9xM)
