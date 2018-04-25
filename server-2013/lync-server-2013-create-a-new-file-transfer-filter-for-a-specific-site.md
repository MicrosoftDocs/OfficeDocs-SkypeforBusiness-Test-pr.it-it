---
title: Creare un nuovo filtro trasferimento file per un sito specifico
TOCTitle: Creare un nuovo filtro trasferimento file per un sito specifico
ms:assetid: d0006487-5217-491c-b730-e6c551cd9825
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182589(v=OCS.15)
ms:contentKeyID: 49302036
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un nuovo filtro trasferimento file per un sito specifico

 

_**Ultima modifica dell'argomento:** 2012-10-18_

Oltre a modificare il filtro di trasferimento di file globale, è possibile configurare filtri di trasferimento di file personalizzati per siti specifici nell'ambito della distribuzione di Lync Server 2013. Per informazioni dettagliate sul filtro di trasferimento di file, vedere [Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md).

## Per creare un filtro di trasferimento di file per un sito specifico

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Messaggistica istantanea e presenza** e quindi su **Filtro file**.

4.  Nella pagina **Filtro file** fare clic su **Nuovo**.

5.  Nella finestra di dialogo **Seleziona un sito** fare clic sul sito per il quale si desidera creare il filtro di trasferimento file e quindi fare clic su **OK**.

6.  In **Crea nuovo filtro file** fare clic sulla casella di controllo **Abilita filtro file**.

7.  Nella casella di riepilogo a discesa **Trasferimento di file** fare clic su **Blocca tutto** o su **Blocca tipi di file specifici**.

8.  Se si è fatto clic su **Blocca tutto**, andare al passaggio 10.

9.  Se si è fatto clic su **Blocca tipi di file specifici**, eseguire le operazioni seguenti:
    
    1.  Fare clic su **Seleziona** per modificare l'elenco predefinito di estensioni di file da bloccare.
    
    2.  Nella finestra di dialogo **Seleziona estensioni di file** selezionare i tipi di file da bloccare o consentire aggiungendone o rimuovendone le estensioni dalle categorie in **Estensioni di file**.
    
    3.  Se l'estensione di un tipo di file da bloccare non viene visualizzata, digitarla nella casella di testo in **Aggiungi estensioni di file all'elenco** e quindi fare clic su **Aggiungi**.
    
    4.  Fare clic su **OK**.

10. Fare clic su **Commit**.

## Vedere anche

#### Attività

[Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013](lync-server-2013-configuring-file-transfer-and-url-filtering-for-instant-messaging-im.md)  
[Creare un nuovo filtro URL per gestire i collegamenti ipertestuali nelle conversazioni istantanee](lync-server-2013-create-a-new-url-filter-to-handle-hyperlinks-in-im-conversations.md)  
[Modificare il filtro trasferimento file predefinito](lync-server-2013-modify-the-default-file-transfer-filter.md)  

#### Concetti

[Modificare il filtro URL predefinito](lync-server-2013-modify-the-default-url-filter.md)

