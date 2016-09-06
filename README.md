# django-microservices

## About
Simple django package to easily "connect" microservices.

The package loads the service configurations (id, name, host) into a DB table from a json file which can be stored on a shared drive, or hosted on URL.

## Installation
You can simply install the package with pip from **PyPI** or **GitHub**.

**Install with pip from github**

`pip install git+https://github.com/gabor-boros/django-microservices.git`

**Install from pypi**

`TO DO`

## Configuration
Add the `microservices` app to your `INSTALLED_APPS` like this:

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'microservices',
    ...
]
```

After you added it to the `INSTALLED_APPS`, you **must** configure the path where your service configuration exists.
The configuration file is a `json` file. Basically it is an output of `python manage.py dumpdata` command.
It doesn't matter where is your file located. It can be hosted on a website, or located on a *shared* drive.

```
SERVICE_CONFIGURATION_FILE = 'http://myserver.com/services.json'
```

or

```
SERVICE_CONFIGURATION_FILE = 'services.json'
```

**Service configuration example**
*sample.json*
```
[
    {
        "model": "microservices.service",
        "pk": 1,
        "fields": {
            "name": "auth",
            "host": "http://auth.example.com/",
        }
    },
    {
        "model": "microservices.service",
        "pk": 2,
        "fields": {
            "name": "search",
            "host": "http://search.example.com/",
        }
    }
]
```

## Management commands
Three management command ships with this package to help to manage your service configuration.

* `list_services` - Lists your services ordered by their status
* `load_services` - Loads the configuration from the given resource location, set in `settings.py`
* `check_services` - Going thorough your configuration and tries to reach them.
    * If the host sends any response (which is not error related), the service will be marked available
    * If the response is an error, or the service can not be reached, the service's status will be unavailable

## Tests
To run the tests for this package use the `python manage.py test` command as usual
In case you would like to generate a **coverage** report as well, run the `run_test_coverage.sh` file.

## Contributors
If you would like to help to develop this package please read the CONTRIBUTING guideline. Every PR is highly welcomed.
