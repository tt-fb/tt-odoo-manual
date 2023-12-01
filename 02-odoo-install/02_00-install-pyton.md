# <a name="top"></a> Cap 2.1 - Installiamo python
Odoo requires Python 3.7 or later to run.


## Verifica iniziale

Verifichiamo se `python` è installato e che versione ha.

```bash
$ python3 --version
```

Verifichiamo se `pip` è installato e che versione ha.
(pip3 is a command line tool for installing Python 3 modules.)

```bash
$ pip3 --version
```

Esempio:

```bash
tt-fb@odooserver:~$ python3 --version
Python 3.10.12
tt-fb@odooserver:~$ pip3 --version
Command 'pip3' not found, but can be installed with:
apt install python3-pip
Please ask your administrator.
tt-fb@odooserver:~$
```

Nel nostro caso è installato `Python 3.10.12` e **non** è installato `pip`



## Step 3a - Installiamo Pip

Installiamo pip3.

```bash
$ sudo apt install -y python3-pip
```

Esempio

```bash
tt-fb@odooserver:~$ sudo apt install -y python3-pip
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following package was automatically installed and is no longer required:
  libnuma1
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  build-essential bzip2 cpp cpp-11 dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-11 gcc
  gcc-11 gcc-11-base javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libasan6 libatomic1 libc-dev-bin libc-devtools libc6-dev libcc1-0
  libcrypt-dev libdeflate0 libdpkg-perl libexpat1-dev libfakeroot libfile-fcntllock-perl libfontconfig1
  libgcc-11-dev libgd3 libgomp1 libisl23 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery
  libjs-sphinxdoc libjs-underscore liblsan0 libmpc3 libnsl-dev libpython3-dev libpython3.10-dev
  libquadmath0 libstdc++-11-dev libtiff5 libtirpc-dev libtsan0 libubsan1 libwebp7 libxpm4
  linux-libc-dev lto-disabled-list make manpages-dev python3-dev python3-wheel python3.10-dev
  rpcsvc-proto zlib1g-dev
Suggested packages:
  bzip2-doc cpp-doc gcc-11-locales debian-keyring g++-multilib g++-11-multilib gcc-11-doc gcc-multilib
  autoconf automake libtool flex bison gdb gcc-doc gcc-11-multilib apache2 | lighttpd | httpd glibc-doc
  bzr libgd-tools libstdc++-11-doc make-doc
The following NEW packages will be installed:
  build-essential bzip2 cpp cpp-11 dpkg-dev fakeroot fontconfig-config fonts-dejavu-core g++ g++-11 gcc
  gcc-11 gcc-11-base javascript-common libalgorithm-diff-perl libalgorithm-diff-xs-perl
  libalgorithm-merge-perl libasan6 libatomic1 libc-dev-bin libc-devtools libc6-dev libcc1-0
  libcrypt-dev libdeflate0 libdpkg-perl libexpat1-dev libfakeroot libfile-fcntllock-perl libfontconfig1
  libgcc-11-dev libgd3 libgomp1 libisl23 libitm1 libjbig0 libjpeg-turbo8 libjpeg8 libjs-jquery
  libjs-sphinxdoc libjs-underscore liblsan0 libmpc3 libnsl-dev libpython3-dev libpython3.10-dev
  libquadmath0 libstdc++-11-dev libtiff5 libtirpc-dev libtsan0 libubsan1 libwebp7 libxpm4
  linux-libc-dev lto-disabled-list make manpages-dev python3-dev python3-pip python3-wheel
  python3.10-dev rpcsvc-proto zlib1g-dev
0 upgraded, 64 newly installed, 0 to remove and 0 not upgraded.
Need to get 71.3 MB of archives.
After this operation, 239 MB of additional disk space will be used.
Get:1 http://europe-west8-a.gce.clouds.archive.ubuntu.com/ubuntu jammy-updates/main amd64 libc-dev-bin amd64 2.35-0ubuntu3.4 [20.3 kB]

... molti pacchetti installati ...

Scanning processes...                                                                                    
Scanning linux images...                                                                                 

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
tt-fb@odooserver:~$ 
```



