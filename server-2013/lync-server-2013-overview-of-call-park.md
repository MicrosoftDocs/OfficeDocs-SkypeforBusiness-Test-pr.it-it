---
title: 'Lync Server 2013: Panoramica del parcheggio di chiamata'
TOCTitle: Panoramica del parcheggio di chiamata
ms:assetid: 985dc326-0aef-4308-b98b-c1d0069311e7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205124(v=OCS.15)
ms:contentKeyID: 49301404
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

L' Lync Server 2013applicazione Parcheggio di chiamata consente agli utenti di VoIP aziendale di effettuare una o più delle operazioni seguenti:

  - Mettere una chiamata in attesa e quindi recuperare la chiamata dallo stesso telefono o da uno diverso.

  - Mettere una chiamata in attesa per trasferirla a un altro reparto o a un'altra area generale, ad esempio a un reparto vendite o un magazzino in cui è presente un telefono di area comune.

  - Mettere una chiamata in attesa e mantenere libero per altre chiamate il telefono originale da cui si è risposto alla chiamata.

Quando un utente esegue il parcheggio di una chiamata, tramite Lync Server la chiamata viene trasferita a un numero temporaneo, denominato *codice orbit* , in cui resta in attesa fino a quando non viene recuperata o si verifica il timeout. Il codice orbit viene inviato da Lync Server all'utente che ha eseguito il parcheggio della chiamata. Per recuperare la chiamata parcheggiata, l'utente può comporre il codice orbit o fare clic sul collegamento o il pulsante del codice orbit nella finestra Conversazione.

L'utente che ha eseguito il parcheggio di una chiamata può indicare a qualcun altro di recuperare la chiamata utilizzando un meccanismo esterno, ad esempio un sistema di messaggistica istantanea o di paging, per comunicare il codice orbit a un altro utente. L'utente che ha eseguito il parcheggio della chiamata può lasciare aperta la finestra Conversazione per ricevere una notifica quando la chiamata viene recuperata.

Poiché gli intervalli di codici orbit sono intervalli univoci globali, è possibile recuperare chiamate da qualsiasi sito Lync Server o telefono PBX se il routing è configurato correttamente. Se nessuno recupera la chiamata entro una quantità di tempo configurabile, la chiamata viene nuovamente indirizzata alla persona che ne ha eseguito il parcheggio. Se tale persona non risponde alla richiamata, la chiamata viene trasferita a una destinazione di fallback, ad esempio a un operatore, se questa impostazione è configurata. È possibile configurare da uno a dieci il numero di volte per cui consentire una richiamata prima che la chiamata venga trasferita. Se nessuno risponde a una chiamata trasferita, questa viene disconnessa. Il codice orbit viene liberato quando la chiamata viene recuperata o disconnessa.

Quando si distribuisce il parcheggio di chiamata, è necessario riservare intervalli di numeri di interno (codici orbit) per il parcheggio delle chiamate. Tali numeri devono essere interni virtuali, ovvero numeri a cui non sono assegnati utenti o telefoni. È quindi necessario configurare la tabella dei codici orbit del parcheggio di chiamata con gli intervalli di interni e specificare il servizio applicazione che ospita l'applicazione Parcheggio di chiamata che gestisce ogni intervallo. Ogni pool Front End include una tabella di parcheggio di chiamata nel server di back-end corrispondente utilizzato per gestire le chiamate parcheggiate nel pool. L'elenco dei codici orbit è archiviato in archivio di gestione centrale e viene utilizzato per eseguire il routing dei codici orbit al pool di destinazione. Ogni pool Lync Server in cui viene distribuita e configurata l'applicazione Parcheggio di chiamata può essere associato a uno o più intervalli di codici orbit. Gli intervalli di codici orbit devono essere intervalli univoci globali in tutta la distribuzione di Lync Server.

È anche possibile configurare altre impostazioni di parcheggio chiamata, ad esempio la destinazione di reindirizzamento delle chiamate in caso di timeout e se usare la musica di attesa durante il parcheggio. È anche possibile specificare il file musicale da riprodurre mentre la chiamata è in attesa.


> [!NOTE]
> Per i file di musica di attesa personalizzati per il parcheggio chiamate non viene eseguito il backup nell'ambito del processo di ripristino di emergenza di Lync Server 2013 e verranno persi se i file caricati nel pool vengono danneggiati o cancellati. Mantenere sempre una copia di backup distinta dei file di musica di attesa personalizzati caricati per il parcheggio chiamate.



L'applicazione Parcheggio di chiamata è un componente di VoIP aziendale. Quando si distribuisce VoIP aziendale, l'applicazione Parcheggio di chiamata viene installata e attivata automaticamente. Prima di poter utilizzare l'applicazione Parcheggio di chiamata, tuttavia, l'amministratore di VoIP aziendale deve configurarla e abilitarla per gli utenti tramite criteri vocali.

