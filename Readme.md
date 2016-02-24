# Heroku Buildpack: Python

This is a fork of the official [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/) and other excellent software.

This buildpack differs from the standard Heroku buildpack in that it supports deploying the latest version of Python built with shared libraries; this is required to build OpenCV on top of it to support our [OpenCV](http://github.com/computationaltextiles/buildpack-opencv) buildpack, which installs the OpenCV Python package.


See it in Action
----------------

Deploying a Python application couldn't be easier:

    $ ls
    Procfile  requirements.txt  runtime.txt  web.py

    $ heroku create --buildpack git://github.com/heroku/heroku-buildpack-python.git

    $ git push heroku master
    ...
    -----> Python app detected
    -----> Installing python-2.7.11
         $ pip install -r requirements.txt
           Collecting requests (from -r requirements.txt (line 1))
             Downloading requests-2.9.1-py2.py3-none-any.whl (501kB)
           Installing collected packages: requests
           Successfully installed requests-2.9.1
           
    -----> Discovering process types
           Procfile declares types -> (none)

A `requirements.txt` file must be present at the root of your application's repository.

A `runtime.txt` file is required to select the appropriate runtime (see below); the default is not available in this fork.

You can also specify the latest production relase of this buildpack for upcoming builds of an existing application:

    $ heroku buildpacks:set heroku/python



Specify a Python Runtime
------------------------

Specific versions of the Python runtime can be specified with a `runtime.txt` file:

    $ cat runtime.txt
    python-3.5.1

Runtime options include:

- `python-2.7.11`
- `python-2.7.11-shared` (same, but built as a shared library)

Other [unsupported runtimes](https://github.com/heroku/heroku-buildpack-python/tree/master/builds/runtimes) are available as well. Use at your own risk. 
