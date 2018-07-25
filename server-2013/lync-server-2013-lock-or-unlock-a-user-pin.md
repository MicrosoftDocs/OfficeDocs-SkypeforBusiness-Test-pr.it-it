---
title: Bloccare o sbloccare il PIN di un utente
TOCTitle: Bloccare o sbloccare il PIN di un utente
ms:assetid: 3d293a8a-e182-4547-8b06-2603c3c77329
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688028(v=OCS.15)
ms:contentKeyID: 49887528
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Bloccare o sbloccare il PIN di un utente

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile bloccare o sbloccare il PIN di un utente dalla sezione **Utenti** del Pannello di controllo di Lync Server 2013.

## Per bloccare il PIN di un utente nel Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare per intero o solo la prima parte del nome visualizzato, del nome, del cognome, del nome account di Gestione account di protezione (SAM), dell'indirizzo SIP o dell'URI (Uniforma Re source Identifica) di linea dell'account utente e quindi fare clic su **Trova**.
    
      - Nel caso di una query salvata, fare clic sull'icona **Apri query**, utilizzare la finestra di dialogo **Apri** per recuperare la query (un file con estensione usf) e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare ulteriori criteri di ricerca per limitare il numero di risultati restituiti:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Immettere la proprietà utente digitandola o facendo clic sulla freccia dell'elenco a discesa per selezionarla.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore (ad esempio **Uguale a** o **Diverso da**).
    
    4.  A seconda della proprietà utente selezionata, immettere i criteri da utilizzare per filtrare i risultati della ricerca digitandoli o facendo clic sulla freccia dell'elenco a discesa.
        
        > [!tip]  
        > Per aggiungere ulteriori clausole di ricerca alla query, fare clic su <strong>Aggiungi filtro</strong>.    
    5.  Fare clic su **Trova**.
    
    6.  Fare clic sull'utente, su **Azione** e quindi su **Blocca PIN**.

## Per sbloccare il PIN di un utente nel Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare per intero o solo la prima parte del nome visualizzato, del nome, del cognome, del nome account di Gestione account di protezione (SAM), dell'indirizzo SIP o dell'URI (Uniforma Re source Identifica) di linea dell'account utente e quindi fare clic su **Trova**.
    
      - Nel caso di una query salvata, fare clic sull'icona **Apri query**, utilizzare la finestra di dialogo **Apri** per recuperare la query (un file con estensione usf) e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare ulteriori criteri di ricerca per limitare il numero di risultati restituiti:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Immettere la proprietà utente digitandola o facendo clic sulla freccia dell'elenco a discesa per selezionarla.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore (ad esempio **Uguale a** o **Diverso da**).
    
    4.  A seconda della proprietà utente selezionata, immettere i criteri da utilizzare per filtrare i risultati della ricerca digitandoli o facendo clic sulla freccia dell'elenco a discesa.
        
        > [!tip]  
        > Per aggiungere ulteriori clausole di ricerca alla query, fare clic su <strong>Aggiungi filtro</strong>.    
    5.  Fare clic su **Trova**.
    
    6.  Fare clic sull'utente, su **Azione** e quindi su **Sblocca PIN**.

## Per bloccare e sbloccare i PIN degli utenti utilizzando i cmdlet di Lync Server Management Shell

È anche possibile bloccare e sbloccare i PIN utente utilizzando Windows PowerShell e i cmdlet Lock-CsClientPin e Unlock-CsClientPin, che possono essere eseguiti da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per bloccare il PIN di un utente

  - Per bloccare il PIN di un utente, utilizzare il cmdlet Lock-CsClientPin. Ad esempio:
    
        Lock-CsClientPin -Identity "Ken Myer"

## Per sbloccare il PIN di un utente

  - Per sbloccare il PIN di un utente, utilizzare il cmdlet Unlock-CsClientPin. Ad esempio:
    
        Unlock-CsClientPin -Identity "Ken Myer"

Per ulteriori informazioni, vedere l'argomento della Guida relativo ai cmdlet [Lock-CsClientPin](https://docs.microsoft.com/en-us/powershell/module/skype/Lock-CsClientPin) e [Unlock-CsClientPin](https://docs.microsoft.com/en-us/powershell/module/skype/Unlock-CsClientPin).

