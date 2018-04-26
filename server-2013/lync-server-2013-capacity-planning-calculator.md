---
title: Uso dello strumento per il calcolo della pianificazione della capacità di Lync Server 2013
TOCTitle: Uso dello strumento per il calcolo della pianificazione della capacità di Lync Server 2013
ms:assetid: e86c1f05-1393-408a-9549-6001572ec50d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362852(v=OCS.15)
ms:contentKeyID: 56269984
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uso dello strumento per il calcolo della pianificazione della capacità di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-21_

Lo strumento per il calcolo della pianificazione della capacità di Microsoft® Lync™ Server 2013, che può essere scaricato all'indirizzo <http://www.microsoft.com/en-us/download/details.aspx?id=36828>, consente di determinare i requisiti del server in base al numero di utenti e alle modalità di comunicazione abilitate nell'organizzazione. È sufficiente immettere il profilo dell'organizzazione perché lo strumento di calcolo fornisca valori consigliati utili per la pianificazione della topologia.

Tali valori si riferiscono alla sola pianificazione. Per fare in modo che il provisioning di Lync Server 2013 venga effettuato correttamente, è necessario eseguire una simulazione del carico effettivo. A tale scopo, usare lo strumento di [Stress and Performance Tool per Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=282724).

Dopo aver determinato il profilo utente e le modalità da abilitare per gli utenti, è possibile usare lo strumento di calcolo per pianificare il numero di server, la quantità di memoria e la larghezza di banda necessaria. Questa versione dello strumento di calcolo non fornisce indicazioni per i requisiti di I/O disco.

