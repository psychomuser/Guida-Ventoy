# GUIDA VENTOY

## Indice

- Prova
- prova2
- prova3
- prova4

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

## Configurare l'avvio di software eseguibile (Es. Diskgenius)

- Alcuni software come clonezilla o gparted permettono di scaricare direttamente la iso, in tal caso basta inserire la iso su ventoy.
- Altri programmi come DiskGenius o AOMEI Partition invece, necessitano l'installazione del programma su windows/linux, e dalle opzioni del programma permettono di creare una pen drive bootabile WinPE. Ecco ad esempio come rendere eseguibile DiskGenius con Ventoy:

### ESEMPIO: Rendere DiskGenius avviabile da USB con Ventoy

- Rimuovere il supporto USB con Ventoy
- Inserire una pendrive in disuso (serve temporaneamente ma verrà formattata).
- Installare DiskGenius su Windows.
- Aprire il programma, in alto aprire il menù "Tools" e poi su "Create WinPE Bootable USB Drive of DiskGenius".
- Selezionare la pendrive in disuso precedentemente inserita e attendere l'installazione.
- Aprire il percorso della pen drive ed estrarre il file "boot.wim" nella cartella nascosta /boot
- Per comodità rinominare il file in DiskGenius.wim

- Scaricare il plugin wimboot da [questo link](https://github.com/ventoy/wimiso/releases)
- Inserire il file img nella cartella ventoy presente nel supporto usb.
- Inserire il file precedentemente estratto "Diskgenius.wim" ("boot.wim" rinominato) all'interno del supporto USB come se fosse una iso eseguibile.
