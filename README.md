[![CircleCI](https://circleci.com/gh/acro5piano/yarn-issue-workspaces-slow.svg?style=svg)](https://circleci.com/gh/acro5piano/yarn-issue-workspaces-slow)

# yarn-issue-workspaces-slow

Investigation for slow yarn install when workspaces enabled

# Issue

`yarn install` takes a lot of time when using `yarn workspaces`.

# Approach

Run `yarn install` in CircleCI with various patterns.

# Result

### case 1

- version matches with workspace and @yiws/utils
- cache dir
  - node_modules

Result: Works!

### case 2

- version mis-matches with workspace (ky: ^0.14.0) and @yiws/utils (ky: ^0.13.0)
- cache dir
  - node_modules
  - packages/utils/node_modules

Result: Works!

### case 3

- version matches with workspace (js-yaml: ^3.13.1) and @yiws/utils (same)
- cache dir
  - node_modules
  - packages/utils/node_modules

Result: Works!

### case 4

- minor version mis-matches with workspace (js-yaml: ^3.13.1) and @yiws/utils (js-yaml: ^2.0.0)
- cache dir
  - node_modules
  - packages/utils/node_modules

Result: Works!

### case 5

- make @yiws/app depends on @yiws/utils: 1.0.0

Result: Works!

### case 6

- add a lot of deps (ported from my private repository)

Result: Works!

### case 7

- add a lot of deps into child repo

Result:
