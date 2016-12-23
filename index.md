## Canarium Platform

Canarium is a platform to create web applications with ease. The platform is based on Zend Framework 2 and uses other great open source modules and libraries at its core.

Before working on a Canarium Project, it is best that you have a good idea about the following:

- Zend Framework 2
- Composer Dependency Manager
- GIT Commands
- PSR-0 Autoloading Standard
- Doctrine 2 ORM

The rest of the document will discuss only the process specific to Canarium. It is best to familiarize yourself with the above concepts and third party applications before creating your own canarium application.

### Definition of Terms

#### Appmaster

#### Appinstance

#### Modules

#### Libraries


### Creating a site

Instantiate the Appmaster skeleton

`composer create-project unarealidad/canarium-appmaster-skeleton <destination_dir>`

Enter the `<destination_dir>` and go to the instances directory

`cd <destination_dir>/instances`

Instantiate the Appinstance skeleton

`composer create-project unarealidad/canarium-appinstance-skeleton <destination_dir>`

`<destination_dir>` should be in camel case (e.g. CanariumAppinstanceSkeleton)

Enter the `<destination_dir>`

copy the following files from data/config/autoload to config/autoload and remove the `.dist` extension. Customize the values depending on your local setup and preference. Take note that configurations marked as `*.local.php` are igonored in git.

canariumcore.local.php.dist - Site configuration
doctrine.local.php.dist - database configuration
goaliomailservice.local.php.dist - email configuration (required if you want email sending capability)
googlesso.local.php.dist - google login configuration (required if you want google login capability)
ocra-service-manager.local.php.dist - enable/disable dependency view in Zend Developer Tools (optional)
phpini.local.php.dist - php.ini configuration override (optional)
recaptcha.local.php.dist - integrate recaptcha in contact us module (required if you want recaptcha in your contact form)
zenddevelopertools.local.php.dist - Enables zend developer tools for debugging (optional)

For more information about the configuration values, see the core modules' documentation in their github pages.

https://github.com/unarealidad-tech-studio

Create an empty database and put the name of that database in your doctrine.local.php configuration.

Enter the `<destination_dir>` and initialize database using the doctrine tool

`./doctrine- orm:schema-tool:update --force`

Import data/data_imports/initdb.sql to your database to insert some required data

