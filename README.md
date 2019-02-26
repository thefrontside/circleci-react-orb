# circleci-react-orb

[CircleCI React Orbs](https://circleci.com/orbs/registry/orb/thefrontside/react) makes it easy to run tests, linting and code coverage on CircleCI.

## Features

- Includes the following jobs: `install`, `test`, `eslint`, `stylelint` and `build`
- Allows `test`, `eslint`, `stylelint` and `build` to run in parallel
- `install` job caches NPM dependencies
- `test` shows test summary in CircleCI
- `eslint` shows test summary in CircleCI
- `stylelint` stores generated reports in artifacts

## Limitations

- Currently only supports yarn (we'll add NPM support shortly)

## Example

```yaml
version: 2.1

orbs:
  react: thefrontside/react@0.1.0

workflows:
  # push workflow will be triggered when a new pull request is created
  push:
    jobs:
      - react/install
      - react/eslint:
          requires:
            - react/install
      - react/stylelint:
          requires:
            - react/install
      - react/test:
          requires:
            - react/install
      - react/coverage:
          requires:
            - react/install
  # push workflow will be triggered when a build is created
  build:
    jobs:
      - react/install
      - react/eslint:
          requires:
            - react/install
      - react/stylelint:
          requires:
            - react/install
      - react/test:
          requires:
            - react/install
      - react/build:
            requires:
              - react/install
```