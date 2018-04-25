---
title: Visualizzare un elenco di applicazioni attendibili
TOCTitle: Visualizzare un elenco di applicazioni attendibili
ms:assetid: f09300b3-67cf-4e70-a51a-23d62479b913
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182604(v=OCS.15)
ms:contentKeyID: 49302427
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare un elenco di applicazioni attendibili

 

_**Ultima modifica dell'argomento:** 2012-09-21_

È possibile utilizzare Pannello di controllo di Lync Server 2013 per visualizzare un elenco di applicazioni attendibili distribuite nell'ambiente Lync Server 2013. Per applicazione attendibile si intende un'applicazione basata su Microsoft Unified Communications Managed API (UCMA) 3.0 Core SDK, considerato attendibile da Lync Server 2013. Questa relazione di trust è riepilogata nell'elenco seguente:

  - Lync Server non richiede l'autenticazione delle applicazioni attendibili.

  - Le applicazioni attendibili non vengono limitate da Lync Server per transazioni SIP, connessioni o chiamate VoIP (Voice over Internet Protocol) in uscita.

  - Le applicazioni attendibili possono rappresentare qualsiasi utente e possono partecipare a conferenze senza essere inserite negli elenchi dei partecipanti.

  - Le applicazioni attendibili sono resilienti e a disponibilità elevata.

In Pannello di controllo di Lync Server è possibile visualizzare il nome delle applicazioni, il pool in cui vengono eseguite e le porte che utilizzano.

## Per visualizzare un elenco di applicazioni attendibili

1.  Da un account utente assegnato al ruolo CsServerAdministrator, CsAdministrator, CsHelpDesk o CsViewOnlyAdministrator, accedere a un computer nella distribuzione interna. Per informazioni dettagliate sui ruoli amministrativi predefiniti disponibili in Lync Server 2013, vedere [Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013](lync-server-2013-planning-for-role-based-access-control.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Topologia** e quindi su **Applicazioni attendibili**.

4.  Nella pagina **Applicazione attendibile** fare clic sull'intestazione di una colonna per ordinare le applicazioni, se necessario.

## Vedere anche

#### Ulteriori risorse

[Gestione della topologia di Lync Server 2013](lync-server-2013-managing-the-lync-server-topology.md)

