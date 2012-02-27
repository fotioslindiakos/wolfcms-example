WolfCMS on OpenShift Express
============================

This git repository helps you get up and running quickly w/ a WolfCMS installation
on OpenShift Express.  The backend database is MySQL and the database name is the 
same as your application name (using $_ENV['OPENSHIFT_APP_NAME']).  You can call
your application by whatever name you want (the name of the database will always
match the application).


Running on OpenShift
----------------------------

Create an account at http://openshift.redhat.com/

Create a php-5.3 application (you can call your application whatever you want)

    rhc app create -a wolfcms -t php-5.3

Add MySQL support to your application

    rhc app cartridge add -a wolfcms -c mysql-5.1

Add this upstream wolfcms repo

    cd wolfcms
    git remote add upstream -m master git://github.com/openshift/wolfcms-example.git
    git pull -s recursive -X theirs upstream master
    # note that the git pull above can be used later to pull updates to WolfCMSs
    
Then push the repo upstream

    git push

That's it, you can now checkout your application at (default admin account is admin/admin):

    http://wolfcms-$yournamespace.rhcloud.com
    http://wolfcms-$yournamespace.rhcloud.com/admin for WolfCMS Administration



NOTES:

GIT_ROOT/.openshift/action_hooks/deploy:
    This script is executed with every 'git push'.  Feel free to modify this script
    to learn how to use it to your advantage.  By default, this script will create
    the database tables that this example uses.

    If you need to modify the schema, you could create a file 
    GIT_ROOT/.openshift/action_hooks/alter.sql and then use
    GIT_ROOT/.openshift/action_hooks/deploy to execute that script (make sure to
    back up your application + database w/ 'rhc app snapshot save' first :) )

