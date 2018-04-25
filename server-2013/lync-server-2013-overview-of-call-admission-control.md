---
title: 'Lync Server 2013: Panoramica del controllo di ammissione di chiamata'
TOCTitle: Panoramica del controllo di ammissione di chiamata
ms:assetid: 6fda0195-4c89-4dea-82e8-624f03e3d062
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398529(v=OCS.15)
ms:contentKeyID: 49300930
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del controllo di ammissione di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-22_

Le comunicazioni in tempo reale sono sensibili alla latenza e alla perdita di pacchetti che possono verificarsi in reti congestionate. Il controllo di ammissione di chiamata determina, in base alla larghezza di banda disponibile, se consentire di stabilire sessioni di comunicazione in tempo reale, ad esempio chiamate vocali o videochiamate. La progettazione del controllo di ammissione di chiamata in Lync Server 2013 offre quattro attributi principali:

  - È semplice da distribuire e gestire senza richiedere apparecchiature aggiuntive, ad esempio router configurati in modo speciale.

  - Consente di risolvere casi critici di utilizzo delle comunicazioni unificate, ad esempio relativi a utenti mobili e a più punti di presenza. I criteri di controllo di ammissione di chiamata vengono applicati in base alla posizione dell'endpoint e non a quella in cui risiede l'utente.

  - Oltre alle chiamate vocali, può essere applicato ad altro traffico, ad esempio alle videochiamate e alle sessioni di conferenza audio/video.

  - Offre la flessibilità necessaria per consentire la rappresentazione di diversi tipi di topologie di rete. Per alcuni esempi, vedere [Componenti e topologie per il servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-components-and-topologies-for-cac.md).

Se una nuova sessione vocale o video supera i limiti di larghezza di banda impostati in un collegamento WAN, la sessione viene bloccata (solo per le chiamate telefoniche) o reinstradata alla rete PSTN.

Il controllo di ammissione di chiamata controlla solo il traffico audio e video in tempo reale, ma non il traffico di dati.

Gli amministratori definiscono i criteri di controllo di ammissione di chiamata, che vengono applicati dal servizio criteri larghezza di banda installato con ogni pool Front End. Le impostazioni del controllo di ammissione di chiamata vengono automaticamente propagate in Lync Server a tutti i Front End Server della rete.

Per le chiamate non riuscite a causa di criteri di controllo di ammissione di chiamata, l'ordine di precedenza per il rerouting della chiamata è il seguente:

1.  Internet

2.  PSTN

3.  Segreteria telefonica

Tramite la registrazione dettagli chiamata (CDR) vengono acquisite informazioni sulle chiamate reinstradate alla rete PSTN o alla segreteria telefonica. CDR non consente l'acquisizione di informazioni sulle chiamate reinstradate a Internet, perché Internet viene considerato un percorso alternativo anziché un'opzione secondaria.


> [!NOTE]
> L'archiviazione nella segreteria telefonica non viene negata a causa di vincoli di larghezza di banda.



Il servizio criteri di larghezza di banda genera due tipi di file di registro in formato con valori separati da virgole (CSV). Nel file di registro degli **errori di verifica** vengono acquisite informazioni quando vengono negate richieste di larghezza di banda. Nel file di registro dell' **utilizzo dei collegamenti** viene acquisita un'istantanea dell'utilizzo della larghezza di banda della topologia di rete e del collegamento WAN. Entrambi questi file di registro possono semplificare l'ottimizzazione dei criteri di controllo di ammissione di chiamata in base all'utilizzo.

## Considerazioni relative al controllo di ammissione di chiamata

L'amministratore sceglie di installare il servizio criteri di larghezza di banda sul primo pool configurato nel sito centrale. Poiché c'è un unico sito centrale per area di rete, c'è un solo servizio criteri di larghezza di banda che gestisce i criteri di larghezza di banda per quella regione, i siti correlati e i collegamenti a questi. Il servizio criteri di larghezza di banda è eseguito come parte del Front End Server, e pertanto nel pool è integrato un elevato livello disponibilità. Il servizio criteri di larghezza di banda nel Front End Server è sincronizzato ogni 15 secondi. Se il pool Front End non è in funzione, i criteri del Controllo di ammissione di chiamata non sono più applicati fino a che il pool Front End, e di conseguenza il servizio criteri di larghezza di banda, entrano nuovamente in funzione. Ciò include tutte le chiamate effettuate durante il periodo di inattività del servizio criteri di larghezza di banda, e potrebbe causare una richiesta eccessiva di larghezza di banda per i collegamenti durante questo periodo

