---
title: "Lync Server 2013: Crea nuovo filtro URL per gestire hyperlink nelle conversaz"
TOCTitle: "Lync Server 2013: Crea nuovo filtro URL per gestire hyperlink nelle conversaz"
ms:assetid: d0ee01e5-f039-4a34-ac9d-659fe4e9e879
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182590(v=OCS.15)
ms:contentKeyID: 49302044
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un nuovo filtro URL per gestire i collegamenti ipertestuali nelle conversazioni istantanee

 

_**Ultima modifica dell'argomento:** 2012-09-26_

Oltre a modificare il filtro URL globale, è possibile configurare filtri URL personalizzati per singoli siti nella distribuzione di Lync Server 2013. Per informazioni dettagliate sul filtro URL, vedere [Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md).

## Per creare un nuovo filtro URL

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Messaggistica istantanea e presenza** e quindi su **Filtro URL**.

4.  Nella pagina **Filtro URL** fare clic su **Nuovo**.

5.  In **Seleziona un sito** fare clic sul site per il quale si desidera creare il filtro URL e quindi su **OK**.

6.  Nella finestra di dialogo **Nuovo filtro URL** selezionare la casella di controllo **Abilita filtro URL** per abilitare il filtro URL per il sito.

7.  Per bloccare tutti gli URL attivi contenenti un file con un'estensione elencata in **Estensioni di file da bloccare** in **Modifica filtro file** selezionare la casella di controllo **Blocca URL con estensione di file**.

8.  Nella casella di riepilogo a discesa **Prefisso di collegamento ipertestuale** fare clic sull'opzione corrispondente alla modalità desiderata di gestione degli URL nelle conversazioni di messaggistica istantanea.
    
    La casella **Consenti messaggio** consente di visualizzare un messaggio di avviso per l'utente quando si inviano collegamenti ipertestuali il cui invio è consentito.

9.  Fare clic su **Commit**.

## Vedere anche

#### Attività

[Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md)  
[Creare un nuovo filtro trasferimento file per un sito specifico](lync-server-2013-create-a-new-file-transfer-filter-for-a-specific-site.md)  
[Modificare il filtro trasferimento file predefinito](lync-server-2013-modify-the-default-file-transfer-filter.md)  

#### Concetti

[Modificare il filtro URL predefinito](lync-server-2013-modify-the-default-url-filter.md)

