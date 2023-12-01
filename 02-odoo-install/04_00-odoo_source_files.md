# <a name="top"></a> Cap 2.3 - Installiamo i sorgenti di Odoo

Copiamo con git i sorgenti di "Odoo community" e li configuriamo/attiviamo



## Step 7: Get Odoo 16 community from git

We now need to upload the Odoo source file to our server, We can directly clone the Community Edition source code from the Odoo GitHub repository.  Once the installation is complete, you can add the Enterprise edition add-ons.

Verifichiamo di avere git

```bash
$ git --version
```

Se non fosse installato lo installiamo.

```bash
$ sudo apt install git
```

### Cambiamo utente e mettiamo l'utente "odoo16" (Switch User)

To make the Odoo system more secure, we must now change the system user to **odoo16** (which is created in Step 1c), prior to cloning. E poi con "gic clone' ci copiamo tutti i sorgenti dal repository di odoo.
Finito usciamo e torniamo al nostro utente iniziale.

```bash
$ sudo su - odoo16 -s /bin/bash
-> whoami
-> pwd
-> ls
-> git clone https://www.github.com/odoo/odoo --depth 1 --branch 16.0 --single-branch .
-> ls
-> exit
$ whoami
$ pwd
```

> ATTENZIONE: lo spazio ed il punto ` .` alla fine del comando dobbiamo metterlo.
> The dot (.) operator is used at the end of the command to copy the files to the current user's home directory, which is /opt/odoo and is the same home directory that was specified when the user was created.

> Nota: nello Step 1c abbiamo indicato che l'utente ha il suo path "home" come "/opt/odoo16" ed infatti una volta fatto il cambio utente possiamo vedere con `whoami` che siamo diventati `odoo16` e con `pwd` vediamo che la "Present Working Directory" si è spostata su `/opt/odoo16`.


Esempio:

```bash
tt-fb@odooserver:~$ git --version
git version 2.34.1
tt-fb@odooserver:~$ sudo apt install git
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
git is already the newest version (1:2.34.1-1ubuntu1.10).
git set to manually installed.
The following package was automatically installed and is no longer required:
  libnuma1
Use 'sudo apt autoremove' to remove it.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
tt-fb@odooserver:~$ git --version
git version 2.34.1
tt-fb@odooserver:~$ sudo su - odoo16 -s /bin/bash
odoo16@odooserver:~$ whoami
odoo16
odoo16@odooserver:~$ pwd
/opt/odoo16
odoo16@odooserver:~$ git clone https://www.github.com/odoo/odoo --depth 1 --branch 16.0 --single-branch .
Cloning into '.'...
warning: redirecting to https://github.com/odoo/odoo.git/
remote: Enumerating objects: 41427, done.
remote: Counting objects: 100% (41427/41427), done.
remote: Compressing objects: 100% (29283/29283), done.
remote: Total 41427 (delta 11578), reused 36996 (delta 10872), pack-reused 0
Receiving objects: 100% (41427/41427), 158.95 MiB | 11.09 MiB/s, done.
Resolving deltas: 100% (11578/11578), done.
Updating files: 100% (36562/36562), done.
odoo16@odooserver:~$ ls
CONTRIBUTING.md  LICENSE      README.md    addons  doc	 odoo-bin	   setup      setup.py
COPYRIGHT	 MANIFEST.in  SECURITY.md  debian  odoo  requirements.txt  setup.cfg
odoo16@odooserver:~$ pwd
/opt/odoo16
odoo16@odooserver:~$ ls -a
.   .git     .gitignore  CONTRIBUTING.md  LICENSE      README.md    addons  doc   odoo-bin	    setup      setup.py
..  .github  .tx	 COPYRIGHT	  MANIFEST.in  SECURITY.md  debian  odoo  requirements.txt  setup.cfg
odoo16@odooserver:~$ cd odoo/
odoo16@odooserver:~/odoo$ ls
__init__.py  api.py  conf	    fields.py  import_xml.rng  models.py  netsvc.py  release.py  sql_db.py  tools
addons	     cli     exceptions.py  http.py    loglevels.py    modules	  osv	     service	 tests	    upgrade
odoo16@odooserver:~/odoo$ cd ..
odoo16@odooserver:~$ ls
CONTRIBUTING.md  LICENSE      README.md    addons  doc	 odoo-bin	   setup      setup.py
COPYRIGHT	 MANIFEST.in  SECURITY.md  debian  odoo  requirements.txt  setup.cfg
odoo16@odooserver:~$ exit
logout
tt-fb@odooserver:~$ whoami
tt-fb
tt-fb@odooserver:~$ pwd
/home/tt-fb
tt-fb@odooserver:~$ 
```



