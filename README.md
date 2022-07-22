# Shared Workflows by Syntro

This repository contains prebuilt workflows and required containers for
automated testing, building & delivery of projects (mostly
[Silverstripe](https://silverstripe.org) related).

## Usage - Silverstripe Project

This repository provides a ready-to-use testsuite for your Silverstripe project.
It provides the following checks:

* PHPUnit
* PHPStan
* Behat
* PHPcs

Usage is straightforward:

```yml
# ...
jobs:
  silverstripe:
    name: 🧰 Silverstripe Testsuite
    uses: syntro-opensource/workflows/.github/workflows/silverstripe.yml@master
    with:
      phpunit: true
      phpunit_suite: app/tests/
      # phpunit_config_file:
      # phpunit_php_version: '8.1'
      phpstan: true
      phpstan_dir: app/src/
      # phpstan_php_version: '8.1'
      phpcs: true
      phpcs_dir: app/
      # behat: false
      # behat_php_version: '8.1'
```

Each check can be configured using inputs.

## Usage - Silverstripe Modules

This repository provides a testsuite for silverstripe modules. The testsuite
is used as the standard in our modules and checks Code in a fixed range of
php and CMS versions:

* PHP 7.4
* PHP 8.0
* PHP 8.1

* CMS 4.9
* CMS 4.10
* CMS 4.11

Usage is straightforward:

```yml
# ...
jobs:
  silverstripe-module:
    name: 🧰 Silverstripe Module Testsuite
    uses: syntro-opensource/workflows/.github/workflows/silverstripe-module.yml@master
    with:
      phpunit: true
      # phpunit_config_file:
      phpstan: true
      # phpstan_config:
      # phpstan_bootstrap:
      phpcs: true
```


Each check can be configured using inputs.

## Usage - Frontend Checks

This repository also provides a testsuite for client-side code. The suite checks:

* ESlint
* Stylelint

Usage is straightforward:

```yml
# ...
jobs:
  silverstripe-client:
    name: 📦 Client Testsuite
    uses: syntro-opensource/workflows/.github/workflows/client.yml@master
    with:
      eslint: true
      eslint_dir: client/src/seo-field/
      eslint_configfile: client/src/seo-field/.eslintrc
      # eslint_ext:
      # eslint_max-warnings:
      stylelint: true
      stylelint_glob: client/src/seo-field/**/*.scss
      # stylelint_max-warnings:
```
Each check can be configured using inputs.
