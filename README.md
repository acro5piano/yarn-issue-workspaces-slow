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

Result:

<!-- ### case 4 -->
<!--  -->
<!-- Result: **Failed** -->

<!-- Even though all directories are cached, `yarn install` tries to install from scratch: -->
<!--  -->
<!-- ``` -->
<!-- #!/bin/bash -eo pipefail -->
<!-- yarn install -->
<!-- yarn install v1.10.1 -->
<!-- [1/4] Resolving packages... -->
<!-- [2/4] Fetching packages... -->
<!-- [3/4] Linking dependencies... -->
<!-- [4/4] Building fresh packages... -->
<!-- success Saved lockfile. -->
<!-- Done in 0.53s. -->
<!-- ``` -->
<!--  -->
<!-- https://circleci.com/gh/acro5piano/yarn-issue-workspaces-slow/31 -->
<!--  -->
