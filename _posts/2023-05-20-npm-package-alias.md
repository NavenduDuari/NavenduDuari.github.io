---
layout: post
title: NPM Package Alias
date: 2023-05-20 01:36 +0530
image: /assets/images/npm_package_alias_banner.jpg
---

## Introduction
In my current job, we recently encountered a scenario where we needed to upgrade google-cloud pubsub to version 3 for one microservice,
while still maintaining version 2 for the other microservices. Thankfully, we were able to leverage the npm aliasing feature to solve this issue.

> Package alias allows installation of packages with custom names.
{: .prompt-tip }

## Installation
To install the package `lodash` with a custom name `my_lodash`, we can add the below line in `package.json`{: .filepath} and run `npm install` to install the package:
```json
  "dependencies": {
    "my_lodash": "npm:lodash"
  }
```
{: file='package.json'}

Or, we can install it using the below command:
`npm install my_lodash@npm:lodash --save`

We can specify a specific package version during installation:

```json
  "dependencies": {
    "lodash_v3": "npm:lodash@^3.10.1",
    "lodash_v4": "npm:lodash@^4.17.21",
  }
```
{: file='package.json'}

Or, we can install it using the below command:
`npm install lodash_v3@npm:lodash@3.10.1 --save`

While installation it will use the specific name provided when it adds it to `node_modules`{: .filepath}.
```
├── node_modules
│   ├── lodash_v3
│   └── lodash_v4
├── package-lock.json
├── package.json
```

## Usage

We can use the custom name while importing the module.
```javascript
import { pluck } from 'lodash_v3' // pluck is removed in v4
import { reverse } from 'lodash_v4' // reverse is not introduced till v3
```

## Conclusion
Similar to the above example, We resolved the issue of conflicting package versions by installing two separate versions of google-cloud pubsub under different names.