Il servizio criteri di larghezza offre elevata disponibilità all'interno di un pool Front End, ma non garantisce la ridondanza all'interno del pool Front End. Il servizio criteri di larghezza non è in grado di garantire il failover da un pool Front End a un altro. Dopo che il servizio sul pool Front End viene ripristinato, anche il servizio criteri di larghezza riprende la verifica dei criteri.

## Considerazioni sulla rete

Benché la limitazione della larghezza di banda per traffico audio e video venga applicata dal servizio criteri larghezza di banda in Lync Server 2013, non viene applicata nel router di rete (livelli 2 e 3). Il controllo di ammissione di chiamata di Lync Server 2010 impedisce a un'applicazione di dati, ad esempio, di utilizzare l'intera larghezza di banda di rete in un collegamento WAN, inclusa la larghezza di banda riservata al traffico audio e video tramite i criteri di controllo di ammissione di chiamata. Per proteggere la larghezza di banda necessaria nella rete, è possibile distribuire un protocollo Qualità del servizio (QoS), ad esempio DiffServ (Differentiated Services). Una procedura consigliata consiste pertanto nel coordinare i criteri di larghezza di banda del controllo di ammissione di chiamata di definiti con qualsiasi impostazione QoS che si intende distribuire.

## Percorsi di contenuti multimediali e segnali su VPN

Se l'organizzazione supporta contenuto multimediale tramite VPN, verificare che il flusso multimediale e il flusso dei segnali attraversino la rete VPN o che venga eseguito il routing di entrambi tramite internet. Per impostazione predefinita, i flussi multimediali e dei segnali passano attraverso il tunnel VPN.

## Controllo di ammissione di chiamata di utenti esterni

Il controllo di ammissione di chiamata non viene applicato per utenti remoti nei casi in cui il flusso del traffico di rete viene eseguito tramite Internet. Poiché il traffico multimediale attraversa Internet, e non viene gestito tramite Lync Server, non è possibile applicare il controllo di ammissione di chiamata. Tali controlli verranno tuttavia eseguiti sulla parte della chiamata il cui flusso attraversa la rete aziendale.

## Controllo di ammissione di chiamata di connessioni PSTN

È possibile applicare il controllo di ammissione di chiamata in Mediation Server sia che il server sia connesso a un sistema IP/PBX, a un gateway PSTN o a un trunk SIP. Poiché Mediation Server è un agente utente back-to-back (B2BUA), termina il contenuto multimediale. Il server include inoltre due lati di connessione: un lato connesso a Lync Server e un lato gateway, connesso a gateway PSTN, sistemi IP/PBX o trunk SIP. Per informazioni dettagliate sulle connessioni PSTN, vedere [Pianificazione per la connettività PSTN in Lync Server 2013](lync-server-2013-planning-for-pstn-connectivity.md).

È possibile applicare il controllo di ammissione di chiamata in entrambi i lati di Mediation Server a condizione che non sia abilitato il bypass multimediale. Se il bypass multimediale è abilitato, il traffico multimediale non attraversa Mediation Server, ma passa direttamente tra il client di Lync e il gateway. In questo caso, il controllo di ammissione di chiamata non è necessario. Per informazioni dettagliate, vedere [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md).

Nella figura seguente viene illustrata l'applicazione di controllo di ammissione di chiamata in connessioni PSTN con o senza il bypass multimediale abilitato.

**Applicazione del controllo di ammissione di chiamata in connessioni alla rete PSTN**

![Applicazione del controllo di ammissione di chiamata vocale con bypass multimediale sulle connessioni](images/Gg398529.4d66d529-0912-4de1-abec-266f54272eb3(OCS.15).jpg "Applicazione del controllo di ammissione di chiamata vocale con bypass multimediale sulle connessioni")

## Compatibilità del controllo di ammissione di chiamata con le versioni precedenti di Office Communications Server

È possibile abilitare il controllo di ammissione di chiamata solo in endpoint abilitati per Lync Server 2010 e versioni successive.

Non è possibile abilitare il controllo di ammissione di chiamata in endpoint che eseguono Office Communicator 2007 R2 o versioni precedenti.

**Applicazione del controllo di ammissione di chiamata in versioni di Lync Server diverse**

![Diagramma di confronto tra le versioni per il controllo di ammissione di chiamata vocale](images/Gg398529.fdbfee7e-15fc-445b-949d-8d61e61ac350(OCS.15).jpg "Diagramma di confronto tra le versioni per il controllo di ammissione di chiamata vocale")

