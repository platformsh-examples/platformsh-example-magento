# Magento 2.2 (Enterprise Edition)

This is a no-thrills example of a minimal repository to deploy a Magento 2 Enterprise Edition instance on Platform.sh.

This example is based on using the Composer to load up dependencies and get the Magento vendor folders.

## Project Variables

This project relies on the following project variables being set prior to initial deploy.

- ADMIN_USERNAME (defaults to “admin”)
- ADMIN_FIRSTNAME (defaults to “John”)
- ADMIN_LASTNAME (defaults to “Doe”)
- ADMIN_EMAIL (defaults to “john@example.com”)
- ADMIN_PASSWORD (defaults to “admin12”)
- ADMIN_URL (defaults to “admin”)
- APPLICATION_MODE (defaults to “production”)_

The latter can be changed at any time adjust the Application Mode on the next deploy.

## Repository structure

Here are the specific files for this example to work on Platform.sh:

```
.platform/
         /routes.yaml
         /services.yaml
.platform.app.yaml
auth.json
composer.json
magento-vars.php
php.ini
```

in `.platform.app.yaml` we have the basic configuration of our application (we call it `mymagento`), saying this is a
Composer based application, that we depend on a database called `database` and that we what to run a build script and a
deploy script during deployment.. and also set up some crons.

In `.platform/routes.yaml` we just say that we will redirect www to the naked domain, and that the application that
will be serving HTTP will be the one we called `php`.

In `.platform/services.yaml` we say we want a MySQL instance, a Redis and a Solr. That would cover most basic Magento
needs, right?

The `composer.json` will fetch Magento, and some configuration scripts to prepare your application
for Platform.sh.

## Providing your MagentoCommerce credentials
Make sure you add your Magento credentials to the `auth.json` file and that those credentials can get you access to Magento Enterprise Edition. You can get those credentials in your [MagentoCommerce account][1].

```
"http-basic": {
      "repo.magento.com": {
         "username": "<public-key>",
         "password": "<private-key>"
      }
   }
```

[1]:	https://www.magentocommerce.com/magento-connect/customerdata/accessKeys/list/