---
title: Modificare il filtro trasferimento file predefinito
TOCTitle: Modificare il filtro trasferimento file predefinito
ms:assetid: 791774a2-0bb6-4b5b-aeb0-ff69abb170f4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521017(v=OCS.15)
ms:contentKeyID: 49301053
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare il filtro trasferimento file predefinito

 

_**Ultima modifica dell'argomento:** 2012-11-01_

In Lync Server 2013 è disponibile un filtro trasferimento file globale che consente di bloccare tipi specifici di file durante le attività correlate ai file seguenti all'interno della distribuzione di Lync Server 2013:

  - Richieste di trasferimento file durante conversazioni di messaggistica istantanea

  - Caricamenti e download di file tramite la caratteristica relativa agli stampati nel client Office Live Meeting 2007

  - Riproduzione multimediale durante le conferenze

A seconda dei tipi di file che si desidera bloccare o consentire, è possibile utilizzare Pannello di controllo di Lync Server per modificare il filtro globale. Per informazioni dettagliate sui filtri trasferimento file, vedere [Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md).

## Per modificare il filtro trasferimento file predefinito

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Messaggistica istantanea e presenza** e quindi su **Filtro file**.

4.  Nella pagina **Filtro file** fare doppio clic sul filtro **Globale**.

5.  In **Modifica filtro file** selezionare la casella di controllo **Abilita filtro file**.

6.  Nella casella di riepilogo a discesa **Trasferimento di file** fare clic su **Blocca tutto** o su **Blocca tipi di file specifici**.

7.  Se si è selezionato **Blocca tutto**, ignorare il passaggio 9.

8.  Se si è selezionato **Blocca tipi di file specifici**, eseguire le operazioni seguenti:
    
    1.  Fare clic su **Seleziona** per modificare l'elenco predefinito delle estensioni di file che si desidera bloccare.
    
    2.  In **Seleziona estensioni di file** selezionare i tipi di file che si desidera bloccare o consentire aggiungendone o rimuovendone le estensioni nelle categorie in **Estensioni di file**.
    
    3.  Se un'estensione di file che si desidera bloccare non è visualizzata, digitarla nella casella di testo in **Aggiungi estensioni di file all'elenco** e quindi fare clic su **Aggiungi**.
    
    4.  Fare clic su **OK**.

9.  Fare clic su **Commit**.

## Vedere anche

#### Attività

[Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md)  
[Creare un nuovo filtro trasferimento file per un sito specifico](lync-server-2013-create-a-new-file-transfer-filter-for-a-specific-site.md)  
[Creare un nuovo filtro URL per gestire i collegamenti ipertestuali nelle conversazioni istantanee](lync-server-2013-create-a-new-url-filter-to-handle-hyperlinks-in-im-conversations.md)  

#### Concetti

[Modificare il filtro URL predefinito](lync-server-2013-modify-the-default-url-filter.md)

