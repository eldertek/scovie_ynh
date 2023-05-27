# Scovie: Digital Signage for High Schools

[![Integration level](https://dash.yunohost.org/integration/scovie_ynh.svg)](https://dash.yunohost.org/appci/app/scovie_ynh) ![Working status](https://ci-apps.yunohost.org/ci/badges/scovie_ynh.status.svg) ![Maintenance status](https://ci-apps.yunohost.org/ci/badges/scovie_ynh.maintain.svg)  
[![Install Django Example with YunoHost](https://install-app.yunohost.org/install-with-yunohost.svg)](https://install-app.yunohost.org/?app=scovie_ynh)

> *This package allows you to install Scovie quickly and simply on a YunoHost server.
If you don't have YunoHost, please consult [the guide](https://yunohost.org/#/install) to learn how to install it.*

## Overview

[![pytest](https://github.com/eldertek/scovie_ynh/actions/workflows/pytest.yml/badge.svg)](https://github.com/eldertek/scovie_ynh/actions/workflows/pytest.yml) [![YunoHost apps package linter](https://github.com/eldertek/scovie_ynh/actions/workflows/package_linter.yml/badge.svg)](https://github.com/eldertek/scovie_ynh/actions/workflows/package_linter.yml)

[Scovie](https://github.com/eldertek/scovie) is an open-source digital signage system for high schools, built using Python and Django. It provides an easy-to-use interface for administrators to upload and manage multimedia content, which is then displayed on screens throughout the school.

You can try the [demo](https://scovie.eclipse-technology.eu) here.

Pull requests welcome ;)


**Shipped version:** 0.0.5
## Disclaimers / important information

## local test

For quicker developing of scovie_ynh in the context of YunoHost app,
it's possible to run the Django development server with the settings
and urls made for YunoHost installation.

e.g.:
```bash
~$ git clone https://github.com/eldertek/scovie_ynh.git
~$ cd scovie_ynh/
~/scovie_ynh$ make
install-poetry         install or update poetry
install                install project via poetry
update                 update the sources and installation and generate "conf/requirements.txt"
lint                   Run code formatters and linter
fix-code-style         Fix code formatting
tox-listenvs           List all tox test environments
tox                    Run pytest via tox with all environments
pytest                 Run pytest
publish                Release new version to PyPi
local-test             Run local_test.py to run the project locally
local-diff-settings    Run "manage.py diffsettings" with local test

~/scovie_ynh$ make install-poetry
~/scovie_ynh$ make install
~/scovie_ynh$ make local-test
```

Notes:

* SQlite database will be used
* A super user with username `test` and password `test` is created
* The page is available under `http://127.0.0.1:8000/`


## history

* [v0.0.5 - 27.05.2023](https://github.com/eldertek/scovie_ynh/compare/4b0275e7f75d199dca8a1e97c26dc8568c31cb52...4f0086c7da6123f3f8b05c4001f9109891e6bd9f)
  * first working state
* [26.05.2023](https://github.com/eldertek/scovie_ynh/commit/4b0275e7f75d199dca8a1e97c26dc8568c31cb52)
  * init the project


## Links

* Report a bug about this package: https://github.com/eldertek/scovie_ynh/issues
* YunoHost website: https://yunohost.org/
* PyPi package: https://pypi.org/project/scovie/

These projects used `scovie_ynh`:

* https://github.com/eldertek/scovie_ynh

---

# Developer info

The App project will be stored under `__FINALPATH__` (e.g.: `/opt/yunohost/$app`) that's Django's `settings.FINALPATH`
"static" / "media" files to serve via nginx are under `__PUBLIC_PATH__` (e.g.: `/var/www/$app`) that's `settings.PUBLIC_PATH`

## package installation / debugging

This app is not in YunoHost app catalog. Test install, e.g.:
```bash
~# git clone https://github.com/eldertek/scovie_ynh.git
~# yunohost app install scovie_ynh/ -f
```
To update:
```bash
~# cd scovie_ynh
~/scovie_ynh# git fetch && git reset --hard origin/testing
~/scovie_ynh# yunohost app upgrade scovie_ynh -u . -F
```

To remove call e.g.:
```bash
sudo yunohost app remove scovie_ynh
```

Backup / remove / restore cycle, e.g.:
```bash
yunohost backup create --apps scovie_ynh
yunohost backup list
archives:
  - scovie_ynh-pre-upgrade1
  - 20201223-163434
yunohost app remove scovie_ynh
yunohost backup restore 20201223-163434 --apps scovie_ynh
```

Debug the installation, e.g.:
```bash
root@yunohost:~# cat /etc/yunohost/apps/scovie_ynh/settings.yml
...

root@yunohost:~# ls -la /var/www/scovie_ynh/
total 18
drwxr-xr-x 4 root root 4 Dec  8 08:36 .
drwxr-xr-x 6 root root 6 Dec  8 08:36 ..
drwxr-xr-x 2 root root 2 Dec  8 08:36 media
drwxr-xr-x 7 root root 8 Dec  8 08:40 static

root@yunohost:~# ls -la /opt/yunohost/scovie_ynh/
total 58
drwxr-xr-x 5 scovie_ynh scovie_ynh   11 Dec  8 08:39 .
drwxr-xr-x 3 root        root           3 Dec  8 08:36 ..
-rw-r--r-- 1 scovie_ynh scovie_ynh  460 Dec  8 08:39 gunicorn.conf.py
-rw-r--r-- 1 scovie_ynh scovie_ynh    0 Dec  8 08:39 local_settings.py
-rwxr-xr-x 1 scovie_ynh scovie_ynh  274 Dec  8 08:39 manage.py
-rw-r--r-- 1 scovie_ynh scovie_ynh  171 Dec  8 08:39 secret.txt
drwxr-xr-x 6 scovie_ynh scovie_ynh    6 Dec  8 08:37 venv
-rw-r--r-- 1 scovie_ynh scovie_ynh  115 Dec  8 08:39 wsgi.py
-rw-r--r-- 1 scovie_ynh scovie_ynh 4737 Dec  8 08:39 scovie_ynh_demo_settings.py

root@yunohost:~# cd /opt/yunohost/scovie_ynh/
root@yunohost:/opt/yunohost/scovie_ynh# source venv/bin/activate
(venv) root@yunohost:/opt/yunohost/scovie_ynh# ./manage.py check
scovie_ynh v0.8.2 (Django v2.2.17)
DJANGO_SETTINGS_MODULE='scovie_ynh_demo_settings'
PROJECT_PATH:/opt/yunohost/scovie_ynh/venv/lib/python3.7/site-packages
BASE_PATH:/opt/yunohost/scovie_ynh
System check identified no issues (0 silenced).

root@yunohost:~# tail -f /var/log/scovie_ynh/scovie_ynh.log
root@yunohost:~# cat /etc/systemd/system/systemd.service
...

root@yunohost:~# systemctl reload-or-restart scovie_ynh
root@yunohost:~# journalctl --unit=scovie_ynh --follow
```



## Documentation and resources

* Official demo website: <https://scovie.eclipse-technology.eu>
* Official user documentation: <https://github.com/eldertek/scovie>
* Official admin documentation: <https://github.com/eldertek/scovie>
* Upstream app code repository: <https://github.com/eldertek/scovie>
* YunoHost documentation for this app: <https://yunohost.org/scovie>
* Report a bug: <https://github.com/eldertek/scovie_ynh/issues>

## Developer info

Please send your pull request to the [testing branch](https://github.com/eldertek/scovie_ynh/tree/testing).

To try the testing branch, please proceed like that.

``` bash
sudo yunohost app install https://github.com/eldertek/scovie_ynh/tree/testing --debug
or
sudo yunohost app upgrade scovie_ynh -u https://github.com/eldertek/scovie_ynh/tree/testing --debug
```

**More info regarding app packaging:** <https://yunohost.org/packaging_apps>
