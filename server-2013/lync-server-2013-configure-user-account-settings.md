---
title: 'Lync Server 2013: Configurare le impostazioni degli account utente'
TOCTitle: Configurare le impostazioni degli account utente
ms:assetid: b7c74ecc-b924-4efc-8a56-3a5f94a9ef13
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412896(v=OCS.15)
ms:contentKeyID: 49301751
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le impostazioni degli account utente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

Gli utenti connessi tramite chiamata in ingresso immettono il proprio numero di telefono o interno e un PIN per partecipare alle conferenze come utenti autenticati. Per l'autenticazione è necessario il valore **URI linea** di telefonia specificato negli account utente di Lync Server.

La procedura in questo argomento descrive come assegnare un **URI linea** a un singolo account utente. Se è necessario assegnare un **URI linea** per più account utente, è possibile creare uno script che utilizzi il cmdlet **Set-CsUser**. Per informazioni dettagliate sull'utilizzo di un script di esempio per assegnare un **URI linea** a più account utente, vedere il post relativo all'assegnazione degli URI di linea a più utenti all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=196945](http://go.microsoft.com/fwlink/p/?linkid=196945).

## Per configurare le impostazioni dell'account utente

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins o come membro del ruolo **Cs-UserAdministrator** o **CsAdministrator** .

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti** .

4.  Nel campo di ricerca digitare il nome dell'utente che si desidera configurare per le conferenze telefoniche con accesso esterno oppure fare clic su **Aggiungi filtro** per specificare i campi di ricerca e quindi fare clic su **Trova** .

5.  Fare doppio clic sul nome dell'utente per aprire la finestra di dialogo **Modifica utente Lync Server**.

6.  In **Telefonia** , nel campo **URI linea** digitare un numero di telefono normalizzato univoco, ad esempio tel:+14255550200).
    

    > [!NOTE]
    > È possibile specificare <STRONG>URI linea</STRONG> esclusivamente se l'opzione <STRONG>Telefonia</STRONG> è impostata su <STRONG>Solo da PC a PC</STRONG> , <STRONG>VoIP aziendale</STRONG> , <STRONG>Controllo delle chiamate remote</STRONG> o <STRONG>Solo controllo delle chiamate remote</STRONG> .



7.  Fare clic su **Commit** .

