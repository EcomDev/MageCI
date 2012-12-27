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

    "ecomdev/mage-ci: "dev-master"

Usage
-----

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
        Creates Magento database dump file at <directory> directory with name <file_prefix><version>.sql.gz, the data dunped database is <prefix>_<version>
           -u  <db_user>       DB Username
           -p  <db_pass>       DB Password
           -s  <file_prefix>   sql file prefix
