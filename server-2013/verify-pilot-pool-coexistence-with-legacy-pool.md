---
title: Verificare la coesistenza del pool pilota con il pool legacy
TOCTitle: Verificare la coesistenza del pool pilota con il pool legacy
ms:assetid: fe7e14bb-c7eb-4719-b154-009e99360520
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205420(v=OCS.15)
ms:contentKeyID: 49302584
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare la coesistenza del pool pilota con il pool legacy

 

_**Ultima modifica dell'argomento:** 2012-09-29_

Dopo aver distribuito il pool pilota, è necessario verificare la coesistenza dei due pool utilizzando gli strumenti di amministrazione per visualizzare le informazioni dei pool. Per i pool e i pool legacy di Lync Server 2013, utilizzare il Pannello di controllo di Lync Server 2013 e gli strumenti di Generatore di topologie.

## Verificare che i servizi di Lync Server 2013 siano stati avviati

1.  Dal Front End Server di Lync Server 2013 passare all'applet Strumenti di amministrazione\\Servizi.

2.  Verificare che i servizi seguenti siano in esecuzione nel Front End Server:

**Servizi di Lync Server 2013**

![Elenco di servizi di Lync Server avviati](images/JJ205420.cfff9385-6bf6-461c-982c-e727c9f20b70(OCS.15).png "Elenco di servizi di Lync Server avviati")

## Aprire il Pannello di controllo di Lync Server 2013

Dal Front End Server nella distribuzione di Lync Server 2013 aprire il Pannello di controllo di Lync Server 2013 e quindi selezionare il pool di Lync Server 2010. Ripetere la procedura per aprire il pool di Lync Server 2013.

**Aprire il Pannello di controllo di Lync Server 2013**

![Finestra di dialogo Seleziona URL](images/JJ205420.b1f8e650-9c3c-4563-a403-5069f198342f(OCS.15).png "Finestra di dialogo Seleziona URL")

> [!important]  
> In Lync Server 2013 aggiornare Silverlight a Silverlight versione 5 prima di utilizzare il Pannello di controllo di Lync Server.

Questa topologia ora include i ruoli server di Lync Server 2010 e Lync Server 2013.

**Pagina della topologia del Pannello di controllo di Lync Server 2013**

![Pannello di controllo di Lync Server - Pagina della topologia](images/JJ205420.4ed1cc7a-cb3e-42f6-82e2-6d4d71d19352(OCS.15).jpg "Pannello di controllo di Lync Server - Pagina della topologia")

## Non tentare di aprire la topologia in Generatore di topologie di Lync Server 2010

Se si tenta di aprire la topologia utilizzando Generatore di topologie di Lync Server 2010, verrà visualizzato l'errore seguente. È possibile visualizzare la topologia solo utilizzando Generatore di topologie di Lync Server 2013. È necessario utilizzare Generatore di topologie di Lync Server 2013 per creare i pool per Lync Server 2013 e Lync Server 2010.

**Messaggio di errore di Generatore di topologie di Lync Server 2010**

![Errore dello snap-in MMC nel Generatore di topologie di Lync Server](images/JJ205420.f6666343-c348-4d81-ae0e-6ba5a44e16c4(OCS.15).png "Errore dello snap-in MMC nel Generatore di topologie di Lync Server")

