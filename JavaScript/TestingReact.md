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

- name test file `ComponentName.test.js`, for layout.tsx -> layout.test.js

```js
import { render, screen } from "@testing-library/react";

test("check testing", () => {
  render(<ComponentName />);
  screen.debug();
});
```

## Reference

[React Testing Crash Course | Traversy Media](https://www.youtube.com/watch?v=OVNjsIto9xM)
