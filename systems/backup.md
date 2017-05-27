# Dal VUA

## Rete Domestica
Partiamo dalla rete domestica:
* Tutte le macchine fanno un backup su un __NAS (synology)__ in rete via __rsync+ssh__, con __duplicity__. 
* Il nas poi sincronizza il backup su un __disco usb__ e su __amazon cloud drive__, entrambi crittografati. 
* Il disco usb viene "spento" spegnendo con il sistema domotico la presa a cui e' attaccato il suo alimentatore esterno, e il cavetto usato e' fatto in maniera da non portargli alimentazione.
* in casa facendo il mio NAS da ponte, semplicemente i vari duplicity, che hanno solo la chiave pubblica per gpg e non quella privata, ho utilizzato il metodo che piu' hanno suggerito: le macchine possono solo scrivere e non cancellare. Sul nas poi faccio il resto e distribuisco i backup.

## Rete On Line
La rete online e' composta da un cluster ganeti sulla quale girano una 50ina di macchine virtuali. 
* I dischi virtuali sono lvm+drbd, ma non e' possibile lavorare di lvm snapshot perche' sarebbe altamente inefficiente essendo poi tutti i dischi virtuali crittografati in FDE all'interno della macchina virtuale stessa.Di conseguenza il backup in questo caso viene fatto su __hubic__ e su __amazon cloud drive__.
sull'ambiente con ganeti, invece, non ho una macchina a fare da ponte per lo storage per il semplice fatto che non avevo sufficiente storage per farla e nessuna intenzione di prendere una macchina in piu' appositamente, quindi semplicemente redirigo tutte le connessioni verso verso il cloud a un proxy, un demoncino in python, che accetta upload dalle macchine via scp ( e quindi i vari duplicity si connettono over scp:// ) e poi via fuse stora i backup sui cloud.
Il demone in questione si occupa anche di vietare le richieste di delete e simili.
Non e' ovviamente una soluzione perfetta e sicuramente ha i suoi difetti, per alcuni versi e' in linea con i suggerimenti ricevuti anche qui.
Volevo solo capire se stavo facendo troppo casino o la mia soluzione poteva andare bene, e direi che va bene.

## Backup
- Dropbox, con 2FA, file critici, tutto syncato su tutti i miei PC.
- Nextcloud, abbastanza blindato ma non mi sento ancora sicuro a metterci i file critici, ho una parte che synco su tutti i PC e una "Archive" non sincronizzata in locale in cui da client web sposto la roba che so non mi servira' piu'. Non e' piu' di tanto necessaria.
- Google Drive, per foto e documenti Google.
Queste tre mi coprono lo scenario post apocalittico, e tutte le cose importanti sono qui dentro. Ho pero' altri due requisiti, che non so come coprire:
- Files che ehm, non si possono caricare su internet, almeno non cosi' come sono. Tipo i 50 GB di "Ai Confini della Realta'", foto delle ex, altri download vari.
- Torrent e quella roba li.
- Video GoPro.
- ISO che non voglio perdere.
- Backup storici che non mi serviranno mai piu', ma che non voglio perdere.
Queste robe sono al momento in giro in modo misto sullo storage locale dei Macbook, o su un disco USB. 250 GB totali ad oggi ma perche' ho sempre avuto problemi di spazio, quindi potrebbero crescere. Devo riordinarle, toglierle dai mac, e togliermi il problema del filesystem (visto che non esiste FS che sia ben gestito da OSX, Linux e Windows).
Le soluzioni variano dal NAS in casa (peraltro ho appena comprato un WD MyCloud in offerta) a infilare tutto su Backblaze B2 / Amazon S3. La prima mi lascia aperto il problema del backup, la seconda mi lascia il problema del dover scaricare / caricare ogni volta che voglio un file.
Voi come fate? Avete consigli?
----
serverino rack con raid6 6x3TB, zfs, backup su ACD unlimited. onestamente per quel volume di roba, io andrei su storage box su hetzner, te la cavi con pochi euro al mese.
io per un periodo ho avuto solo hetzner, per motivi di costo limitavo il backup ai 500GB di "core". poi quando ho scoperto ACD ho mantenuto il core su hetzner e full su ACD. dopo svariati mesi di verifiche costanti, in cui ho potuto valutare l'affidabilità di ACD, ho dismesso hetzner.
mega.nz era una delle opzioni iniziali, ma segata per il rischio sparizione (kim mi deve ancora due anni di account premium mega upload che avevo appena pagato)
Casa A. Proliant g5 riattato a storage in raid 1. Casa B. Rsync notturno in vpn su linuxino handcrafted mdm raid 10.
Bau.
per nextcloud/owncloud io uso un metodo semplice per sentirmi sicuro: la macchina la uso solo per scambiare file crittografati che poi lato client vengono montati con encfs o similari, nessun file e' in chiaro accedibile dall'owncloud in se' se non robe molto blande.
 Soluzione dettata da pigrizia + ambiente casalingo multios ( io vari winzozz+moglie osx + ps3 + TV player Android): NAS 1tb raid1 con media player visto da ps3 e tvplayer, fs principale esportato via cifs e NFS più un fs a parte per il p2p solo locale. Ha client torrent più SSH.
Da uno dei PC monto lo share con le foto/video "da conservare" con un link simbolico (su Windows) che lo fa sembrare locale e da lì faccio backup col client zoolz su zoolz cold storage (2tb lifetime pagato 50€).
Ho un disco esterno collegato al NAS solo alla bisogna dove sposto le foto dei viaggi e della bimba per ulteriore sicurezza (visto che uso winzozz) da vari *Locker.
Giuro che per tutto l'ambaradan ho speso pochissimo e per me basta e avanxa
## veeam
## Crashplan
## Carbonite
## Backblaze

## Chiavi GPG
Smaneggiando con alcuni keyring diversi dal mio personale in cui dovevo aggiungere e togliere alcune chiavi, grazie alla chiarezza di gpg, ho per errore rimosso la mia chiave privata dal mio keyring.
Nessun problema, ovviamente ho il mio bel backup e quindi non la ho certamente persa.
Faccio quindi subito un bel gpg --import miachiave.privata.asc, e la importa correttamente.
La edito e gli do il trust. A gpg -K la vedo correttamente, sembra tutto ok.
Non ci sono altre chiavi private.
Se tento di firmare qualcosa:
gpg: signing failed: No secret key
gpg: [stdin]: clearsign failed: No secret key

 fde + yubico
 AES256 [edit].
 FileVault con nuke della password on sleep sui portatili, FileVault e basta sul fisso. Password per modificare la sequenza di boot, yubikey come 2FA per il login e per L'unlock dello screensaver.
 Io tengo un'unica partizione cifrata, che monto solo all'occorrenza e dove metto solo cose di vitale importanza ma di accesso raro. In tal modo se qualcuno ha accesso al mio portatile per un tempo non lunghissimo, deve beccare uno dei momenti in cui la partizione e' montata, altrimenti nisba. Cifrare tutto e non smontare e' un approccio utile per altri tipi di attacchi, in particolare nel caso in cui il portatile venga smarrito mentre e' spento.
 
https://www.dyne.org/software/tomb/

Io ho *tutto* in fde, e quando dico tutto intendo tutto, ws, portatile, cellulare, media server etcetc. Non pesa particolarmente, ma in generale me ne fotto della velocità di accesso, la reliability è per me molto più importante, e dove ho davvero bisogno di velocità vado di tmpfs, eventualmente come overlay cache.
Tutto in FDE. Con le CPU di oggi e AES-NI o equivalenti oramai è praticamente a costo zero.
FDE con SecureBoot e chiavi custom sul portatile, a casa non ho (ancora) migrato tutto su FDE.
ma io so che è sbagliato fare un ecryptfs ad esempio della home se sotto hai la FDE
