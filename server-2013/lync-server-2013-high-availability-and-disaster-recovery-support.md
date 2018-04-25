---
title: 'Lync Server 2013: Supporto per la disponibilità elevata e il ripristino di emergenza'
TOCTitle: Supporto per la disponibilità elevata e il ripristino di emergenza
ms:assetid: 47e77e85-c7c3-4ade-8db7-a34c71aeafd7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204866(v=OCS.15)
ms:contentKeyID: 49300421
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-25_

Lync Server 2013 offre disponibilità elevata grazie alla ridondanza dei server ottenuta tramite i pool. Se si verifica un errore in un determinato ruolo del server, gli altri server del pool che eseguono lo stesso ruolo se ne assumono il carico. Ciò si applica ai Front End Server, ai server perimetrali, ai Mediation Server e ai server Director. Per informazioni dettagliate sui ruoli dei server, vedere [Ruoli del server in Lync Server 2013](lync-server-2013-server-roles.md).

Lync Server 2013 offre anche funzionalità di ripristino di emergenza tramite l'abilitazione dell'abbinamento di pool. Se si distribuisce questa topologia, vengono designate coppie di pool Front End, in cui ogni pool si trova in un data center distinto e in un'area geografica separata. Se uno dei pool o dei siti diventa inattivo, è possibile reindirizzare gli utenti che vi appartengono all'altro pool della coppia, provocando in questo modo un'interruzione minima del servizio.

Lync Server 2013 supporta la funzionalità di disponibilità elevata anche per i server back-end. Questa è una topologia facoltativa in cui vengono distribuiti due server back-end per un pool Front End e viene impostato il mirroring sincrono di SQL Server per tutti i database di Lync in esecuzione nei server back-end.

Per informazioni dettagliate sull'abbinamento di pool e sul mirroring dei server back-end, vedere [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md).

## Vedere anche

#### Concetti

[Ruoli del server in Lync Server 2013](lync-server-2013-server-roles.md)  
[Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)

