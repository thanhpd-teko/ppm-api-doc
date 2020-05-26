# Teko Open API OpenAPI Specification

[![CircleCI](https://circleci.com/gh/teko-vn/api-docs/tree/master.svg?style=svg)](https://circleci.com/gh/teko-vn/api-docs/tree/master)

## Working on specification

### Folder Structure

#### spec/openapi.yaml

- This file describes the whole Teko API ecosystem
- tags: Each tag equals to a resource endpoint
- x-tagGroups: describes how tag in tags is grouped (should be by service).
  ```
    tags:
        - name: Vouchers
        description: Provides apis for voucher service
    x-tagGroups:
        - name: Offline Sales
        tags:
            - Vouchers
        ...
  ```
  The code above make Voucher API to show as a child to Offline Sales group

#### spec/components

- This is where you declare your [components](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md#componentsObject)

#### spec/paths

- This is where you declare your api's [paths](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md#pathsObject)
- Write each path specification in separate file
- Filename is mapped to path by replacing `@` with `/`, i.e. `vouchers@{voucher_code}.yaml` matches to `vouchers/{voucher_code}` path
- _Remember to declare tag inside your path specification same to what you declared in openapi.yaml file_
  ```
  get:
      tags:
          - Vouchers
      ...
  ```

## Creating or Updating an API

- In case of creating an API, please follow the _Working on specification_ section above.
- When your specification is ready, create a pull request and assign to tien.dv@teko.vn.

## Testing your changes locally

1. Install [Node JS](https://nodejs.org/):
   - Using `yarn`: `node`>=10.14.0.
   - Using `npm`: `node`>=8.15.x.
2. Clone repo and run `yarn install` or `npm install` in the repo root

### Usage

#### `yarn start`

#### `npm run start` (with `npm`)

Starts the development server.

#### `yarn build`

#### `npm run build` (with `npm`)

Bundles the spec and prepares web_deploy folder with static assets.

#### `yarn test`

#### `npm run test` (with `npm`)

Validates the spec.
