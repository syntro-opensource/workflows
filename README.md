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
    uses: syntro-opensource/workflows/.github/workflows/silverstripe.yml@5
    with:
      phpunit: true
      phpunit_suite: app/tests/
      # phpunit_config_file:
      # phpunit_php_version: '8.1'
      # phpunit_build_graphql: false
      phpstan: true
      phpstan_dir: app/src/
      # phpstan_php_version: '8.1'
      phpcs: true
      phpcs_dir: app/
      # behat: false
      # behat_php_version: '8.1'
```

### Working with Private Repositories
You can enable an SSH-Client to clone private repositories described in `composer.json`. 
**Please make sure you understand the risks of adding private keys to GitHub workflow Runs!**
This feature can be enabled as follows:
```yml
# ...
jobs:
  silverstripe:
    name: 🧰 Silverstripe Testsuite
    uses: syntro-opensource/workflows/.github/workflows/silverstripe.yml@5
    with:
        # ...
        uses_private_repos: true
        uses_private_keys: |
            ${{ secrets.YOURPRIVATEKEY }}
```
We use [webfactory/ssh-agent](https://github.com/marketplace/actions/webfactory-ssh-agent) to
enable this feature. You can find more information there.


> For Silverstripe 4 related Checks, use the [`4` branch](https://github.com/syntro-opensource/workflows/tree/4).

Each check can be configured using inputs.

## Usage - Silverstripe Modules

This repository provides a testsuite for silverstripe modules. The testsuite
is used as the standard in our modules and checks Code in a fixed range of
php and CMS versions.

Usage is straightforward:

```yml
# ...
jobs:
  silverstripe-module-5:
    name: 🧰 Silverstripe Module Testsuite 5
    uses: syntro-opensource/workflows/.github/workflows/silverstripe-module-5.yml@master
    with:
      phpunit: true
      # phpunit_config_file:
      phpstan: true
      # phpstan_config:
      # phpstan_bootstrap:
  silverstripe-module-6:
    name: 🧰 Silverstripe Module Testsuite 6
    uses: syntro-opensource/workflows/.github/workflows/silverstripe-module-6.yml@master
    with:
      phpunit: true
      # phpunit_config_file:
      phpstan: true
      # phpstan_config:
      # phpstan_bootstrap:
  silverstripe-module-codecoverage:
    name: 📊 Silverstripe Code Coverage
    uses: syntro-opensource/workflows/.github/workflows/silverstripe-module-codecoverage.yml@master
    with:
      php_version: 8.3
      silverstripe_version: 6.0
  silverstripe-phpcs:
    name: 🧹 Silverstripe PHPCS
    uses: syntro-opensource/workflows/.github/workflows/silverstripe-phpcs.yml@master
    with:
      dir: src/
```


Each check can be configured using inputs.

> For Silverstripe 4 related Checks, use the [`4` branch](https://github.com/syntro-opensource/workflows/tree/4).


## Usage - Frontend Checks

This repository also provides a testsuite for client-side code. The suite checks:

* ESlint
* Stylelint
* Jest

You can also configure which Node.js version the tests run on. The test suite defaults to `18.x`.

Usage is straightforward:

```yml
# ...
jobs:
  silverstripe-client:
    name: 📦 Client Testsuite
    uses: syntro-opensource/workflows/.github/workflows/client.yml@5
    with:
      eslint: true
      eslint_dir: client/src/seo-field/
      eslint_configfile: client/src/seo-field/.eslintrc
      eslint_node-ver: 16.x
      # eslint_ext:
      # eslint_max-warnings:
      stylelint: true
      stylelint_glob: client/src/seo-field/**/*.scss
      stylelint_node-ver: 16.x
      # stylelint_max-warnings:
      jest: true
      jest_node-ver: 16.x
```
Each check can be configured using inputs.

### Working with Private Repositories
You can enable an SSH-Client to clone private repositories described in `composer.json`. 
**Please make sure you understand the risks of adding private keys to GitHub workflow Runs!**
This feature can be enabled as follows:
```yml
# ...
jobs:
  silverstripe:
    name: 📦 Client Testsuite
    uses: syntro-opensource/workflows/.github/workflows/client.yml@5
    with:
        # ...
        uses_private_repos: true
        uses_private_keys: |
            ${{ secrets.YOURPRIVATEKEY }}
```
We use [webfactory/ssh-agent](https://github.com/marketplace/actions/webfactory-ssh-agent) to
enable this feature. You can find more information there.

> For Silverstripe 4 related Checks, use the [`4` branch](https://github.com/syntro-opensource/workflows/tree/4).
