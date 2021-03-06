# github-copier

A command line utility to clone all user repositories from Github or Bitbucket. If the repositories are already cloned,
the utility receives the changes in all branches and tries to merge the changes in the current branch with
the local repository.

How to install
--------------

* `$ cd ~` 
* `$ mkdir ghcopy` 
* `$ cd ghcopy`
* `$ virtualenv --python=python3 .`
* `$ source bin/activate`
* `$ pip install git+git://github.com/oleglpts/github-copier.git` (recommended) or
* `$ pip install ghcopy`

You can not use a virtual environment if you do not need it. When installing without git (last line),
you will have to clone the repository, create directory ~/.ghcopy and copy the configuration files and locales:

* `$ git clone https://github.com/oleglpts/github-copier.git`
* `$ cd github-copier/ghcopy/data`
* `$ mkdir ~/.ghcopy`
* `$ cp config.json ~/.ghcopy`
* `$ cp -r locale ~/.ghcopy`
* `$ cd ../../..`
* `$ rm -rf github-copier`

See ~/.ghcopy/config.json:

    {
        "environment": "",
        "user": "",
        "password": "",
        "token": "",
        "type": "github",
        or
        "type": "bitbucket",
        "locale_domain": "ghcopy",
        "language": "en",
        "locale_dir": "~/.ghcopy/locale",
        "log_file": "~/.ghcopy/ghcopy.log",
        "log_format": "%(levelname)-10s|%(asctime)s| %(name)s --- %(message)s (%(filename)s:%(lineno)d)"
    }

You can change parameter values and specify a username and password or token if you do not want to specify them on
the command line, but then the password and token will be stored in clear text. On July 1st, 2020, basic authentication
using password to Github will no longer work, use a personal access token (PAT) with the appropriate scope to
access repositories (parameter -t --token or token in config file). 
Visit https://github.com/settings/tokens for more information.

Command Line Tool
-----------------

    ghcopy [-h] [-c CONFIG] [-o OUTPUT] [-u USER] [-p PASSWORD] [-t token]
              [-l LOG_LEVEL]

    optional arguments:
      -h, --help show this help message and exit
      -c CONFIG, --config CONFIG config file (default: ~/.ghcopy/config.json)
      -o OUTPUT, --output OUTPUT output directory (default: ~/RemoteCopies)
      -u USER, --user USER user name (default: parameter user from config file)
      -p PASSWORD, --password PASSWORD password (default: parameter password from config file)
      -t TOKEN, --token TOKEN personal access token (PAT) (default: parameter token from config file)
      -b HUB, --hub HUB repository type: github, bitbucket (default: parameter type from config file)
      -l LOG_LEVEL, --log_level LOG_LEVEL logging level: CRITICAL, ERROR, WARNING, INFO, DEBUG or NOTSET (default: INFO)

Requirements
------------

* GitPython>=3.0.8
* PyGithub>=1.46
* bitbucket-python>=0.2.2
