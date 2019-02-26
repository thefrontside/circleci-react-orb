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
- Current Orb assumes: Create React App, Jest, ESLint and Stylelint
- TypeScript not supported yet, but will be in the future

## Basic setup

The smallest meaningful setup is to run tests on every PR. To do this, you need the following configuration.

```yaml
version: 2.1

orbs:
  react: thefrontside/react@0.1.0

workflows:
  # push workflow will be triggered when a new pull request is created
  push:
    jobs:
      - react/install
      - react/test
          requires:
            - react/install
```

## Adding ESLint to your project

For `eslint` to run successfully, you need an `eslint` script to be present in your package.json. 

You can add it by doing the following,

1. `yarn add --dev eslint`
2. Add `eslintConfig` to package.json or create an `.eslintrc` file. The minimum configuration is this:
  ```json
  {
    ...
    "eslintConfig": {
      "extends": "react-app"
    }
    ...
  }
  ```
3. Add `eslint` script to package.json
   ```json
   {
     "scripts": {
       ...
       "eslint": "eslint ./",
     }
   }
   ```
4. ⛴ it.

## Adding Stylelint to your project

For `stylelint` to run succesfully, you need an `stylelint` script to be present in your package.json

You can add it by doing the following,

1. `yarn add --dev stylelint stylelint-config-standard stylelint-junit-formatter`
2. Create a `.stylelintrc.js` file with the following
   ```js
    module.exports = {
      extends: 'stylelint-config-standard'
    };
   ```
3. Add `stylelint` script to package.json
   ```json
   {
     "script": {
      "stylelint": "stylelint \"src/**/*.css\""
     }
   }
   ```
4. 🚢 it.

## Contributing

* All PR are welcome. 
* Anything addressed in Limitation is SUPER welcome.
* Adding tests to `.circleci/config.yml` makes it easier to accept PRs

This project uses Orb testing workflow described in [orb-tools-orb](https://github.com/CircleCI-Public/orb-tools-orb). 
When you create a PR with a change, it'll automatically run tests and verify the orb. 

You can save yourself a bit of time by running the following before creating the PR,

### Validate the ORB

```bash
circleci config pack src | circleci config validate
```

### Validate the config

```bash
circleci config validate .circleci/config.yml
```

## Happy shipping!
