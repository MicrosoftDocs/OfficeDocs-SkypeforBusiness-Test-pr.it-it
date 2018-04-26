---
title: 'Lync Server 2013: Riduzione della messaggistica istantanea indesiderata'
TOCTitle: Riduzione della messaggistica istantanea indesiderata per Lync Server 2013
ms:assetid: d2998708-e699-4465-a918-e1d9ea4c49c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn518335(v=OCS.15)
ms:contentKeyID: 60490919
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riduzione della messaggistica istantanea indesiderata per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-05_

Il filtro di protezione per messaggi istantanei consente di proteggere la distribuzione di Microsoft Lync Server 2013 dalla diffusione delle forme più comuni di virus con ripercussioni minime sull'esperienza utente. Il filtro di protezione per messaggi istantanei offre le funzionalità seguenti:

  - Filtro avanzato per gli URL

  - Filtro avanzato per il trasferimento di file

Usare il filtro di protezione per messaggi istantanei per configurare filtri per bloccare i messaggi istantanei indesiderati o potenzialmente pericolosi provenienti da endpoint sconosciuti esterni al firewall aziendale. È possibile configurare i filtri specificando i criteri da usare per determinare gli elementi da bloccare, ad esempio i messaggi istantanei contenenti collegamenti ipertestuali e file con estensioni specifiche.

Prima di distribuire il filtro di protezione per messaggi istantanei, è necessario acquisire familiarità con le modalità di applicazione delle opzioni di filtro quando i messaggi vengono instradati da un server Lync Server 2013 a un altro. Il modo in cui queste opzioni di filtro vengono applicate è coerente, indipendentemente dal fatto che i server si trovino in una singola organizzazione oppure oltre i confini dell'organizzazione. Tale coerenza riguarda il modo in cui i testi delle note e degli avvisi personalizzati vengono inseriti nei messaggi e inviati tra server.

L'opzione di filtro consigliata prevede di consentire i messaggi istantanei con collegamenti ipertestuali, ma richiede la disabilitazione del collegamento anteponendo un carattere di sottolineatura. Se si sceglie questa opzione, è possibile scrivere un avviso per gli utenti che viene visualizzato all'inizio di ogni messaggio istantaneo che contiene un collegamento ipertestuale.

Una seconda opzione di filtro permette di consentire i messaggi istantanei con collegamenti ipertestuali invariati. Se si sceglie questa opzione, è possibile (operazione consigliata) scrivere un avviso per gli utenti, che verrà inserito in ogni messaggio.

Una terza opzione prevede il blocco di tutti i messaggi istantanei che contengono collegamenti ipertestuali. Se si sceglie questa opzione, il server invia un avviso all'utente ed è necessario scrivere questo avviso.