Questo strumento di calcolo si integra con [Microsoft Lync Server](http://go.microsoft.com/fwlink/?linkid=282725) e [Microsoft Lync Server](lync-server-2013-planning.md). È consigliabile usarlo dopo aver letto la guida e aver creato la topologia suggerita dallo strumento di pianificazione.

È possibile trarre i maggiori benefici dallo strumento di calcolo se si dispone di informazioni precise e dettagliate sul profilo utente specifico. Dati come la percentuale di utenti abilitati per VoIP, il numero medio di chiamate per utente per ora, la durata delle chiamate e la percentuale di utenti simultanei nelle conferenze possono ad esempio fare molta differenza per i requisiti del server. La precisione dei valori consigliati creati dallo strumento di calcolo dipende dall'accuratezza delle informazioni fornite.

## Uso dello strumento di calcolo della capacità

Lo strumento è un foglio di calcolo di Microsoft Excel®. Le celle di colore arancione sono per l'input dell'utente. Il foglio include valori predefiniti, ovvero 80.000 utenti in un pool con dodici server front-end, ma tali valori possono essere modificati in base alle esigenze dell'organizzazione.

Il modello di utilizzo include le sezioni seguenti. Per calcolare i requisiti relativi alla capacità, immettere i dati come indicato:

**Messaggistica istantanea e presenza**

  - In Number of Users digitare il numero di utenti che saranno connessi simultaneamente. Questo numero rappresenta in genere l'80% del numero totale degli utenti di cui è stato eseguito il provisioning. Nella maggior parte dei casi il 100% degli utenti simultanei verrà abilitato per la messaggistica istantanea e la presenza. Il valore predefinito è 80.000.

  - Il numero medio di contatti presente nell'elenco dei contatti indica il numero di contatti che verrà usato per convalidare i requisiti di sistema. Questo numero non può essere modificato.

**VoIP aziendale**

  - In Users enabled for Enterprise Voice digitare la percentuale di utenti abilitati per il VoIP aziendale. Il valore predefinito è 60%.

  - In Average number of calls per user per hour (peak) digitare il numero di chiamate all'ora a cui si prevede che l'utente medio parteciperà durante i periodi di picco del carico. Il valore predefinito è 4.

  - In Percentage of calls that use media bypass digitare la percentuale di chiamate eseguite dagli utenti che eseguirà il bypass di Mediation Server. Il valore predefinito è 65%.

  - In Percentage of voice users involved in UC-PSTN calls digitare la percentuale delle chiamate UC-PSTN dell'organizzazione. Il valore predefinito è 60%

  - In Percentage of voice users involved in UC-UC calls viene visualizzata la percentuale di utenti abilitati per il VoIP aziendale che verranno abilitati solo per le chiamate UC-PSTN. Questo numero viene calcolato in base al valore immesso in Percentage of voice users enabled for UC-PSTN calls.

**Servizi di conferenza**

  - In Percentage of users in concurrent conferences digitare la percentuale di utenti che parteciperanno alle conferenze simultaneamente. Il valore predefinito è 5%.

  - In Percentage of conferences with group IM only (no voice) digitare la percentuale di conferenze per cui verrà usata solo la messaggistica istantanea senza alcun componente audio. Il valore predefinito è 10%

  - In Percentage of users using dial-in conferencing digitare la percentuale di partecipanti simultanei che useranno la conferenza telefonica con accesso esterno. Il valore predefinito è 15%.

  - In Percentage of conferences using voice digitare la percentuale di conferenze per cui verrà usato un componente audio.
    
      - Se il 20% delle conferenze vocali includerà anche un componente video standard, selezionare la casella di controllo Including video (no Multi View).
    
      - Se il 20% delle conferenze includerà anche un componente video MultiView, selezionare la casella di controllo Including Multi View.
    
      - Se il 50% delle conferenze vocali includerà anche la condivisione dell'applicazione, selezionare la casella di controllo Including application sharing.
    
      - Se il 20% delle conferenze include caricamenti di dati, ad esempio presentazioni di Microsoft PowerPoint®, selezionare la casella di controllo Including web conferencing.

**Mobilità**

  - In Percentage of users enabled for Mobility digitare la percentuale di utenti per cui verrà abilitata la connessione a Lync Server mediante dispositivi mobili. Il valore predefinito è 40%.

Dopo che saranno state immesse tutte le informazioni necessarie, lo strumento di calcolo della capacità stimerà i requisiti. Nelle celle gialle verranno visualizzati i valori calcolati per i requisiti di CPU, memoria e larghezza di banda in base ai test eseguiti nei laboratori delle prestazioni di Lync Server 2013. I numeri forniti sono solo indicativi poiché non viene verificata e convalidata ogni singola variazione. Vengono calcolati i valori seguenti:

  - Front End CPU: percentuale di utilizzo di CPU se l'intero carico venisse gestito da un server front-end con le stesse specifiche di quello utilizzato durante il test eseguito da Microsoft.

  - Network in Mbps: requisiti della larghezza di banda espressi in megabit al secondo (Mbps) per il carico di lavoro corrispondente.

  - Memory in GB: quantità di memoria necessaria, espressa in gigabyte (GB), per il carico di lavoro corrispondente.

Nelle celle verdi vengono visualizzati i valori consigliati per il modello di utilizzo immesso.

  - Total Front End Servers: il numero di server fisici necessari è basato sui server dedicati che eseguono Lync Server 2013 con processore doppio hex-core a 2.260 megacicli.

  - Si noti che l'abilitazione dell'hyperthreading è consigliata in quanto consente di migliorare le prestazioni per i server che supportano l'audio e il video.

  - Edge Servers: numero di server perimetrali necessari considerando che il 30% di tutti gli utenti simultanei comunichino mediante server perimetrali. Questa percentuale non può essere modificata nello strumento di calcolo.

  - Archiving/Call Detail Recording/Quality of Experience services Store: numero di archivi necessario per le funzionalità di archiviazione o di monitoraggio, nel caso siano abilitate nell'organizzazione.

  - Back End Database Server Required (Pools Required): numero di server di database back-end necessari per il supporto del carico di lavoro selezionato.

Nella riga accanto a Total Front End Servers sono inoltre disponibili altre informazioni sul carico nei server e nella rete per tutti i carichi di lavoro pianificati.

  - Average CPU Load: utilizzo medio della CPU per ogni server front-end.

  - Network in Mbps: allocazione di larghezza di banda necessaria per il supporto del modello di utilizzo immesso.

  - Memory in GB: quantità di memoria, espressa in gigabyte, necessaria per ogni server front-end.

## Modifiche per i processori in uso

Tutte le cifre relative all'utilizzo della CPU presenti nel foglio di calcolo presuppongono che ogni server disponga di un processore doppio hex-core con 2,26 GHz, almeno 32 GB di memoria e almeno 8 unità disco rigido da 10.000-RPM con almeno 72 GB di spazio libero su disco.

Se i server in uso dispongono di processori diversi, è possibile modificare le cifre in base al proprio hardware.

