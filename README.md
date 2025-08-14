# GUIDA VENTOY

## Indice

- [Installazione](#installazione)
- [Configurazione di script](#configurare-script-autounattendxml)
- [Configurazione Avvio di Software](#configurare-lavvio-di-software-eseguibili)
- [Configurare l'avvio di un sistema linux persistente](#configurare-lavvio-di-un-sistema-linux-persistente)

---

## Installazione

- Scaricare Ventoy dal [Sito Ufficiale](https://www.ventoy.net/en/download.html) e scompattare il file zip
- Aprire l'eseguibile "Ventoy2Disk.exe"
- Selezionare il supporto su cui installarlo e attendere la fine dell'installazione.
- L'installazione è completata, adesso è possibile inserire le iso dentro il supporto USB, è consigliato creare delle sottocartelle per organizzarsi meglio.

## Configurare Script autounattend.xml

- Creare una cartella specifica in cui inserire le iso windows, e trasferire la/le iso all'interno.
- Creare una cartella specifica per i file autounattend.xml, e un ulteriore sottocartella per ogni file XML da inserire, in modo tale da distinguerli. A quel punto trasferire i file autounattend.xml desiderati all'interno.
- Aprire l'eseguibile "VentoyPlugson.exe" e poi premere su start, si aprirà il browser
- Sulla sinistra andare nella sezione "Auto Install Plugin"
- Cliccare il tasto verde "Add"
- Scegliere [image] se si vuole associare il file XML a una singola immagine; [parent] Se invece si vuole associare a una cartella specifica e tutte le iso che contiene.
- Come da istruzioni, nel primo campo mettere il percorso della cartella (o della iso) che va associata al file
- Nel secondo campo invece inserire il percorso del file autounattend.xml, comprensivo del nome completo del file.
- A quel punto premere "OK"
- La configurazione è terminata, tornare su VentoyPlugson e cliccare "STOP"

## Configurare l'avvio di software eseguibili 

- Alcuni software come clonezilla o gparted permettono di scaricare direttamente la iso, in tal caso basta inserire la iso su ventoy.
- Altri programmi come DiskGenius o AOMEI Partition invece, necessitano l'installazione del programma su windows/linux, e dalle opzioni del programma permettono di creare una pen drive bootabile WinPE. Ecco ad esempio come rendere eseguibile DiskGenius con Ventoy:

### ESEMPIO: Rendere DiskGenius avviabile da USB con Ventoy

- Rimuovere il supporto USB con Ventoy
- Inserire una pendrive in disuso (serve temporaneamente ma verrà formattata).
- Installare DiskGenius su Windows.
- Aprire il programma, in alto aprire il menù "Tools" e poi su "Create WinPE Bootable USB Drive of DiskGenius".
- Selezionare la pendrive in disuso precedentemente inserita e attendere l'installazione.
- Aprire il percorso della pen drive ed estrarre il file "boot.wim" nella cartella nascosta /boot.
- Per comodità rinominare il file in DiskGenius.wim.
- Rimuovere la pen drive e rimettere il supporto USB con Ventoy.

- Scaricare il plugin wimboot da [questo link](https://github.com/ventoy/wimiso/releases)
- Inserire il file img scaricato nella cartella ventoy presente nel supporto usb.
- Inserire il file precedentemente estratto "Diskgenius.wim" ("boot.wim" rinominato) all'interno del supporto USB come se fosse una iso eseguibile qualunque.
- Adesso DiskGenius apparirà tra le opzioni di boot allo stesso modo delle altre iso.

## Configurare l'avvio di un sistema Linux Persistente

Con Ventoy è possibile configurare un sistema persistente di Linux, che mantiene tutte le modifiche effettuate all'interno come un normale sistema operativo.
Nella tabella presente in [questo link](https://www.ventoy.net/en/plugin_persistence.html), è possibile vedere quali sono le distro compatibili per questa procedura. 

**Note:**
- Non sono riuscito a far funzionare fedora, neanche inserendo il comando "selinux=0" dall'avvio di GRUB, come indicato nella tabella.
- Arch non utilizza una live iso, ho provato con Manjaro ma a quanto pare non è compatibile, non so con quale distro Arch si potrebbe fare.

Ecco ad esempio come creare una live iso persistente di Linux Mint (una delle distro linux che fa uso di una live iso):

### ESEMPIO: Inserire la iso di Linux Mint come immagine persistente

**FILE NECESSARI**
- Iso live di Linux Mint scaricabile a [questo link](https://linuxmint.com/download.php)
- Scaricare il file zip a [questo link](https://github.com/ventoy/backend/releases), contiene delle immagini pre-create di diverse dimensioni.
- Estrarre dallo zip il file .dat adatto alla build Linux Mint. Secondo la tabella presente a [questo link](https://www.ventoy.net/en/plugin_persistence.html), Mint necessita il file col nome "casper-rw". In questo caso io scarico il file "persistence_ext4_4GB_casper-rw.dat".
  - "EXT4" è il formato consigliato.
  - "casper-rw" è la dicitura corretta per Linux Mint secondo la tabella vista prima.
  - "4GB" indica che il sistema persistente che andremo ad avviare sarà grande 4GB.

**PROCEDIMENTO**
- Inserire la iso di Mint all'interno del Supporto USB Ventoy (dove si preferisce).
- Inserire il file "persistence_ext4_4GB_casper-rw.dat" nel Supporto USB Ventoy (per comodità l'ho inserito in una cartella chiamata "Mint Persistence").
- Aprire "VentoyPlugson" e cliccare su apri per aprire l'interfaccia web.
- Sulla sinistra cliccare su "Persistence plugin" e poi il tasto verde "Add".
- Si aprirà un popup, nel primo campo inserire il percorso della iso di Mint con incluso il nome del file iso.
- Nel secondo campo inserire il percorso del file .dat con incluso il nome del file.
- Cliccare su ok e la configurazione è terminata, tornare su VentoyPlugson e cliccare su "Stop" per chiudere.
- Adesso è possibile avviare la iso di Mint come immagine persistente, selezionando facoltativamente l'opzione persistence associata.
