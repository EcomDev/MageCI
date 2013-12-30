Magento Continuous Integration Tools
===================================

A set of tools to help set up 
a proper environment for testing magento

Installation
------------

Installation is very easy though composer.json

In your application or dependent library root directory, create a _composer.json_ file. 
In case you are not familiar with [Composer](http://getcomposer.org/), see [composer.json Schema](http://getcomposer.org/doc/04-schema.md).

In the _require_ or alternatively in the _require-dev_ section, add the following dependency:

    "ecomdev/mage-ci": "dev-master"

Usage
-----

### Running a batch of PHPUnit tests
    $ mage-ci phpunit <directory> <OPTIONS> 
        Runs unit tests for all phpunit.xml or phpunit.dist.xml files in <directory> or its subdirectories. 
        <OPTIONS> will be passed directly to phpunit binary.


### Installing a particular Magento version
    $ bin/mage-ci install <magento_directory> <version> <db_name> <OPTIONS>
        Installs a Magento version to a specified destination
          -c                  Create databases flag
          -t                  Create test database flag (only in combination with -c option)
          -u  <db_user>       DB Username
          -p  <db_pass>       DB Password
          -r  <sql_base_url>  SQL dumps repository url for a particular Magento version (<sql_base_url>/<version>.sql.gz)
          -f  <sql_dump_file> SQL dump file, if you'd like to preinstall some data and specfied -c option

### Installing a Magento module
    $ bin/mage-ci install-module <magento_directory> <module_dir_or_vcs_url>
        Installs a Magento module with modman definition 

### Updating installed Magento modules
    $ bin/mage-ci update-modules <magento_directory>
        Updates all installed modman modules at specified Magento instnace 

### Uninstalling Magento version
    $ bin/mage-ci uninstall <magento_directory> [<db_name>] <OPTIONS>
        Performs uninstall of Magento instance
          -u  <db_user>       DB Username
          -p  <db_pass>       DB Password

### Uninstalling Magento module
    $ bin/mage-ci uninstall-module <magento_directory> <module_dir_or_vcs_url>
        Performs uninstall of Magento module from instance

### Mass Install of Magento versions  
    $ bin/mage-ci install-multiple <directory> <prefix> <version1> ... <versionN> <OPTIONS>
        Installs multiple version of magento at <directory> in subdirectories which name is a combined value of <prefix>-<version> 
           -d  <download_dir>  Directory where all downloads are stored
           -u  <db_user>       DB Username
           -p  <db_pass>       DB Password
           -t                  Create test db as well
           -r  <sql_base_url>  SQL dumps repository url for a particular Magento version (<sql_base_url>/<version>.sql.gz)

### Dump databases of existing installed versions
    $ bin/mage-ci db-dump <directory> <prefix> <version1> ... <versionN> <OPTIONS>
        Creates Magento database dump file at <directory> directory with name <file_prefix><version>.sql.gz, the dumped database is <prefix>_<version>
           -u  <db_user>       DB Username
           -p  <db_pass>       DB Password
           -s  <file_prefix>   sql file prefix


Magento Clean DB Dumps
----------------------

It is possible to specify base url for downloading of database dump for a particular Magento version.
Most of the time clean installation of Magento takes a lot of time, so it is nice to have this clean db dump prepared for each Magento version. 

We created such repository at the following url:
http://mage-ci.ecomdev.org 

You just need to specify it during installation of process:

    $ bin/mage-ci install magento-1.7.0.2 1.7.0.2 mage_1.7.0.2 -r http://mage-ci.ecomdev.org 
        
This command will download db dump from the following URL: http://mage-ci.ecomdev.org/1.7.0.2.sql.gz

