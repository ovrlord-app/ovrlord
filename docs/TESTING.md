# Testing Ovrlord

In effort to maintain a stable application Ovrlord is supported by automated testing

## End to End Testing

[Playwright](https://playwright.dev/) is used for End to End testing of the User facing features, keep tests atomic!

```bash
cd e2e
npm ci
npx playwright install --with-deps
npm test
```

## Frontend Unit Testing

Frontend unit tests are run with [Vitest](https://vitest.dev/).

Then you can run tests

```bash
task test-ui
```

### Conventions for Frontend Unit Tests

- Refer to [vitest documentation](https://vitest.dev/) for React component testing patterns
- Test files are named `{componentName}.test.tsx`
- Test files can be placed alongside source files as `{componentName}.test.tsx`

## Go Unit Testing

Run `task test-go` to run go tests