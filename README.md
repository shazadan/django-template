# django-template

A base django application template that can be used with the following:
1. Heroku

Pre-requisites
--------------
*	Download and Install
    1. Python
    2. Oracle Virtual Box VM
    3. Vagrant
    4. Fabric
    5. Boto

*	Clone the git repository in a project directory of your choice
    git clone https://github.com/shazadan/django-template.git

Setup Environment
-----------------
1. Go to the repo directory
2. Run command to setup virtual box
    $ vagrant up
3. Run command to bootstrap environment
    $ fab vagrant bootstrap

Configure PostgreSQL
--------------------

    $ vagrant ssh
    
Let's start off our configuration by working with PostgreSQL. With PostgreSQL we need to create a database, create a user, and grant the user we created access to the database we created. Start off by running the following command:

    [vagrant] $ sudo su - postgres

Your terminal prompt should now say "postgres@yourserver". If this is the case, then run this command to create your database:

    [vagrant/postgres@yourserver] $ createdb [dbname]

Your database has now been created and is named "mydb" if you didn't change the command. You can name your database whatever you would like. Now create your database user with the following command:

    [vagrant/postgres@yourserver] $ createuser -P

You will now be met with a series of 6 prompts. The first one will ask you for the name of the new user. Use whatever name you would like. The next two prompts are for your password and confirmation of password for the new user. For the last 3 prompts just enter "n" and hit "enter". This just ensures your new users only has access to what you give it access to and nothing else. Now activate the PostgreSQL command line interface like so:

    [vagrant/postgres@yourserver] $ psql

Finally, grant this new user access to your new database with this command:

    GRANT ALL PRIVILEGES ON DATABASE [dbname] TO [dbuser];

To ensure that a test database can be created when running tests alter the
[dbuser] role.

    ALTER USER [dbuser] CREATEDB;


You now have a PostgreSQL database and a user to access that database with.

    \q

Set Environment Variables
-------------------------

1. Set the following environment variables - for system-wide put this in
/etc/environment
    * export SECRET_KEY='value'
    * export EMAIL_HOST='value'
    * export EMAIL_HOST_USER='value'
    * export EMAIL_HOST_PASSWORD='value'
    * export DEFAULT_FROM_EMAIL='value'
    * export DB_NAME='value'
    * export DB_USER='value'
    * export DB_PASSWORD='value'
    * export DB_HOST='value'
    * export DB_PORT='value'

2. Implement changes in the environment
        
   [vagrant] $ source /etc/environment
    
    exit

Run Migrations
--------------
1. Run command to push DB migrations
   
   $ fab vagrant migrate

Check Django Application
------------------------
1. Run command
    $ fab vagrant runserver
    
2. Open a browswer and goto address localhost:8000 or 127.0.0.1:8000