## Installiamo i paccetti python richiesti da odoo

Questi sono pacchetti diversi rispetto a quelli che abbiamo installato nei precedenti capitoli.
Questi pacchetti li prendiamo dal file `requirements.txt` che ci siamo presi clonando i sorgenti di odoo.

Odoo utilizes a variety of Python packages and libraries for various tasks. We must use pip3 to install them in order to run Odoo. Additionally, the requirement.txt file included in the Odoo folder has a list of the necessary requirements. Consequently, we can pass this file as a parameter to the pip install command, which will cause each package listed in requirement.txt to be installed automatically.

```bash
$ sudo pip3 install -r /opt/odoo16/requirements.txt
```

All the packages must be correctly installed for Odoo to function properly, and you should make sure of that.

Esempio:

```bash
tt-fb@odooserver:~$ sudo pip3 install -r /opt/odoo16/requirements.txt
Ignoring freezegun: markers 'python_version < "3.8"' don't match your environment
Ignoring gevent: markers 'python_version == "3.7"' don't match your environment
Ignoring gevent: markers 'python_version > "3.7" and python_version <= "3.9"' don't match your environment
Ignoring gevent: markers 'python_version > "3.10"' don't match your environment
Ignoring greenlet: markers 'python_version == "3.7"' don't match your environment
Ignoring greenlet: markers 'python_version > "3.7" and python_version <= "3.9"' don't match your environment
Ignoring greenlet: markers 'python_version > "3.10"' don't match your environment
Ignoring Jinja2: markers 'python_version > "3.10"' don't match your environment
Ignoring lxml: markers 'python_version > "3.10"' don't match your environment
Ignoring MarkupSafe: markers 'python_version > "3.10"' don't match your environment
Ignoring ofxparse: markers 'python_version <= "3.9"' don't match your environment
Ignoring Pillow: markers 'python_version > "3.10"' don't match your environment
Ignoring psutil: markers 'python_version > "3.10"' don't match your environment
Ignoring psycopg2: markers 'sys_platform != "win32" and python_version < "3.8"' don't match your environment
Ignoring psycopg2: markers 'sys_platform == "win32" and python_version < "3.10"' don't match your environment
Ignoring psycopg2: markers 'python_version > "3.10" or (sys_platform == "win32" and python_version == "3.10")' don't match your environment
Ignoring PyPDF2: markers 'python_version > "3.10"' don't match your environment
Ignoring pypiwin32: markers 'sys_platform == "win32"' don't match your environment
Ignoring pyusb: markers 'python_version > "3.10"' don't match your environment
Ignoring reportlab: markers 'python_version > "3.10"' don't match your environment
Ignoring Werkzeug: markers 'python_version <= "3.9"' don't match your environment
Ignoring xlrd: markers 'python_version < "3.8"' don't match your environment
Collecting Babel==2.9.1
  Downloading Babel-2.9.1-py2.py3-none-any.whl (8.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.8/8.8 MB 55.9 MB/s eta 0:00:00
Requirement already satisfied: chardet==4.0.0 in /usr/lib/python3/dist-packages (from -r /opt/odoo16/requirements.txt (line 4)) (4.0.0)
Requirement already satisfied: cryptography==3.4.8 in /usr/lib/python3/dist-packages (from -r /opt/odoo16/requirements.txt (line 5)) (3.4.8)
Collecting decorator==4.4.2
  Downloading decorator-4.4.2-py2.py3-none-any.whl (9.2 kB)
Collecting docutils==0.16
  Downloading docutils-0.16-py2.py3-none-any.whl (548 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 548.2/548.2 KB 57.7 MB/s eta 0:00:00
Collecting ebaysdk==2.1.5
  Downloading ebaysdk-2.1.5.tar.gz (42 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 43.0/43.0 KB 10.2 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting freezegun==0.3.15
  Downloading freezegun-0.3.15-py2.py3-none-any.whl (14 kB)
Collecting gevent==21.8.0
  Downloading gevent-21.8.0.tar.gz (6.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 6.2/6.2 MB 101.9 MB/s eta 0:00:00
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... error
  error: subprocess-exited-with-error
  
  × Preparing metadata (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [40 lines of output]
      Traceback (most recent call last):
        File "/usr/lib/python3/dist-packages/pip/_vendor/pep517/in_process/_in_process.py", line 363, in <module>
          main()
        File "/usr/lib/python3/dist-packages/pip/_vendor/pep517/in_process/_in_process.py", line 345, in main
          json_out['return_val'] = hook(**hook_input['kwargs'])
        File "/usr/lib/python3/dist-packages/pip/_vendor/pep517/in_process/_in_process.py", line 164, in prepare_metadata_for_build_wheel
          return hook(metadata_directory, config_settings)
        File "/usr/lib/python3/dist-packages/setuptools/build_meta.py", line 174, in prepare_metadata_for_build_wheel
          self.run_setup()
        File "/usr/lib/python3/dist-packages/setuptools/build_meta.py", line 267, in run_setup
          super(_BuildMetaLegacyBackend,
        File "/usr/lib/python3/dist-packages/setuptools/build_meta.py", line 158, in run_setup
          exec(compile(code, __file__, 'exec'), locals())
        File "setup.py", line 481, in <module>
          run_setup(EXT_MODULES)
        File "setup.py", line 348, in run_setup
          setup(
        File "/usr/lib/python3/dist-packages/setuptools/__init__.py", line 153, in setup
          return distutils.core.setup(**attrs)
        File "/usr/lib/python3/dist-packages/setuptools/_distutils/core.py", line 109, in setup
          _setup_distribution = dist = klass(attrs)
        File "/usr/lib/python3/dist-packages/setuptools/dist.py", line 459, in __init__
          _Distribution.__init__(
        File "/usr/lib/python3/dist-packages/setuptools/_distutils/dist.py", line 293, in __init__
          self.finalize_options()
        File "/usr/lib/python3/dist-packages/setuptools/dist.py", line 837, in finalize_options
          ep(self)
        File "/usr/lib/python3/dist-packages/setuptools/dist.py", line 858, in _finalize_setup_keywords
          ep.load()(self, ep.name, value)
        File "/tmp/pip-build-env-mb2x3el8/overlay/local/lib/python3.10/dist-packages/cffi/setuptools_ext.py", line 216, in cffi_modules
          add_cffi_module(dist, cffi_module)
        File "/tmp/pip-build-env-mb2x3el8/overlay/local/lib/python3.10/dist-packages/cffi/setuptools_ext.py", line 49, in add_cffi_module
          execfile(build_file_name, mod_vars)
        File "/tmp/pip-build-env-mb2x3el8/overlay/local/lib/python3.10/dist-packages/cffi/setuptools_ext.py", line 25, in execfile
          exec(code, glob, glob)
        File "src/gevent/libev/_corecffi_build.py", line 31, in <module>
          ffi = FFI()
        File "/tmp/pip-build-env-mb2x3el8/overlay/local/lib/python3.10/dist-packages/cffi/api.py", line 54, in __init__
          raise Exception("Version mismatch: this is the 'cffi' package version %s, located in %r.  When we import the top-level '_cffi_backend' extension module, we get version %s, located in %r.  The two versions should be equal; check your installation." % (
      Exception: Version mismatch: this is the 'cffi' package version 1.16.0, located in '/tmp/pip-build-env-mb2x3el8/overlay/local/lib/python3.10/dist-packages/cffi/api.py'.  When we import the top-level '_cffi_backend' extension module, we get version 1.15.0, located in '/usr/lib/python3/dist-packages/_cffi_backend.cpython-310-x86_64-linux-gnu.so'.  The two versions should be equal; check your installation.
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
error: metadata-generation-failed

× Encountered error while generating package metadata.
╰─> See above for output.

note: This is an issue with the package mentioned above, not pip.
hint: See above for details.
tt-fb@odooserver:~$ 
```

