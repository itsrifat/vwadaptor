vwadaptor
=========


The vwadaptor repository contains the server code for our modeling API. The
current deployment can be accessed from
[https://modelserver.virtualwatershed.org/api/](https://modelserver.virtualwatershed.org/api/).


Get started using Docker
------------------------

The best way to get started using the modeling server and other Virtual
Watershed tools is to follow the
[deployment instructions and usage examples on
vw-deploy](https://github.com/mtpain/vw-deploy/tree/4b4f8aacc650b1f2f3f268dc860282e0c4713ed5/v1.0/development).
That requires some knowledge of Docker, which can be gained by following
instructions and tutorials at [docker.com](https://www.docker.com).


Dev Quickstart
--------------

First, set your app's secret key as an environment variable. For example,
add the following to `.bashrc` or `.bash_profile`.

```bash
export VWADAPTOR_SECRET='something-really-secret'
```


Then run the following commands to bootstrap your environment.

```
git clone https://github.com/itsrifat/vwadaptor
cd vwadaptor
pip install -r requirements/dev.txt
python manage.py server
```

You will see a pretty welcome screen.

Once you have installed your DBMS (sqlite3 will do for development),
run the following to create your app's
database tables and perform the initial "migration," which creates the databases
with the appropriate columns to match the models found in the corresponding
subdirectories of `vwadaptor`, e.g. `vwadaptor/modelrun/models.py`,
`vwadaptor/modelresource`, etc.:

```
python manage.py db init
python manage.py db migrate
python manage.py db upgrade
python manage.py server
```



Deployment
----------

In your production environment, make sure the `VWADAPTOR_ENV`
environment variable is set to `"prod"`.


Shell
-----

To open the interactive shell, run

```
python manage.py shell
```

By default, you will have access to `app`, `db`, and the `User` model.


Running Tests
-------------

To run all tests, run

```
python manage.py test
```


Migrations
----------

Whenever a database migration needs to be made. Run the following commands:

```
python manage.py db migrate
```

This will generate a new migration script. Then run:

```
python manage.py db upgrade
```

To apply the migration.

For a full migration command reference, run `python manage.py db --help`.
