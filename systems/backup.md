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
