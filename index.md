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

1. Instantiate the Appmaster skeleton

composer create-project unarealidad/canarium-appmaster-skeleton <destination_dir>

2. Enter the <destination_dir> and go to the instances directory

`cd <destination_dir>/instances`

3. Instantiate the Appinstance skeleton

composer create-project unarealidad/canarium-appinstance-skeleton <destination_dir>

<destination_dir> should be in camel case (e.g. CanariumAppinstanceSkeleton)

4. Enter the <destination_dir> and initialize database using the doctrine tool

./doctrine- orm:schema-tool:update --force

5. Import data/initdb.sql to your database to insert some required data