Qui ci sono i vari problemi da risolvere. 

risolto una parte

```bash
tt-fb@odooserver:~$ sudo pip3 install -r /opt/odoo16/requirements.txt
tt-fb@odooserver:~$ pip install --upgrade pip setuptools wheel
tt-fb@odooserver:~$ sudo apt-get install python-cffi
tt-fb@odooserver:~$ sudo apt install python-cffi
tt-fb@odooserver:~$ sudo pip install cffi==1.5.2

$ pip3 install --upgrade pip
$ pip install --upgrade pip setuptools wheel

$ pip install --upgrade pip setuptools wheel
$ pip install pandas -i https://pypi.mirrors.ustc.edu.cn/simple/

$ sudo pip3 install -r /opt/odoo16/requirements.txt
```

Altro errore su `cffi` l'ho risolto con

```bash
tt-fb@odooserver:~$ sudo pip install --upgrade cffi==1.16.0

$ sudo pip3 uninstall cffi
$ sudo apt-get install python3-cffi

$ sudo pip3 install -r /opt/odoo16/requirements.txt
```


Altro errore su `python-ldap` l'ho risolto con

```bash
$ sudo apt install python-dev libldap2-dev libsasl2-dev libssl-dev
$ sudo apt install python2-dev python2 python-dev-is-python3 libldap2-dev libsasl2-dev libssl-dev
$ sudo pip install python-ldap

$ sudo pip3 install -r /opt/odoo16/requirements.txt
```

