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

#### Canarium Kernal
This contains the base of canarium which is composed of libraries and modules to allow the platform to work.

#### Modules
The blocks that extends the functionality of the Canarium Kernal. This includes complete routes, templates, permissions, and configuration (e.g. Pages, Contant Us)

#### Libraries
Libraries helps modules to do their work. The code does not have template files and only exposes routes, services and models for canarium modules to use. (e.g. ErrorHandler, GoogleSSO)

#### Plugins
Plugins are like libraries but does not rely on Canarium Kernal. (e.g. Country List, Postcode lookup etc.)

#### AppMaster
- The AppMaster level should include all the core operating procedures from Canarium Kernal, and customise it on this level.
- All 3rd party libraries should be included from Canarium Kernal too.
- Libraries
 - The libraries found here are more specific to this particular application. Most likely it is custom built libraries with a specific business function. This means it’s not shared with all applications, but it is required for all Instances of this Application.
- Modules
  - The Modules found here include the basic operational procedures from Canarium Kernal to get an Application running. But it will have a wider selection of modules that are purposely built for this Application (e.g. Custom Calculator, Image Gallery)
- Plugins
 - If there is a reason to put a plugin on the App level it is because it’s not general enough for other Apps to share its use.

#### AppInstance
- If there is an override on the AppInstance level it is because the owner of this instance wants something that works slightly differently. An example may be a different tax structure for pricing of products. Or it could be a different region that requires different shipping methods. In many cases, new instancecs would just need to vary in configurations and not need to worry about the code.
- Libraries
 - There should be no libraries stored at this level, but we will make a provision for there to be if the case arises.
- Modules
 - Most likely there are no overrides on the AppInstance level, but if there needs to be we have made provisions for this. 
- Plugins
 - Primarily inherited from the Kernal or AppMaster. If there is a reason to put a plugin on the AppInstance level it is because it’s not general enough for other AppInstances to share its use.

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

- **canariumcore.local.php.dist** - Site configuration
- **doctrine.local.php.dist** - database configuration
- **goaliomailservice.local.php.dist** - email configuration (required if you want email sending capability)
- **googlesso.local.php.dist** - google login configuration (required if you want google login capability)
- **ocra-service-manager.local.php.dist** - enable/disable dependency view in Zend Developer Tools (optional)
- **phpini.local.php.dist** - php.ini configuration override (optional)
- **recaptcha.local.php.dist** - integrate recaptcha in contact us module (required if you want recaptcha in your contact form)
- **zenddevelopertools.local.php.dist** - Enables zend developer tools for debugging (optional)

For more information about the configuration values, see the core modules' documentation in their github pages.

https://github.com/unarealidad-tech-studio

Create an empty database and put the name of that database in your doctrine.local.php configuration.

Enter the `<destination_dir>` and initialize database using the doctrine tool

`./doctrine- orm:schema-tool:update --force`

Import data/data_imports/initdb.sql to your database to insert some required data

Create a symlink of `<appmaster_dir>/vendor/unarealidad/canarium-kernal-core/public/assets` in `<appinstance_dir>/public/assets`. This will link the resources needed to render the administrator web interface.

`ln -s <appmaster_dir>/vendor/unarealidad/canarium-kernal-core/public/assets <appinstance_dir>/public/assets`

Give the following directories write permission:

`<appmaster_dir>/data`
`<appinstance_dir>/data`


Setup your domain's doc root to your `<destination_dir>/public/` directory and the site should now be running.

To access the administration page, visit the /admin route and login with the following default admin user

`username: root`
`email: root@root.com`
`password: 123456`

Be sure to change your admin password afterwards.

### Directory Structure

#### Appmaster Structure

Directory/File | Description
------------- | -------------
config | (dir) AppMaster specific configuration. Configuration that are applicable to the instances under the appmaster will be placed here. For example, if we cloned a Form AppMaster here, then all configuration files that are needed for all Form instances to work should be configured here.
application.config.php | AppMaster Main configuration file.
autoload | (dir) AppMaster Module specific configuration
data | (dir) Cache data are generated here. Other miscellaneous files can also be placed here like dist files for local configurations
vendor | (dir) Dependencies that are applicable to all sites that are under the AppMaster are placed here. This directory will be automatically be created by composer when we run composer install.
composer.json | The composer definition file. We will list the dependencies that we want composer to download here. The files will be downloaded to the vendor directory.
composer.phar | Composer executable
compose.lock | Composer lock file
init_autoloader.php | Composer autoload file
instances | (dir) This contains the AppInstance clones. See AppInstance Structure for more details.

#### Appinstance Structure

Directory/File | Description
-------------- | --------------
bin | (dir) Contains executables/binaries. The doctrine executable are placed here.
config | (dir) AppInstance specific configuration. Configuration will be placed here. 
instance.config.php | AppInstance Main configuration file that supplements the application.config.php
module.config.php | AppInstance module configuration file.
autoload | (dir) AppMaster Module specific configuration
data | (dir) Cache data are generated here. Other miscellaneous files can also be placed here.
config | (dir) Configuration templates are placed here. This is meant to be a guideline for local configurations that will be placed in config/autoload.
composer.json | The composer definition file. This contains information about this AppInstance.
doctrine-module | Doctrine main executable for linux based machines
doctrine-module.bat | Doctrine main executable for windows based machines
Module.php | Main module class
public | (dir) Contains front end resources as well as site templates. This directory should be the only one that is accessible to integrators.
assets | (symlink) This is linked to the CanariumCore’s public/assets directory.
css | (dir) AppInstance css files
images | (dir) AppInstance images files
js | (dir) AppInstance js files
templates | (dir) Module template overrides.
