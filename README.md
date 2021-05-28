## Introduction
This repo provides a guide for integrating the `semantic-release` npm library into an existing repo. Here, you will find instructions on:
- Preparing your repo for use with `semantic-release`
- Installing and configuring `semantic-release`
- Configuring `semantic-release` to work with GitHub Actions

## Prep work
`semantic-release` helps to automate changelog documentation and to determine the next semantic version of your release, among other things. To do this accurately, the commits in your repo must follow [Conventional Commits formatting](https://www.conventionalcommits.org/en/v1.0.0/). 

To help us with this, we will be installing [`commitlint`](https://github.com/conventional-changelog/commitlint) and [`husky`](https://typicode.github.io/husky/#/?id=manual) to enforce proper commit formatting through Git hooks. What this means is that we will use Git hooks to prevent commits whose messages do not meet the required formatting standard from being committed into the repo.

### Installing `commitlint`
```
# Install commitlint cli and conventional config
npm install --save-dev @commitlint/{config-conventional,cli}
# For Windows:
npm install --save-dev @commitlint/config-conventional @commitlint/cli

# Configure commitlint to use conventional config
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

### Installing `husky`
```
# Install Husky v6
npm install husky --save-dev

# Activate hooks
npx husky install

# Add hook
npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
```
