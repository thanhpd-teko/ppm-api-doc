# Teko Open API OpenAPI Specification

[![Build Status](https://travis-ci.com/teko-vn/api-docs.svg?branch=master)](https://travis-ci.com/teko-vn/api-docs)

## Steps to finish

1. Enable [Travis](https://docs.travis-ci.com/user/getting-started/#To-get-started-with-Travis-CI%3A) for your repository (**note**: you already have `.travis.yml` file)
1. [Create GitHub access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/); select `public_repo` on `Select scopes` section.
1. Use the token value as a value for [Travis environment variable](https://docs.travis-ci.com/user/environment-variables/#Defining-Variables-in-Repository-Settings) with the name `GH_TOKEN`
1. Make a test commit to trigger CI: `git commit --allow-empty -m "Test Travis CI" && git push`
1. Wait until Travis build is finished. You can check progress by clicking on the `Build Status` badge at the top
1. **[Optional]** You can setup [custom domain](https://help.github.com/articles/using-a-custom-domain-with-github-pages/) (just create `web/CNAME` file)
1. **[Optional]** If your API is public consider adding it into [APIs.guru](https://APIs.guru) directory using [this form](https://apis.guru/add-api/).
1. Delete this section ❌

## Links

- [Reference Documentation (ReDoc)](https://teko-vn.github.io/api-docs/)
- [SwaggerUI](https://teko-vn.github.io/api-docs/swagger-ui/)
- OpenAPI Raw Files: [JSON](https://teko-vn.github.io/api-docs/openapi.json) [YAML](https://teko-vn.github.io/api-docs/openapi.yaml)

**Warning:** All above links are updated only after Travis CI finishes deployment

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
