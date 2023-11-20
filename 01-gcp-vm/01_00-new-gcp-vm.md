# <a name="top"></a> Cap 1.1 - La macchina virtuale su google cloud

Il nostro ambiente di sviluppo e produzione lo mettiamo su una macchina virtuale (VM) su Google Cloud Platform (GCP) che raggiungeremo tramite ssh con Visual Studio Code (VS Code).

Prepariamo la macchina virtuale GCP VM (Google Cloud Project Virtual Machine) su cui installeremo Odoo.

> nota: ogni macchina virtuale GCP VM che viene creata è detta "**istanza**"



## Risorse esterne

- [How to Create a Virtual Machine (VM) on Google Cloud Platform (GCP)](https://www.youtube.com/watch?v=g2Il8cxNv18)
- []()


## Creiamo la GCP VM

Andiamo sulla Google Cloud Console (https://console.cloud.google.com/)
- Navigation Menu -> Products & solutions -> All products
- Management -> API & Services
  - Enabled APIs & services -> + ENABLE APIS AND SERVICES -> Search for: Compute Engine API
  - Enable -> Compute Engine API

- Navigation Menu -> Products & solutions -> All products
- Compute -> Compute Engine
- go to -> VM instances -> + CREATE INSTANCE

### Name
Name: odoo-server

### Region and Zone (are **permanent**)
Region: europe-west1 (Belgium)
Zone: europe-west1-b

### Machine configuration
- General purpose -> N2 (Balanced price & performance)
- -> n2-standard-2 (2 vCPU, 1 core, 8 GB memory) [$ 63.39/month]

### Boot disk
Qui scegliamo il nostro sistema operativo.
- CHANGE -> PUBLIC IMAGES
  - Operating System: Ubuntu
  - Version: Ubuntu 22.04 LTS (x86/64, amd64 jammy image built on 2023-10-30)
  - Boot disk type: Balanced persistent disk
  - Size (GB): 40

### Identity and API access
Le piattaforme Google lavorano tutte per API ed alla macchina virtuale viene, di default, assegnata una sua identità che è chiamata "service account". Questo è importante.

- Lasciamo il `service account` di default.
  ad esempio, Compute Engine default service account: 900749175873-compute@developer.gserviceaccount.com

- Access scopes: Allow default access

## Firewall
Flaggiamo tutte e tre le opzioni
- Allow HTTP traffic -> Sì
- Allow HTTPS traffic -> Sì
- Allow Load Balancer Health Checks -> Sì

## Advanced options
Le lasciamo di default.

> Nota: in Advanced options -> Management -> Automation c'è un campo dove si può inserire uno script che è eseguito tutte le volte che la VM fa boot-up. Questo può essere utile per spegnere la VM la notte e riaccenderla la mattina e lanciare una serie di programmi che ci servono.

Abbiamo configurato tutto.
Possiamo premere il pulsante CREATE per creare la nostra VM.
(in pochi minuti la macchina sarà creata e farà il boot)



## Lavoriamo con la VM
Una volta creata l'istanza della VM possiamo cliccare sul suo nome e vedere tutti i dettagli.

Per aprire il terminale basta fare clic sul bottone SSH. (vedremo più avanti come gestirla dal terminale del mac e come collegare VS Code per la programmazione)

Un altro link utile è Logs -> Serial port 1 (console)
Qui si vedono tutti i messaggi di log della VM che ci possono essere molto utili per eventuali debugs.



## Scheduling
Un'ultima cosa utile per gestire la nostra VM è creare una pianificazione di accensione e spegnimento della nostra VM per risparmiare sui costi.

- Navigation Menu -> Products & solutions -> All products
- Compute -> Compute Engine
- go to -> VM instances -> INSTANCE SCHEDULES -> CREATE SCHEDULE

Esempio:
- Name: daily-working-hours
- Region: europe-west1 (Belgium)
- Start time: 07:00
- Stop time: 22:00
- Time zone: Europe/Rome
- Frequency: Repeat daily

E poi attacchiamo questo profilo di pianificazione alla nostra istanza.
- Basta cliccare sul name "daily-working-hours" -> + ADD INSTANCES TO SCHEDULE
- e scegliere "odoo-server"

