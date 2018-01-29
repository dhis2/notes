# DHIS2 Advanced setup
In most cases, the basic setup guide for DHIS2 is all you need. But some cases requires you to have different versions and databases, and in this guide we will point out how you can do just that.

## DHIS2 versions
There are two different ways to get a specific version of DHIS2 (omitting tools like docker):
1. [Github](https://github.com/dhis2/dhis2-core)
2. [Dhis2.org](https://www.dhis2.org/downloads)

The most versatile option is Github, which allows you not only to clone and easily switch between versions and even commits, but it allows you to access the newest changes as soon as they are available. On Github, we create a new branch for each new release and currently have all versions from 2.21 available. When using Github for fetching and switching between versions, you need to recompile the code each time.

The war files available on dhis2.org is for versions 2.23 and newer, and changes made on Github will not be reflected in these war files until they have been tested and built by [Jenkins](https://ci.dhis2.org/). Switching between versions using war files and tomcat can be tedious, but some tips and tricks on how to maintain multiple instances of DHIS2 running at the same time with tomcat will come in the Tomcat section.

## Databases in general
Testing different versions, different amount of data or debugging problems for users are some of the use-cases for maintaining multiple databases. Here are some key tips for you too keep in mind:
1. Naming conventions on databases to easily identify which one you want
2. When working with a specific version of DHIS2, remember to use the demo-database of the same version
3. Running a newer version of DHIS2 on an older versions database will upgrade the database. In some cases, that will make it unusable on the older version. (To fix this, re-import the database)
4. Changing the database connection information in dhis.conf only requires you to restart the application to take effect.

## Jetty
The fastest way to get a DHIS2 instance up and running, is using the built-in jetty server. Assuming you have compiled the dhis2 and dhis-web folders of the project as covered in the basic setup guide, you can follow up with these commands to start jetty:

    $ cd dhis-web-portal/

    & mvn jetty:run-war

With jetty, you can only run a single instance at the time. To switch between versions, you need to checkout the correct branch on Github, compile the project and start jetty again. To switch between databases, you need to update your dhis.conf and just restart jetty.

## Tomcat (WIP!)
Tomcat takes some time to set up properly, but also has the possibility to run multiple different versions of DHIS2 in parallel with their own databases. Since setting up tomcat is covered in the basic setup guide, I will point out the steps to setting up multiple instances with multiple databases here.

The following steps is required for each instance you want to run:
1. Aquire a war file of the DHIS2 version you want to run
2. Create a new folder on your system, which will be the DHIS2_HOME folder of the new instance. (This folder cannot be shared by instances you want to have a different configuration)
3. Create a new dhis.conf in the folder you just created, and put in the configuration you want to use for this instance (For example a new database)
4. Create a new namespace in tomcat to run the new instance and add the war file
5. Update the setenv.sh file for the new directory, and set JAVA_HOME and DHIS2_HOME here. Remember to set DHIS2_HOME to point to the new directory you created in step 2.
6. Start/restart the new instance.

Repeat this process until you have all the instances you want running.




    
