---
title: 'Lync Server 2013: Configurare la tabella dei numeri non assegnati'
TOCTitle: Configurare la tabella dei numeri non assegnati
ms:assetid: eaa01986-e92f-4328-acf6-4e46c4306a04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399053(v=OCS.15)
ms:contentKeyID: 49302379
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la tabella dei numeri non assegnati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-30_

In Lync Server 2013 è possibile specificare il comportamento per le chiamate in arrivo verso numeri di telefono validi per l'organizzazione ma non assegnati a un utente o un telefono. I chiamanti possono ascoltare un messaggio, essere instradati verso un'altra destinazione oppure entrambe le opzioni.

La configurazione della tabella dei numeri non assegnati dipende dal modo in cui si desidera utilizzarla. È possibile configurare la tabella con tutti gli interni validi dell'organizzazione, solo con gli interni non assegnati o con una combinazione di numeri di entrambi i tipi. La tabella dei numeri non assegnati può includere sia numeri assegnati che numeri non assegnati ma viene richiamata solo se un chiamante compone un numero non assegnato. Se nella tabella dei numeri non assegnati si inseriscono tutti gli interni validi, è possibile specificare l'azione da eseguire quando un utente lascia l'organizzazione, senza alcuna necessità di riconfigurare la tabella. Se nella tabella si inseriscono interni non assegnati, è possibile modificare l'azione da eseguire per numeri specifici. Se ad esempio si modifica l'interno del servizio di assistenza clienti, è possibile inserire il vecchio numero nella tabella e quindi assegnarlo a un annuncio in cui viene indicato il nuovo numero.

> [!IMPORTANT]  
> Prima di configurare la tabella di numeri non assegnati, è possibile che nel sistema siano già stati definiti annunci o che sia stato impostato un operatore automatico di Messaggistica unificata di Exchange.

> [!TIP]  
> Quando viene effettuata una chiamata a un numero non assegnato, in Lync Server viene eseguita una ricerca nella tabella dei numeri non assegnati, dall'alto verso il basso, e viene utilizzato il primo intervallo corrispondente. Pertanto, per l'ultimo intervallo della tabella è consigliabile specificare un'azione che si desidera venga eseguita come ultima risorsa.

## Argomenti della sezione

[Creare o modificare un intervallo di numeri non assegnati in Lync Server 2013](lync-server-2013-create-or-modify-an-unassigned-number-range.md) [Creare un annuncio in Lync Server 2013](lync-server-2013-create-an-announcement.md)

