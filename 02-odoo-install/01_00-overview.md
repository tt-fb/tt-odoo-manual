# <a name="top"></a> Cap 2.1 - Installiamo Odoo

Odoo is an open source software used as business purposes like crm, invoice, ecommerce, billing, accounting, project management and inventory management and more. Now I want to share how to install Odoo latest version on Ubuntu 22.04 server.



## Risorse esterne

- [Odoo docs: Install and Maintain](https://www.odoo.com/documentation/16.0/administration.html)
- [Odoo docs: Install / Source](https://www.odoo.com/documentation/16.0/administration/install/source.html)
- [How to Install Odoo 16 on Ubuntu 20.04 LTS](https://www.cybrosys.com/blog/how-to-install-odoo-16-on-ubuntu-2004-lts)


- [How To Install Odoo 16 on Ubuntu 22.04 - post](https://technologyrss.com/how-to-install-odoo-16-on-ubuntu-22-04/)
- [How To Install Odoo 16 on Ubuntu 22.04 - video](https://www.youtube.com/watch?v=VblqEEFY7Cs)


## Overview

Il tipo di installazione che faremo è quella da sorgente (Source) perché è quella che ci permette maggiore flessibilità.

Installeremo dal repository di Github https://github.com/odoo/odoo

```bash
$ git clone https://github.com/odoo/odoo.git
```

Ma facciamo un passo alla volta.

Vediamo i vari passi:
0. prepariamo una Virtual Machine con Ubuntu 22.04
1. la Virtual Machine
  a. Aggiorniamo il sistema operativo
  b. Mettiamo il server in sicurezza
  c. Aggiungiamo utente
2. Installiamo/aggiorniamo Python ed i relativi pacchetti e librerie necessari a odoo
  a. Installiamo Pyton e PIP3 (pip3 is a command line tool for installing Python 3 modules.)
  b. Installiamo con pip3 i moduli Pyton che ci servono per odoo (pacchetti e librerie)
  c. Installiamo dipendenze web (npm)
3. Installiamo postgresql
4. Copiamo il sorgente di odoo con git e configuriamo l'ambiente
  a. Prepariamo l'utente userodoo16 sia per postgresql che per odoo
  b. Copiamo il codice sorgente di odoo 16 community tramite git 



## Step 1 - la VM

Abbiamo già preparato nel capitolo precedente "gcp-vm" un computer virtuale con le seguenti caratteristiche:

```
RAM 		          : 8GB
Disk 		          : 50GB
IP Address 	      : 35.198.222.21
Operating System  : Ubuntu 22.04 LTS
Nome Utente       : odoo16
```



## Step 1a - Aggiorniamo il sistema operativo

Colleghiamoci al computer virtuale ed aggiorniamo il sistema operativo

```bash
$ ssh -i ~/.ssh/fb-odoo-server-key tt-fb@34.154.165.20
$ lsb_release -a && ip r
$ sudo apt update 
$ sudo apt upgrade
```


## Step 1b - mettiamo in sicurezza il server

Make sure the system is protected against ssh assaults; using Fail2ban will aid in ssh attack prevention.

```bash
sudo apt install openssh-server fail2ban
```


## Step 1c - Aggiungiamo utente

Creiamo un nuovo utente di sistema
Next, let's create a system user for security and **to fulfill Odoo roles**.
This user will only have limited access to certain files and locations within Odoo.
After that, we'll restrict this user's access to all files and directories linked to Odoo.

```bash
$ sudo adduser --system --home=/opt/odoo16 --group odoo16
```

ALTERNATIVA VECCHIA:

```bash
$ sudo adduser --system --group --home=/opt/odoo --shell=/bin/bash odoo
```


- `--home=/opt/odoo16` -> crea la nuova cartella `odoo16` su cui copieremo poi tutto il sorgente tramite git
- `odoo16` è il nome che diamo al nuovo utente di sistema

Esempio:

```bash
tt-fb@odooserver:~$ sudo adduser --system --home=/opt/odoo16 --group odoo16
Adding system user `odoo16' (UID 114) ...
Adding new group `odoo16' (GID 122) ...
Adding new user `odoo16' (UID 114) with group `odoo16' ...
Creating home directory `/opt/odoo16' ...
```

Nel prossimo capitolo installiamo Python