Altro errore su `psycopg2` lho risolto con

```bash
sudo apt install libpq-dev python3-dev
sudo apt install build-essential
```




---
---



Download odoo latest branch from below link.

```bash
$ cd /opt/odoo
$ whoami
$ sudo chown tt-fb /opt/odoo
$ cd /opt/odoo
$ git clone https://github.com/odoo/odoo.git --depth 1 --branch 16.0 --single-branch odoo-server
```

> Try using `sudo chown yourUserName /path/to/folder` this will give you ownership of the directory if it was for some reason mounted as root. If this still doesn't work try `chmod +rwx /path/to/folder` which will allow reading and writing to that directory

Setup permission and going to server location folder.

```bash
$ sudo chown -R odoo:odoo /opt/odoo/odoo-server
```






---
---

Warning

wkhtmltopdf is not installed through pip and must be installed manually in version 0.12.5 for it to support headers and footers. Check out the wkhtmltopdf wiki for more details on the various versions.

```bash
$ wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.jammy_amd64.deb
$ sudo dpkg -i wkhtmltox_0.12.6.1-2.jammy_amd64.deb
```




## Step 03: Install requirements.txt file

```bash
(venv) root@odoo:/opt/odoo-odoo-server# pip3 install -r requirements.txt
```

Then exit venv terminal using below command.

```bash
(venv) root@odoo:/opt/odoo/odoo-server# deactivate
```

Setup odoo user permission.

```bash
root@odoo:~# sudo mkdir /var/log/odoo
root@odoo:~# sudo chown odoo:odoo /var/log/odoo
root@odoo:~# sudo chmod 777 /var/log/odoo
```


## Step 04: Create odoo server conf file.

```bash
root@odoo:~# sudo nano /etc/odoo-server.conf
```

Then insert below all lines into this file. This file contain odoo master password its needed when create database from browser.

```bash
[options]
admin_passwd = P@ss$123
db_user = odoo
addons_path = /opt/odoo/odoo-server/addons
logfile = /var/log/odoo/odoo-server.log
log_level  = debug
```

Setup file user permission.

```bash
sudo chown odoo:odoo /etc/odoo-server.conf
```

Create odoo service file.

```bash
root@odoo:~# sudo nano /etc/systemd/system/odoo.service
```

Then insert below all lines into this file.

```bash
[Unit]
Description=Odoo 16.0 Service
Requires=postgresql.service
After=network.target postgresql.service
 
[Service]
Type=simple
SyslogIdentifier=odoo
PermissionsStartOnly=true
User=odoo
Group=odoo
ExecStart=/opt/odoo/odoo-server/venv/bin/python3 /opt/odoo/odoo-server/odoo-bin -c /etc/odoo-server.conf
StandardOutput=journal+console
 
[Install]
WantedBy=multi-user.target
```

Now reload deamon.

```bash
root@odoo:~# sudo systemctl daemon-reload
root@odoo:~# sudo systemctl enable --now odoo.service
root@odoo:~# sudo systemctl status odoo.service
```

Now going to your server ip with port then create database and import demo data.

```bash
http://10.66.10.8:8069
```

See as like below image, Now input some info like master password, database name, email, account password, phone number, country etc. Then click check mark Demo data, then click Create database and wait 1 min for installation process done.