## Step 3b - Installiamo con Pip i moduli necessari a odoo

Install Packages and libraries.

```bash
$ sudo apt install python-dev python3-dev libxml2-dev libxslt1-dev zlib1g-dev libsasl2-dev libldap2-dev build-essential libssl-dev libffi-dev libmysqlclient-dev libjpeg-dev libpq-dev libjpeg8-dev liblcms2-dev libblas-dev libatlas-base-dev python3-venv python3-wheel
```

Esempio

```bash
tt-fb@odooserver:~$ sudo apt-get install python-dev python3-dev libxml2-dev libxslt1-dev zlib1g-dev libsasl2-dev libldap2-dev build-essential libssl-dev libffi-dev libmysqlclient-dev libjpeg-dev libpq-dev libjpeg8-dev liblcms2-dev libblas-dev libatlas-base-dev
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package python-dev is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
However the following packages replace it:
  python2-dev python2 python-dev-is-python3

E: Package 'python-dev' has no installation candidate
tt-fb@odooserver:~$ 
```

### ALTERNATIVA

Saltiamo questo paragrafo.

su una guida installavano anche questi:

```bash
wget python3-venv python3-wheel
```

Active venv terminal.

```bash
$ cd /opt/odoo/odoo-server
$ sudo python3 -m venv venv
$ source venv/bin/activate
(venv) root@odoo:/opt/odoo/odoo-server# pip3 install wheel

venv_$ sudo chown tt-fb /opt/odoo/odoo-server
```

ma è un modo per far girare pip su un ambiente virtuale. Non ci serve.



## Step 3c - Installiamo dipendenze web (npm)

Install Web web dependencies.

```bash
sudo apt-get install -y npm
sudo ln -s /usr/bin/nodejs /usr/bin/node
sudo npm install -g less less-plugin-clean-css
sudo apt-get install -y node-less
```

Esempio:

