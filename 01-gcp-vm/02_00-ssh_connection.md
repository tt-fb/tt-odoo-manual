# <a name="top"></a> Cap 1.2 - Creiamo un collegamento SSH alla GCP VM

Colleghiamoci alla macchina virtuale di google cloud platform tramite Secure SHell (SSH).



## Risorse esterne

- [How to connect to GCP VM Instance using SSH MacOS Terminal](https://www.youtube.com/watch?v=2ibBF9YqveY)
  Questo video ha funzionato!!! E mi sembra anche molto semplice. Un ottimo punto di partenza.
  Spiega come collegarsi con MAC e c'è un altro video che spiega come collegarsi con Windows
- [How to connect to GCP VM Instance using SSH on WINDOWS](https://www.youtube.com/watch?v=StA1i-p6G4o)
  Questo video è come quello sopra ma pe WINDOWS.
  Su windows dobbiamo installare le applicazioni "PUTTY" e "PUTTYGEN".
- [How to Connect to Google Compute Engine Virtual Machine with SSH or puTTY on Mac](https://www.youtube.com/watch?v=vA18jo-4gu4)
  Anche questo video dice la stessa cosa ma con altri spunti
- [stackoverflow: ssh to google cloud platform - permission denied](https://stackoverflow.com/questions/51614552/google-cloud-platform-ssh-to-google-cloud-instance-will-have-permission-denied)
  Qui c’è una nota interessante (comunque già considerata nei video sopra)



## Colleghiamoci alla VM da Mac con SSH
Per collegarci dobbiamo creare una coppia di chiavi (Privata e Pubblica). Metteremo la chiave pubblica sull'istanza della VM (Virtual Machine) su GCP (Google Cloud Platform) e ci colleghiamo usando la nostra chiave privata.

Lanciamo il terminale e creiamo la coppia di chiavi:

```bash
$ cd ~/.ssh
$ ssh-keygen -t rsa -f fb-odoo-server-key -C tt-fb
```

> nota: per la "passfrase" lascio il campo vuoto

- `cd ~` entra nella cartella dell'utente. Nel mio caso `/Users/FB`.
    `/.ssh` entra nella cartella nascosta dove, di default, sono raccolti i files delle chiavi
- `-t` è per scegliere il tipo di criptatura. Abbiamo scelto `rsa`.
- `-f` è per scegliere la cartella su cui mettere le chiavi.
- `-C` è per lo "username". In questo caso `tt-fb`

Esempio:

```bash
MacBook-Pro-di-Flavio:~ FB$ cd ~/.ssh
MacBook-Pro-di-Flavio:.ssh FB$ ls
config		id_rsa		id_rsa.pub	known_hosts
MacBook-Pro-di-Flavio:.ssh FB$ ssh-keygen -t rsa -f fb-odoo-server-key -C tt-fb
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in fb-odoo-server-key.
Your public key has been saved in fb-odoo-server-key.pub.
The key fingerprint is:
SHA256:q1/+wWXQN2r5/diPxCwhF7sGRyC7cacP/nnnR0kBrJQ tt-fb
The key randomart image is:
+---[RSA 3072]----+
|        . . o..  |
|         o E * . |
|        o o o ..o|
|         + = +oo.|
|        S = =++ .|
|         + O.A..o|
|        . o C +o.|
|       . o o =.++|
|      ... ..+.ooB|
+----[SHA256]-----+
MacBook-Pro-di-Flavio:.ssh FB$ ls
config			fb-odoo-server-key	fb-odoo-server-key.pub	id_rsa			id_rsa.pub		known_hosts
MacBook-Pro-di-Flavio:.ssh FB$ 
```


## Mettiamo la chiave pubblica sulla nostra GCP VM

Andiamo su GCP -> Compute Engine -> VM Instances

- click sul nome istanza "odoo-server"
- click su EDIT
- scroll down until you find SSH Keys -> click "+ ADD ITEM" button
- inserisci dentro il campo che ti si presenta il contenuto del file "fb-odoo-server-key.pub"

Lo puoi fare da interfaccia grafica:

- vai nella cartella FlaMac -> Users -> FB
- premi Command + Shift + . (the period key). This will show hidden files in the folder. (To hide the files again, press Command + Shift + . again.)
- entra nella cartella .ssh ed apri il file `fb-odoo-server-key.pub` con TextEdit
- copia TUTTO il testo incluso "ssh-rsa" iniziale e "tt-fb" finale.

Oppure da terminale:

```bash
$ cd ~/.ssh
$ cat fb-odoo-server-key.pub
```

Esempio:

```bash
MacBook-Pro-di-Flavio:.ssh FB$ cat fb-odoo-server-key.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC4JaFYyGoTCCIRESm6hLS6XhhNzqZqRK/YdSNEQIoFePs+KqGM+s1AYWOhecHpT/8h5x7h5GwuZHdYUFScHoVS5Qu1UhdJaXqvApHHNrFB0MpjuX9mag+KNHySAsnAuxKHxJ/0DDzUUYzWHS647tlfuZJEUCUa4DAYvJp6K9cGiXO8YL9qY8WC3KJMOd4Yy4hRZWq44L17aklZigY9564/ILErDYNPz++EXamj+6RfW/WbZ8c0iLTC5QJ1bUhjnJOKaxtZ0h5uHY03+bb3EDVx3w0eKMcUIaBMj4i8g2CRrRLUr1LUt8ZLuKC2bTTqw+X5WsP6FOSjsLbNN1KiHnS3P6qApql4m2ni8E5P0mFJT+hL9+0hRh4vYbWtJqrFWiyFjEOAfLe5HlhVMLgyLKuJ6vbhY+pbo7c+JAHOxrNIZigp5f5l3IbmwqyZDcHUoIG8aGLt/Vx9ONZ6nCQgWLnXxxPfh5tHbluo4RAhcJPM06L0xNVvQfypoCjbie2nvkk= tt-fb
MacBook-Pro-di-Flavio:.ssh FB$
```



## Colleghiamoci
Per collegarci useremo la nostra chiave privata (il file "fb-odoo-server-key")

```bash
$ ssh -i ~/.ssh/fb-odoo-server-key tt-fb@34.154.165.20
```

- `tt-fb@34.154.240.173`: username + indirizzo IP PUBBLICO della VM GCP

Esempio:

```bash
MacBook-Pro-di-Flavio:.ssh FB$ ssh -i ~/.ssh/fb-odoo-server-key tt-fb@34.154.240.173
The authenticity of host '34.154.240.173 (34.154.240.173)' can't be established.
ECDSA key fingerprint is SHA256:FNEV+0eHZs7if63nAFmjLdUNutUSWiyIIQVQyBSSvxo.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '34.154.240.173' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 6.2.0-1018-gcp x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Nov 20 15:46:52 UTC 2023

  System load:  0.0               Processes:             99
  Usage of /:   3.8% of 48.27GB   Users logged in:       0
  Memory usage: 2%                IPv4 address for ens4: 10.198.0.2
  Swap usage:   0%

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

tt-fb@server-odoo:~$ 
```



## Colleghiamoci con un'altra chiave di criptatura SSH
Possiamo saltare questo paragrafo.
A scopo didattico creiamo un'altra coppia di chiavi.

Lanciamo il terminale:

```bash
$ ssh-keygen -t rsa -f ~/Desktop/other-key -C otheruser
```

- `-t` è per scegliere il tipo di criptatura. Abbiamo scelto `rsa`.
- `-f` è per scegliere la cartella su cui mettere le chiavi ed il nome delle chiavi.
- `-C` è per lo "username". In questo caso `otheruser`

Questo comando ci crea i seguenti due files sul desktop:
- `other-key` : che è la chiave privata
- `other-key.pub` : che è la chiave pubblica


Altro modo di creare la stessa coppia di chiavi:

```bash
$ cd ~/Desktop
$ ssh-keygen -t rsa -f other-key -C otheruser -b 2048
```

- `-f` sono già nella cartella che mi interessa quindi do solo il nome delle chiavi.
- `-b` è la dimensione della chiave in bits (key size in bits). In questo caso `2048`



## Mettiamo la chiave pubblica sulla nostra VM

Andiamo su GCP -> Compute Engine -> VM Instances
- click sul nome istanza "odoo-server"
- click su EDIT
- scroll down until you find "You have 1 SSH keys" -> click "show and edit" button
- inserisci dentro il campo che ti si presenta il contenuto del file "other-key.pub"
  (il file other-key.pub lo puoi aprire con TextEdit)


## Colleghiamoci
Per collegarci useremo la nostra chiave privata (il file "other-key")

```bash
$ ssh -i ~/Desktop/other-key otheruser@35.198.222.21
```



## Alcuni tentativi che NON hanno funzionato

DI SEGUITO TENTATIVI CHE NON HANNO FUNZIONATO!

https://cloud.google.com/sdk/docs/install?hl=it

Verifica di disporre di una versione supportata di Python
Per verificare la versione attuale di Python, esegui python3 -V o python -V. Le versioni supportate sono Python 3 (da 3.8 a 3.9).

```bash
MacBook-Pro-di-Flavio:~ FB$ python3 -V
Python 3.8.2
MacBook-Pro-di-Flavio:~ FB$ python -V
Python 2.7.16
```

Scarica il pacchetto
Per determinare il nome dell'hardware della tua macchina, esegui uname -m dalla riga di comando.

```bash
MacBook-Pro-di-Flavio:~ FB$ uname -m 
x86_64
```

Scarica il relativo pacchetto.
Estrai l'archivio in qualsiasi posizione del file system (preferibilmente nella directory Home). 

il file è `google-cloud-cli-451.0.0-darwin-x86_64.tar.gz`

Fatto doppio click per scompattare il pacchetto ed ho ottenuto la cartella “google-cloud-sdk” cho ho copiato su “FlaMac/Users/FB/”

Apro il terminale vado nella cartella FB ed eseguo:   ./google-cloud-sdk/install.sh
Do “y” a tutte le richieste.

[Purtroppo il processo mi si blocca durante installazione di python 3.10]

```bash
MacBook-Pro-di-Flavio:~ FB$ ./google-cloud-sdk/install.sh
Welcome to the Google Cloud CLI!
To help improve the quality of this product, we collect anonymized usage data
and anonymized stacktraces when crashes are encountered; additional information
is available at <https://cloud.google.com/sdk/usage-statistics>. This data is
handled in accordance with our privacy policy
<https://cloud.google.com/terms/cloud-privacy-notice>. You may choose to opt in this
collection now (by choosing 'Y' at the below prompt), or at any time in the
future by running the following command:
    gcloud config set disable_usage_reporting false
Do you want to help improve the Google Cloud CLI (y/N)?  
Your current Google Cloud CLI version is: 451.0.0
The latest available version is: 451.0.1
┌────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                                     Components                                                     │
├──────────────────┬──────────────────────────────────────────────────────┬──────────────────────────────┬───────────┤
│      Status      │                         Name                         │              ID              │    Size   │
├──────────────────┼──────────────────────────────────────────────────────┼──────────────────────────────┼───────────┤
│ Update Available │ Google Cloud CLI Core Libraries                      │ core                         │  21.9 MiB │
│ Not Installed    │ App Engine Go Extensions                             │ app-engine-go                │   4.4 MiB │
│ Not Installed    │ Appctl                                               │ appctl                       │  18.5 MiB │
│ Not Installed    │ Artifact Registry Go Module Package Helper           │ package-go-module            │   < 1 MiB │
│ Not Installed    │ Cloud Bigtable Command Line Tool                     │ cbt                          │  15.9 MiB │
│ Not Installed    │ Cloud Bigtable Emulator                              │ bigtable                     │   7.0 MiB │
│ Not Installed    │ Cloud Datastore Emulator                             │ cloud-datastore-emulator     │  36.2 MiB │
│ Not Installed    │ Cloud Firestore Emulator                             │ cloud-firestore-emulator     │  42.8 MiB │
│ Not Installed    │ Cloud Pub/Sub Emulator                               │ pubsub-emulator              │  62.1 MiB │
│ Not Installed    │ Cloud Run Proxy                                      │ cloud-run-proxy              │  11.7 MiB │
│ Not Installed    │ Cloud SQL Proxy                                      │ cloud_sql_proxy              │   7.6 MiB │
│ Not Installed    │ Google Container Registry's Docker credential helper │ docker-credential-gcr        │   2.2 MiB │
│ Not Installed    │ Kustomize                                            │ kustomize                    │   7.6 MiB │
│ Not Installed    │ Log Streaming                                        │ log-streaming                │  12.3 MiB │
│ Not Installed    │ Minikube                                             │ minikube                     │  34.0 MiB │
│ Not Installed    │ Nomos CLI                                            │ nomos                        │  28.0 MiB │
│ Not Installed    │ On-Demand Scanning API extraction helper             │ local-extract                │  14.1 MiB │
│ Not Installed    │ Skaffold                                             │ skaffold                     │  25.2 MiB │
│ Not Installed    │ Terraform Tools                                      │ terraform-tools              │  66.4 MiB │
│ Not Installed    │ anthos-auth                                          │ anthos-auth                  │  20.2 MiB │
│ Not Installed    │ config-connector                                     │ config-connector             │  57.1 MiB │
│ Not Installed    │ enterprise-certificate-proxy                         │ enterprise-certificate-proxy │   6.7 MiB │
│ Not Installed    │ gcloud Alpha Commands                                │ alpha                        │   < 1 MiB │
│ Not Installed    │ gcloud Beta Commands                                 │ beta                         │   < 1 MiB │
│ Not Installed    │ gcloud app Java Extensions                           │ app-engine-java              │ 123.7 MiB │
│ Not Installed    │ gcloud app PHP Extensions                            │ app-engine-php               │  21.9 MiB │
│ Not Installed    │ gcloud app Python Extensions                         │ app-engine-python            │   8.3 MiB │
│ Not Installed    │ gcloud app Python Extensions (Extra Libraries)       │ app-engine-python-extras     │  31.5 MiB │
│ Not Installed    │ gke-gcloud-auth-plugin                               │ gke-gcloud-auth-plugin       │   7.8 MiB │
│ Not Installed    │ kpt                                                  │ kpt                          │  15.1 MiB │
│ Not Installed    │ kubectl                                              │ kubectl                      │   < 1 MiB │
│ Not Installed    │ kubectl-oidc                                         │ kubectl-oidc                 │  20.2 MiB │
│ Not Installed    │ pkg                                                  │ pkg                          │           │
│ Installed        │ BigQuery Command Line Tool                           │ bq                           │   1.6 MiB │
│ Installed        │ Cloud Storage Command Line Tool                      │ gsutil                       │  11.3 MiB │
│ Installed        │ Google Cloud CRC32C Hash Tool                        │ gcloud-crc32c                │   1.2 MiB │
└──────────────────┴──────────────────────────────────────────────────────┴──────────────────────────────┴───────────┘
To install or remove components at your current SDK version [451.0.0], run:
  $ gcloud components install COMPONENT_ID
  $ gcloud components remove COMPONENT_ID
To update your SDK installation to the latest version [451.0.1], run:
  $ gcloud components update
Modify profile to update your $PATH and enable shell command completion?
Do you want to continue (Y/n)?  
The Google Cloud SDK installer will now prompt you to update an rc file to bring
 the Google Cloud CLIs into your environment.
Enter a path to an rc file to update, or leave blank to use 
[/Users/FB/.bash_profile]:  
No changes necessary for [/Users/FB/.bash_profile].
Google Cloud CLI works best with Python 3.10 and certain modules.
Python 3.10 installation detected, install recommended modules? (Y/n)?  
Setting up virtual environment
Creating virtualenv...
Installing modules...
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.3/2.3 MB 19.1 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
  Preparing metadata (setup.py) ... done
  DEPRECATION: crcmod is being installed using the legacy 'setup.py install' method, because it does not have a 'pyproject.toml' and the 'wheel' package is not installed. pip 23.1 will enforce this behaviour change. A possible replacement is to enable the '--use-pep517' option. Discussion can be found at https://github.com/pypa/pip/issues/8559
  Running setup.py install for crcmod ... done
  DEPRECATION: grpcio is being installed using the legacy 'setup.py install' method, because it does not have a 'pyproject.toml' and the 'wheel' package is not installed. pip 23.1 will enforce this behaviour change. A possible replacement is to enable the '--use-pep517' option. Discussion can be found at https://github.com/pypa/pip/issues/8559
^C  Running setup.py install for grpcio ... canceled
ERROR: Operation cancelled by user
```

Lascio così e vado avanti.
Sembra non funzionare.



---
https://cloud.google.com/compute/docs/instances/connecting-advanced?hl=it#thirdpartytools

Connessione a VM Linux mediante metodi avanzati

Per fornire la chiave SSH all'istanza, utilizza uno dei seguenti metodi:

(Opzione consigliata) Attiva OS Login. OS Login utilizza i ruoli IAM per fornire la chiave SSH pubblica all'istanza tramite il tuo Account Google o un account utente gestito. Per le istruzioni, consulta la pagina Configurare OS Login.

https://cloud.google.com/compute/docs/oslogin/set-up-oslogin?hl=it

Configurare OS Login
https://www.youtube.com/watch?v=I29400R8tXg&t=49s

![odoo-server metadati](https://github.com/tt-fb/tt-odoo-manual/blob/main/01-gcp-vm/02_81-odoo-server-metadati.png)

Edit della mia VM e su Metadati click su + AGGIUNGI ELEMENTO
chiave: enable-oslogin
valore: TRUE

![odoo-server metadati](https://github.com/tt-fb/tt-odoo-manual/blob/main/01-gcp-vm/02_82-odoo-server-metadati.png)

click SALVA
→ OS Login è ora abilitato su questa istanza di VM e solo gli utenti con un appropriato ruolo IAM possono collegarsi attraverso SSH.

LO HO POI TOLTO PERCHÈ QUESTO AUMENTA LE RESTRIZIONI.

