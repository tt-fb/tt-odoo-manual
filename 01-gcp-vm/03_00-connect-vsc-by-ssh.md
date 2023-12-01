# <a name="top"></a> Cap 1.2 - Colleghiamo VS Code all GCP VM

Colleghiamo la nostra app Visual Studio Code alla macchina virtuale su google cloud platform.



## Risorse esterne

- [SSH into Remote VM with VS Code | Tunneling into any cloud | GCP Demo](https://www.youtube.com/watch?v=0Bjx3Ra8PRM)
  Qui parla di più su VS code

- [Using VS Code with GCP VMs](https://learn.canceridc.dev/cookbook/virtual-machines/using-vs-code-with-gcp-vms)
- [Use VSCode and Remote SSH extension to connect to Compute Engine on Google Cloud](https://medium.com/@ivanzhd/vscode-sftp-connection-to-compute-engine-on-google-cloud-platform-gcloud-9312797d56eb)



## Colleghiamo VS Code alla VM con SSH
- Apriamo Visual Studio Code 
- clicchiamo nella sezione delle estensioni (extensions)
- Verifichiamo che "Remote - SSH" sia installato.
  - Altrimenti lo installiamo mettendo nel campo di ricerca la voce "remote-ssh"
  - clicchiamo sull'icona
  - clicchiamo su "Install"

![Google Cloud Console](https://github.com/tt-fb/tt-odoo-manual/blob/main/01-gcp-vm/03_01-vsc-extension-remote_ssh.png)

- Click su "View" -> "Command Palette..." (oppure SHIFT + CMD + p)
- cerchiamo per "Remote-SSH: Open SSH Configuration file..." 
  - e scegliamo "/Users/FB/.ssh/config"
  - oppure avremmo potututo cercare per "Remote-SSH: Add new SSH Host..."



Se è la prima volta si aprirà un file tipo questo

```bash
Host alias
  HostName hostname
  User user
```

Se già hai connessioni sarà tipo questo

```bash
Host 192.168.64.7
  HostName 192.168.64.7
  User ubuntu

Host 192.168.64.3
  HostName 192.168.64.3
  User ubuntu
```

Aggiungiamo come nuovo Host la nostra GCP VM

```bash
Host server-odoo
  HostName 34.154.240.173
  User tt-fb
  IdentityFile ~/.ssh/fb-odoo-server-key
```

Salviamo il file e siamo pronti a collegarci perché la chiave pubblica l'abbiamo già inserita nella GCP VM nel capitolo precedente.



## Effettuiamo il collegamento

