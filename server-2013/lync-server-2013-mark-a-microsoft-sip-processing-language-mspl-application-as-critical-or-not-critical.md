---
title: "Lync Server 2013: Applicaz. MSPL (MS SIP Processing Language) critica o non critica"
TOCTitle: "Lync Server 2013: Applicaz. MSPL (MS SIP Processing Language) critica o non critica"
ms:assetid: df68fdc6-b7e6-4f07-acdc-0cd4c2c888a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182598(v=OCS.15)
ms:contentKeyID: 49302201
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Contrassegnare un'applicazione MSPL (Microsoft SIP Processing Language) come critica o non critica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Le applicazioni server MSPL (Microsoft SIP Processing Language) sono applicazioni script in cui viene utilizzato il linguaggio di script MSPL anziché l'API Microsoft Lync 2010. Alcune applicazioni server MSPL sono specificate come di importanza critica. Se è di importanza critica, uno script deve essere avviato all'avvio del sistema per consentire l'avvio di Lync Server 2013. Se lo script ha esito negativo durante l'esecuzione di Lync Server, il server non si arresta, ma interrompe l'invio di traffico allo script e scrive errori nel registro eventi.

È possibile utilizzare Pannello di controllo di Lync Server per contrassegnare le applicazioni server MSPL come critiche o per rimuovere il contrassegno.

Non tutti gli script supportano questa opzione. Ad esempio, lo script DefaultRouting è contrassegnato come critico e non è possibile modificare questa opzione per DefaultRouting.

## Per contrassegnare un'applicazione server MSPL come critica o rimuovere il contrassegno

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Topologia** e quindi su **Applicazione server**.

4.  Nella pagina **Applicazione server** fare clic sull'intestazione di una colonna per cambiare l'ordine delle applicazioni, se necessario, e quindi fare clic sull'applicazione server da modificare.

5.  Fare clic su **Azione**.

6.  Fare clic su **Seleziona come critica** o su **Deseleziona come critica** (ossia, se lo script supporta questa opzione).

## Vedere anche

#### Attività

[Abilitare o disabilitare un'applicazione server MSPL (Microsoft SIP Processing Language)](lync-server-2013-enable-or-disable-a-microsoft-sip-processing-language-mspl-server-application.md)  

#### Concetti

[Visualizzare le applicazioni server MSPL (Microsoft SIP Processing Language) in Lync Server 2013](lync-server-2013-view-microsoft-sip-processing-language-mspl-server-applications.md)  

#### Ulteriori risorse

[Gestione della topologia di Lync Server 2013](lync-server-2013-managing-the-lync-server-topology.md)

