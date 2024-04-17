# package-version-action
[![Release](https://github.com/infrastructure-blocks/package-version-action/actions/workflows/git-tag-semver-from-label.yml/badge.svg)](https://github.com/infrastructure-blocks/package-version-action/actions/workflows/git-tag-semver-from-label.yml)
[![Self Test](https://github.com/infrastructure-blocks/package-version-action/actions/workflows/self-test.yml/badge.svg)](https://github.com/infrastructure-blocks/package-version-action/actions/workflows/self-test.yml)
[![Update From Template](https://github.com/infrastructure-blocks/package-version-action/actions/workflows/update-from-template.yml/badge.svg)](https://github.com/infrastructure-blocks/package-version-action/actions/workflows/update-from-template.yml)

## Inputs

| Name | Required  | Description                                                                                                                                                |
|:----:|:---------:|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| type |   true    | The package type. Valid values include "npm".                                                                                                              |
| file |   false   | The package file. When not provided, it defaults to the standard file of the package type. For example, for type "npm", the default file is "package.json" |

## Outputs

|  Name   | Description           |
|:-------:|-----------------------|
| version | The extracted version |

## Permissions

N/A

## Usage

```yaml
jobs:
  do-stuff:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
      - uses: infrastructure-blocks/package-version-action@v1
        id: package-version
        with:
          type: npm
      - run: echo "The current package version is ${{ steps.package-version.outputs.version }}" 
```
