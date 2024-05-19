# package-version-action
[![Release](https://github.com/infra-blocks/package-version-action/actions/workflows/release.yml/badge.svg)](https://github.com/infra-blocks/package-version-action/actions/workflows/release.yml)
[![Self Test](https://github.com/infra-blocks/package-version-action/actions/workflows/self-test.yml/badge.svg)](https://github.com/infra-blocks/package-version-action/actions/workflows/self-test.yml)
[![Update From Template](https://github.com/infra-blocks/package-version-action/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infra-blocks/package-version-action/actions/workflows/update-from-template.yml)

This action extracts the version of a package. At the moment, it supports "npm" and "git" packages. It also
supports overriding the default file where the version is extracted from, where it makes sense. 

| Package Type | Default File | Supports Custom File | Description                                                                                                                                                                                                                                                               |
|:------------:|:------------:|:--------------------:|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     npm      | package.json |  :white_check_mark:  | The version is extracted from the `version` field of the `package.json` file.                                                                                                                                                                                             |
|     git      |     N/A      |         :x:          | The version is extracted from the git tag. Only semantic versioning tags of the form `v<major>.<minor>.<patch>` are looked at. Note that it requires the git tags be available on the git tree. Make sure to call `actions/checkout` with `fetch-depth=0` prior to using. 
|


## Inputs

| Name | Required  | Description                                                                                                                                                |
|:----:|:---------:|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type |   true    | The package type. Valid values include "npm", "git".                                                                                                       |
| file |   false   | The package file. When not provided, it defaults to the standard file of the package type. For example, for type "npm", the default file is "package.json" |

## Outputs

|  Name   | Description           |
|:-------:|-----------------------|
| version | The extracted version |

## Permissions

N/A

## Usage

### With NPM

```yaml
jobs:
  do-stuff:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
      - uses: infra-blocks/package-version-action@v1
        id: package-version
        with:
          type: npm
      - run: echo "The current package version is ${{ steps.package-version.outputs.version }}" 
```

### With Git tags

```yaml
jobs:
  do-stuff:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      - uses: infra-blocks/package-version-action@v1
        id: package-version
        with:
          type: git
      - run: echo "The current package version is ${{ steps.package-version.outputs.version }}" 
```
