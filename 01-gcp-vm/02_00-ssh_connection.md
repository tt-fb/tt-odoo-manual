# <a name="top"></a> Cap 1.2 - Colleghiamo VS Code all GCP VM

Colleghiamo la nostra app Visual Studio Code alla macchina virtuale su google cloud platform.



## Risorse esterne

- [How to connect to GCP VM Instance using SSH MacOS Terminal](https://www.youtube.com/watch?v=2ibBF9YqveY)
  Questo video ha funzionato!!! E mi sembra anche molto semplice. Un ottimo punto di partenza.
  Spiega come collegarsi con MAC e c'è un altro video che spiega come collegarsi con Windows
- [How to Connect to Google Compute Engine Virtual Machine with SSH or puTTY on Mac](https://www.youtube.com/watch?v=vA18jo-4gu4)
  Anche questo video dice la stessa cosa ma con altri spunti
- [stackoverflow: ssh to google cloud platform - permission denied](https://stackoverflow.com/questions/51614552/google-cloud-platform-ssh-to-google-cloud-instance-will-have-permission-denied)
  Qui c’è una nota interessante (comunque già considerata nei video sopra)
- [SSH into Remote VM with VS Code | Tunneling into any cloud | GCP Demo](https://www.youtube.com/watch?v=0Bjx3Ra8PRM)
  Qui parla di più su VS code


---
Using VS Code with GCP VMs
https://learn.canceridc.dev/cookbook/virtual-machines/using-vs-code-with-gcp-vms

Use VSCode and Remote SSH extension to connect to Compute Engine on Google Cloud
https://medium.com/@ivanzhd/vscode-sftp-connection-to-compute-engine-on-google-cloud-platform-gcloud-9312797d56eb



## Colleghiamoci alla VM da Mac con SSH
Per collegarci dobbiamo creare una coppia di chiavi (Privata e Pubblica). Metteremo la chiave pubblica sull'istanza della VM (Virtual Machine) di GCP (Google Cloud Platform) e ci colleghiamo usando la nostra chiave privata.

Lanciamo il terminale e creiamo la coppia di chiavi:

```bash
$ ssh-keygen -t rsa -f ~/Desktop/key -C techamatic
```

- `-t` è per scegliere il tipo di criptatura. Abbiamo scelto `rsa`.
- `-f` è per scegliere la cartella su cui mettere le chiavi.
- `-C` sta per "comment"
- e per ultimo lo "username". In questo caso `techamatic`

Questo comando ci crea i seguenti due files sul desktop:
- key (che è la chiave privata)
- key.pub (che è la chiave pubblica)


## Mettiamo la chiave pubblica sulla nostra VM

Andiamo su GCP -> Compute Engine -> VM Instances
- click sul nome istanza "odoo-server"
- click su EDIT
- scroll down until you find "You have 0 SSH keys" -> click "show and edit" button
- inserisci dentro il campo che ti si presenta il contenuto del file "key.pub"
  (il file key.pub lo puoi aprire con TextEdit)


## Colleghiamoci
Per collegarci useremo la nostra chiave privata (il file "key")

```bash
$ ssh -i ~/Desktop/key techamatic@35.198.222.21
```
- `techamatic@35.198.222.21`: username + indirizzo IP PUBBLICO della VM GCP



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

