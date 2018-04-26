---
title: Abilitare o disabilitare un'applicazione server MSPL (Microsoft SIP Processing Language)
TOCTitle: Abilitare o disabilitare un'applicazione server MSPL (Microsoft SIP Processing Language)
ms:assetid: b20af38d-224a-4459-991d-0b7eabb3ca7c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182573(v=OCS.15)
ms:contentKeyID: 49301699
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare un'applicazione server MSPL (Microsoft SIP Processing Language)

 

_**Ultima modifica dell'argomento:** 2012-09-21_

È possibile utilizzare il Pannello di controllo di Lync Server per abilitare o disabilitare le applicazioni server MSPL (Microsoft SIP Processing Language) in esecuzione nell'ambiente Lync Server 2013. Si tratta di applicazioni script che utilizzano un linguaggio di script anziché l'API Microsoft Lync 2013 Preview.

Non tutti gli script possono essere abilitati o disabilitati. Ad esempio, lo script DefaultRouting è abilitato e tale opzione non può essere modificata.

## Per abilitare o disabilitare un'applicazione server MSPL

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Topologia** e quindi su **Applicazione server**.

4.  Nella pagina **Applicazione server** fare clic su un'intestazione di colonna per ordinare le applicazioni, se necessario, quindi fare clic sul'applicazione server che si desidera modificare.

5.  Fare clic su **Azione**.

6.  Fare clic su **Abilita applicazione** o **Disabilita applicazione**, se lo script supporta tale opzione.

## Vedere anche

#### Attività

[Contrassegnare un'applicazione MSPL (Microsoft SIP Processing Language) come critica o non critica](lync-server-2013-mark-a-microsoft-sip-processing-language-mspl-application-as-critical-or-not-critical.md)  

#### Concetti

[Visualizzare le applicazioni server MSPL (Microsoft SIP Processing Language) in Lync Server 2013](lync-server-2013-view-microsoft-sip-processing-language-mspl-server-applications.md)  

#### Ulteriori risorse

[Gestione della topologia di Lync Server 2013](lync-server-2013-managing-the-lync-server-topology.md)

