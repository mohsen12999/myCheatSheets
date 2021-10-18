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
expect(screen.getByRole('button',{name: /pay/i })).toBeEnabled();
```

- sometime, we need time to evaluate, we can use async method

```js
test("pay button at initial must be disable", async () => {
  render(<ComponentName />);
  expect(await screen.findByRole('button',{name: /pay/i })).toBeDisabled();
});
```

- in form better use `getByLabelText`, if not can use`getByPlaceHolder` or `getByTitle`
- more info [Testing Library - About Queries](https://testing-library.com/docs/queries/about)

```js
import userEvent from "@testing-library/user-event";

test("pay button enable after fill form", async () => {
  render(<ComponentName />); // Arrange

  userEvent.type(screen.getByPlaceholderText(/amount/i),"500"); // Act

  expect(await screen.findByRole('button',{name: /pay/i })).toBeEnabled(); // Assert
});
```

### integration test

- testing a functionality like combine of some unit testing, like user use our application (user flow)

```js
test("testing btn behavior", async () => {
  render(<ComponentName />);
  
  expect(await screen.findByRole('button',{name: /pay/i })).toBeDisabled();

  userEvent.type(screen.getByPlaceholderText(/amount/i),"500");

  expect(await screen.findByRole('button',{name: /pay/i })).toBeEnabled();
});
```

### end to end test

- install `cypress` -> `npm i -D cypress @testing-library/cypress`
- open cypress with `npm run cypress open`
- for supporting cypress go to `cypress/support/commands.js`

```js
import "cypress @testing-library/cypress/add-commends"
```

## Reference

[React Testing Crash Course | Traversy Media](https://www.youtube.com/watch?v=OVNjsIto9xM)
