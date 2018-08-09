---
title: "Compatibilità di LS 2013 con la resilienza di siti metropolitani di LS 2010"
TOCTitle: Resilienza di siti metropolitani di Lync Server 2010
ms:assetid: 18673ff6-b664-4a57-a89b-cbda8b129e6a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204715(v=OCS.15)
ms:contentKeyID: 49299817
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Resilienza di siti metropolitani di Lync Server 2010

 

_**Ultima modifica dell'argomento:** 2014-03-19_

In Lync Server 2013 la soluzione con resilienza di siti metropolitani di Lync Server 2010 non è supportata. Tale soluzione prevedeva l'estensione di un singolo pool Front End tra due data center situati nella stessa area metropolitana.

La soluzione con resilienza di siti metropolitani è stata progettata per il recupero in caso di perdita di un intero centro dati. Quando si estende il pool in due centri dati, in genere metà dei server front-end viene collocata in un centro dati e l'altra metà nel secondo centro dati. In caso di perdita di un intero centro dati, viene persa metà dei server front-end. Questo può causare problemi con il nuovo modello di sistema distribuito per i pool Front End in Lync Server 2013. Per ulteriori informazioni,vedere [Topologie e componenti per Front End Server, messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md).