```bash
tt-fb@odooserver:~$ sudo apt-get install -y npm
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following package was automatically installed and is no longer required:
  libnuma1
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  adwaita-icon-theme at-spi2-core dconf-gsettings-backend dconf-service fontconfig
  gsettings-desktop-schemas gtk-update-icon-cache gyp hicolor-icon-theme humanity-icon-theme
  libatk-bridge2.0-0 libatk1.0-0 libatk1.0-data libatspi2.0-0 libauthen-sasl-perl libavahi-client3
  libavahi-common-data libavahi-common3 libc-ares2 libcairo-gobject2 libcairo2 libclone-perl libcolord2
  libcups2 libdata-dump-perl libdatrie1 libdconf1 libdrm-amdgpu1 libdrm-intel1 libdrm-nouveau2
  libdrm-radeon1 libencode-locale-perl libepoxy0 libfile-basedir-perl libfile-desktopentry-perl
  libfile-listing-perl libfile-mimeinfo-perl libfont-afm-perl libfontenc1 libgdk-pixbuf-2.0-0
  libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgl1 libgl1-amber-dri libgl1-mesa-dri libglapi-mesa
  libglvnd0 libglx-mesa0 libglx0 libgraphite2-3 libgtk-3-0 libgtk-3-bin libgtk-3-common libgtkd-3-0
  libharfbuzz0b libhtml-form-perl libhtml-format-perl libhtml-parser-perl libhtml-tagset-perl
  libhtml-tree-perl libhttp-cookies-perl libhttp-daemon-perl libhttp-date-perl libhttp-message-perl
  libhttp-negotiate-perl libice6 libio-html-perl libio-socket-ssl-perl libio-stringy-perl
  libipc-system-simple-perl libjs-events libjs-highlight.js libjs-inherits libjs-is-typedarray
  libjs-psl libjs-source-map libjs-sprintf-js libjs-typedarray-to-buffer liblcms2-2 libllvm11 libllvm15
  liblwp-mediatypes-perl liblwp-protocol-https-perl libmailtools-perl libnet-dbus-perl libnet-http-perl
  libnet-smtp-ssl-perl libnet-ssleay-perl libnode-dev libnode72 libnotify-bin libnotify4 libpango-1.0-0
  libpangocairo-1.0-0 libpangoft2-1.0-0 libpciaccess0 libphobos2-ldc-shared98 libpixman-1-0 librsvg2-2
  librsvg2-common libsensors-config libsensors5 libsm6 libssl-dev libthai-data libthai0
  libtie-ixhash-perl libtimedate-perl libtry-tiny-perl liburi-perl libuv1-dev libvte-2.91-0
  libvte-2.91-common libvted-3-0 libwayland-client0 libwayland-cursor0 libwayland-egl1 libwww-perl
  libwww-robotrules-perl libx11-protocol-perl libx11-xcb1 libxaw7 libxcb-dri2-0 libxcb-dri3-0
  libxcb-glx0 libxcb-present0 libxcb-randr0 libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1
  libxcb-xfixes0 libxcomposite1 libxcursor1 libxdamage1 libxfixes3 libxft2 libxi6 libxinerama1
  libxkbcommon0 libxkbfile1 libxml-parser-perl libxml-twig-perl libxml-xpathengine-perl libxmu6
  libxrandr2 libxrender1 libxshmfence1 libxt6 libxtst6 libxv1 libxxf86dga1 libxxf86vm1 node-abab
  node-abbrev node-agent-base node-ansi-regex node-ansi-styles node-ansistyles node-aproba node-archy
  node-are-we-there-yet node-argparse node-arrify node-asap node-asynckit node-balanced-match
  node-brace-expansion node-builtins node-cacache node-chalk node-chownr node-clean-yaml-object
  node-cli-table node-clone node-color-convert node-color-name node-colors node-columnify
  node-combined-stream node-commander node-console-control-strings node-copy-concurrently
  node-core-util-is node-coveralls node-cssom node-cssstyle node-debug node-decompress-response
  node-defaults node-delayed-stream node-delegates node-depd node-diff node-encoding node-end-of-stream
  node-err-code node-escape-string-regexp node-esprima node-events node-fancy-log node-fetch
  node-foreground-child node-form-data node-fs-write-stream-atomic node-fs.realpath node-function-bind
  node-gauge node-get-stream node-glob node-got node-graceful-fs node-growl node-gyp node-has-flag
  node-has-unicode node-hosted-git-info node-https-proxy-agent node-iconv-lite node-iferr
  node-imurmurhash node-indent-string node-inflight node-inherits node-ini node-ip node-ip-regex
  node-is-buffer node-is-plain-obj node-is-typedarray node-isarray node-isexe node-js-yaml node-jsdom
  node-json-buffer node-json-parse-better-errors node-jsonparse node-kind-of node-lcov-parse
  node-lodash-packages node-log-driver node-lowercase-keys node-lru-cache node-mime node-mime-types
  node-mimic-response node-minimatch node-minimist node-minipass node-mkdirp node-move-concurrently
  node-ms node-mute-stream node-negotiator node-nopt node-normalize-package-data node-npm-bundled
  node-npm-package-arg node-npmlog node-object-assign node-once node-opener node-osenv
  node-p-cancelable node-p-map node-path-is-absolute node-process-nextick-args node-promise-inflight
  node-promise-retry node-promzard node-psl node-pump node-punycode node-quick-lru node-read
  node-read-package-json node-readable-stream node-resolve node-retry node-rimraf node-run-queue
  node-safe-buffer node-semver node-set-blocking node-signal-exit node-slash node-slice-ansi
  node-source-map node-source-map-support node-spdx-correct node-spdx-exceptions
  node-spdx-expression-parse node-spdx-license-ids node-sprintf-js node-ssri node-stack-utils
  node-stealthy-require node-string-decoder node-string-width node-strip-ansi node-supports-color
  node-tap node-tap-mocha-reporter node-tap-parser node-tar node-text-table node-time-stamp node-tmatch
  node-tough-cookie node-typedarray-to-buffer node-unique-filename node-universalify
  node-util-deprecate node-validate-npm-package-license node-validate-npm-package-name node-wcwidth.js
  node-webidl-conversions node-whatwg-fetch node-which node-wide-align node-wrappy
  node-write-file-atomic node-ws node-yallist nodejs nodejs-doc perl-openssl-defaults session-migration
  tilix tilix-common ubuntu-mono x11-common x11-utils x11-xserver-utils xdg-utils
Suggested packages:
  libdigest-hmac-perl libgssapi-perl colord cups-common gvfs libjs-angularjs liblcms2-utils
  libcrypt-ssleay-perl gnome-shell | notification-daemon librsvg2-bin lm-sensors libssl-doc
  libsub-name-perl libbusiness-isbn-perl libauthen-ntlm-perl libunicode-map8-perl
  libunicode-string-perl xml-twig-tools node-nyc python-nautilus mesa-utils nickle cairo-5c
  xorg-docs-core
The following NEW packages will be installed:
  adwaita-icon-theme at-spi2-core dconf-gsettings-backend dconf-service fontconfig
  gsettings-desktop-schemas gtk-update-icon-cache gyp hicolor-icon-theme humanity-icon-theme
  libatk-bridge2.0-0 libatk1.0-0 libatk1.0-data libatspi2.0-0 libauthen-sasl-perl libavahi-client3
  libavahi-common-data libavahi-common3 libc-ares2 libcairo-gobject2 libcairo2 libclone-perl libcolord2
  libcups2 libdata-dump-perl libdatrie1 libdconf1 libdrm-amdgpu1 libdrm-intel1 libdrm-nouveau2
  libdrm-radeon1 libencode-locale-perl libepoxy0 libfile-basedir-perl libfile-desktopentry-perl
  libfile-listing-perl libfile-mimeinfo-perl libfont-afm-perl libfontenc1 libgdk-pixbuf-2.0-0
  libgdk-pixbuf2.0-bin libgdk-pixbuf2.0-common libgl1 libgl1-amber-dri libgl1-mesa-dri libglapi-mesa
  libglvnd0 libglx-mesa0 libglx0 libgraphite2-3 libgtk-3-0 libgtk-3-bin libgtk-3-common libgtkd-3-0
  libharfbuzz0b libhtml-form-perl libhtml-format-perl libhtml-parser-perl libhtml-tagset-perl
  libhtml-tree-perl libhttp-cookies-perl libhttp-daemon-perl libhttp-date-perl libhttp-message-perl
  libhttp-negotiate-perl libice6 libio-html-perl libio-socket-ssl-perl libio-stringy-perl
  libipc-system-simple-perl libjs-events libjs-highlight.js libjs-inherits libjs-is-typedarray
  libjs-psl libjs-source-map libjs-sprintf-js libjs-typedarray-to-buffer liblcms2-2 libllvm11 libllvm15
  liblwp-mediatypes-perl liblwp-protocol-https-perl libmailtools-perl libnet-dbus-perl libnet-http-perl
  libnet-smtp-ssl-perl libnet-ssleay-perl libnode-dev libnode72 libnotify-bin libnotify4 libpango-1.0-0
  libpangocairo-1.0-0 libpangoft2-1.0-0 libpciaccess0 libphobos2-ldc-shared98 libpixman-1-0 librsvg2-2
  librsvg2-common libsensors-config libsensors5 libsm6 libssl-dev libthai-data libthai0
  libtie-ixhash-perl libtimedate-perl libtry-tiny-perl liburi-perl libuv1-dev libvte-2.91-0
  libvte-2.91-common libvted-3-0 libwayland-client0 libwayland-cursor0 libwayland-egl1 libwww-perl
  libwww-robotrules-perl libx11-protocol-perl libx11-xcb1 libxaw7 libxcb-dri2-0 libxcb-dri3-0
  libxcb-glx0 libxcb-present0 libxcb-randr0 libxcb-render0 libxcb-shape0 libxcb-shm0 libxcb-sync1
  libxcb-xfixes0 libxcomposite1 libxcursor1 libxdamage1 libxfixes3 libxft2 libxi6 libxinerama1
  libxkbcommon0 libxkbfile1 libxml-parser-perl libxml-twig-perl libxml-xpathengine-perl libxmu6
  libxrandr2 libxrender1 libxshmfence1 libxt6 libxtst6 libxv1 libxxf86dga1 libxxf86vm1 node-abab
  node-abbrev node-agent-base node-ansi-regex node-ansi-styles node-ansistyles node-aproba node-archy
  node-are-we-there-yet node-argparse node-arrify node-asap node-asynckit node-balanced-match
  node-brace-expansion node-builtins node-cacache node-chalk node-chownr node-clean-yaml-object
  node-cli-table node-clone node-color-convert node-color-name node-colors node-columnify
  node-combined-stream node-commander node-console-control-strings node-copy-concurrently
  node-core-util-is node-coveralls node-cssom node-cssstyle node-debug node-decompress-response
  node-defaults node-delayed-stream node-delegates node-depd node-diff node-encoding node-end-of-stream
  node-err-code node-escape-string-regexp node-esprima node-events node-fancy-log node-fetch
  node-foreground-child node-form-data node-fs-write-stream-atomic node-fs.realpath node-function-bind
  node-gauge node-get-stream node-glob node-got node-graceful-fs node-growl node-gyp node-has-flag
  node-has-unicode node-hosted-git-info node-https-proxy-agent node-iconv-lite node-iferr
  node-imurmurhash node-indent-string node-inflight node-inherits node-ini node-ip node-ip-regex
  node-is-buffer node-is-plain-obj node-is-typedarray node-isarray node-isexe node-js-yaml node-jsdom
  node-json-buffer node-json-parse-better-errors node-jsonparse node-kind-of node-lcov-parse
  node-lodash-packages node-log-driver node-lowercase-keys node-lru-cache node-mime node-mime-types
  node-mimic-response node-minimatch node-minimist node-minipass node-mkdirp node-move-concurrently
  node-ms node-mute-stream node-negotiator node-nopt node-normalize-package-data node-npm-bundled
  node-npm-package-arg node-npmlog node-object-assign node-once node-opener node-osenv
  node-p-cancelable node-p-map node-path-is-absolute node-process-nextick-args node-promise-inflight
  node-promise-retry node-promzard node-psl node-pump node-punycode node-quick-lru node-read
  node-read-package-json node-readable-stream node-resolve node-retry node-rimraf node-run-queue
  node-safe-buffer node-semver node-set-blocking node-signal-exit node-slash node-slice-ansi
  node-source-map node-source-map-support node-spdx-correct node-spdx-exceptions
  node-spdx-expression-parse node-spdx-license-ids node-sprintf-js node-ssri node-stack-utils
  node-stealthy-require node-string-decoder node-string-width node-strip-ansi node-supports-color
  node-tap node-tap-mocha-reporter node-tap-parser node-tar node-text-table node-time-stamp node-tmatch
  node-tough-cookie node-typedarray-to-buffer node-unique-filename node-universalify
  node-util-deprecate node-validate-npm-package-license node-validate-npm-package-name node-wcwidth.js
  node-webidl-conversions node-whatwg-fetch node-which node-wide-align node-wrappy
  node-write-file-atomic node-ws node-yallist nodejs nodejs-doc npm perl-openssl-defaults
  session-migration tilix tilix-common ubuntu-mono x11-common x11-utils x11-xserver-utils xdg-utils
0 upgraded, 336 newly installed, 0 to remove and 0 not upgraded.
Need to get 103 MB of archives.
After this operation, 458 MB of additional disk space will be used.
Get:1 http://europe-west8-a.gce.clouds.archive.ubuntu.com/ubuntu jammy/main amd64 hicolor-icon-theme all 0.17-2 [9976 B]

... molti pacchetti installati ...

Scanning processes...                                                                                    
Scanning linux images...                                                                                 

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
tt-fb@odooserver:~$

tt-fb@odooserver:~$ sudo ln -s /usr/bin/nodejs /usr/bin/node
ln: failed to create symbolic link '/usr/bin/node': File exists
tt-fb@odooserver:~$ 

tt-fb@odooserver:~$ sudo npm install -g less less-plugin-clean-css

added 26 packages, and audited 27 packages in 4s

1 package is looking for funding
  run `npm fund` for details

1 low severity vulnerability

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
tt-fb@odooserver:~$ 

tt-fb@odooserver:~$ sudo npm audit fix --force
npm WARN using --force Recommended protections disabled.
npm ERR! code ENOLOCK
npm ERR! audit This command requires an existing lockfile.
npm ERR! audit Try creating one first with: npm i --package-lock-only
npm ERR! audit Original error: loadVirtual requires existing shrinkwrap file

npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2023-12-01T10_22_24_814Z-debug-0.log
tt-fb@odooserver:~$ npm i --package-lock-only
npm ERR! code ENOENT
npm ERR! syscall open
npm ERR! path /home/tt-fb/package.json
npm ERR! errno -2
npm ERR! enoent ENOENT: no such file or directory, open '/home/tt-fb/package.json'
npm ERR! enoent This is related to npm not being able to find a file.
npm ERR! enoent 

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/tt-fb/.npm/_logs/2023-12-01T10_22_51_641Z-debug-0.log
tt-fb@odooserver:~$ sudo npm i --package-lock-only
npm ERR! code ENOENT
npm ERR! syscall open
npm ERR! path /home/tt-fb/package.json
npm ERR! errno -2
npm ERR! enoent ENOENT: no such file or directory, open '/home/tt-fb/package.json'
npm ERR! enoent This is related to npm not being able to find a file.
npm ERR! enoent 

npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2023-12-01T10_22_56_859Z-debug-0.log
tt-fb@odooserver:~$ 

tt-fb@odooserver:~$ sudo apt-get install -y node-less
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following package was automatically installed and is no longer required:
  libnuma1
Use 'sudo apt autoremove' to remove it.
The following additional packages will be installed:
  node-tslib
The following NEW packages will be installed:
  node-less node-tslib
0 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
Need to get 516 kB of archives.
After this operation, 4339 kB of additional disk space will be used.
Get:1 http://europe-west8-a.gce.clouds.archive.ubuntu.com/ubuntu jammy/universe amd64 node-tslib all 2.3.1-2 [16.1 kB]
Get:2 http://europe-west8-a.gce.clouds.archive.ubuntu.com/ubuntu jammy/universe amd64 node-less all 3.13.0+dfsg-7 [500 kB]
Fetched 516 kB in 0s (2570 kB/s)  
Selecting previously unselected package node-tslib.
(Reading database ... 96133 files and directories currently installed.)
Preparing to unpack .../node-tslib_2.3.1-2_all.deb ...
Unpacking node-tslib (2.3.1-2) ...
Selecting previously unselected package node-less.
Preparing to unpack .../node-less_3.13.0+dfsg-7_all.deb ...
Unpacking node-less (3.13.0+dfsg-7) ...
Setting up node-tslib (2.3.1-2) ...
Setting up node-less (3.13.0+dfsg-7) ...
Processing triggers for man-db (2.10.2-1) ...
Scanning processes...                                                                                    
Scanning linux images...                                                                                 

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
tt-fb@odooserver:~$ 
```


Configuriamo PostgreSQL nel prossimo capitolo



## ALTERNATIVA per installare le dipendenze

Noi abbiamo usato pip per installare le dipendenze.
Qui c'è un metodo alternativo che possiamo saltare.

Using distribution packages is the preferred way of installing dependencies. Alternatively, install the Python dependencies with pip.

```bash
$ cd /CommunityPath
$ sed -n -e '/^Depends:/,/^Pre/ s/ python3-\(.*\),/python3-\1/p' debian/control | sudo xargs apt-get install -y
```

> For languages using a right-to-left interface (such as Arabic or Hebrew), the rtlcss package is required.
> `$ sudo npm install -g rtlcss`
