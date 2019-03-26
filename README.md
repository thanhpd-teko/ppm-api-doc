# Teko Open API OpenAPI Specification

[![Build Status](https://travis-ci.com/teko-vn/api-docs.svg?token=9i8z2rrAK7dzCRPGv6yq&branch=master)](https://travis-ci.com/teko-vn/api-docs)

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

1. Install [Node JS](https://nodejs.org/)
2. Clone repo and run `yarn install` in the repo root

### Usage

#### `yarn start`

Starts the development server.

#### `yarn build`

Bundles the spec and prepares web_deploy folder with static assets.

#### `yarn test`

Validates the spec.
