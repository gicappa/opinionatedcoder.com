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
