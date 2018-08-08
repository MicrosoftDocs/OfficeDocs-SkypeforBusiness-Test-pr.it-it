---
title: "Lync Server 2013: Imposta PIN di conference call di un utente"
TOCTitle: Impostare il PIN di conferenza telefonica con accesso esterno di un utente
ms:assetid: 4252b5a5-4267-4513-b18e-0253a8d66f72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520985(v=OCS.15)
ms:contentKeyID: 49300351
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostare il PIN di conferenza telefonica con accesso esterno di un utente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-06-10_

Per partecipare a una conferenza telefonica con accesso esterno come utente autenticato, un utente di Lync Server 2013 con credenziali di Servizi di dominio Active Directory deve disporre di un PIN (Personal Identification Number). Se un utente dimentica il PIN della conferenza telefonica con accesso esterno o non ha impostato il PIN mediante Lync Server, sarà possibile impostare il PIN di tale utente dal Pannello di controllo di Lync Server. È possibile generare automaticamente il PIN o crearne uno manualmente.


> [!NOTE]
> Le caratteristiche specifiche del PIN, ad esempio la lunghezza minima, possono essere configurate come criterio. Oltre al criterio globale, è possibile configurare un criterio PIN per singoli siti o utenti. Per informazioni dettagliate sulla configurazione di un criterio PIN, vedere <A href="lync-server-2013-configure-dial-in-conferencing-personal-identification-number-pin-rules.md">Configurare regole per il PIN della conferenza telefonica con accesso esterno in Lync Server 2013</A>.



## Per impostare il PIN di un utente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti** .

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare interamente o la parte iniziale di nome visualizzato, nome, cognome, nome account SAM (Security Accounts Manager), indirizzo SIP o URI (Uniform Resource Identifier) dell'account utente desiderato e quindi fare clic su **Trova** .
    
      - Se è presente una query salvata, fare clic sull'icona **Apri query** , utilizzare la finestra di dialogo **Apri** per recuperare la query (file con estensione usf) e quindi fare clic su **Trova** .

5.  (Facoltativo) Specificare criteri di ricerca aggiuntivi per ridurre i risultati:
    
    1.  Fare clic su **Aggiungi filtro** .
    
    2.  Immettere la proprietà utente digitandola o facendo clic sulla freccia nell'elenco a discesa e selezionando la proprietà.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore (ad esempio **Uguale a** o **Non uguale a** ).
    
    4.  A seconda della proprietà utente selezionata, immettere i criteri che si desidera utilizzare per filtrare i risultati della ricerca digitandoli oppure facendo clic sulla freccia nell'elenco a discesa.
        
        > [!TIP]  
        > Per aggiungere ulteriori clausole di ricerca alla query, fare clic su <strong>Aggiungi filtro</strong> .    
    5.  Fare clic su **Trova** .
    

    > [!NOTE]
    > Se il PIN è bloccato, è necessario sbloccarlo per poterlo impostare. Per sbloccare il PIN, fare clic sull'utente, su <STRONG>Azione</STRONG> e quindi su <STRONG>Sblocca PIN</STRONG> .



6.  Fare clic su un utente nei risultati della ricerca, su **Azione** e quindi su **Imposta PIN** .

7.  Nella finestra di dialogo **Imposta PIN** eseguire una delle operazioni seguenti:
    
      - Per consentire a Lync Server 2013 di generare il PIN dell'utente, selezionare **Genera automaticamente un PIN valido** (impostazione predefinita).
    
      - Per creare un PIN personalizzato, fare clic su **Immetti manualmente un PIN specifico** , fare clic sulla casella di testo e quindi digitare un PIN che soddisfi i requisiti PIN specificati nelle impostazioni del criterio PIN.

8.  Fare clic su **OK** .

9.  In **Imposta PIN** eseguire una delle operazioni seguenti:
    
      - Selezionare la casella di controllo **Mostra PIN** per visualizzare il PIN e quindi copiare il PIN e comunicarlo all'utente utilizzando il metodo preferito dell'organizzazione.
    
      - Fare clic su **Apri applicazione di posta elettronica per inviare il nuovo PIN all'utente** per inviare il PIN per posta elettronica. Se si utilizza Microsoft Office Outlook come client di posta elettronica, il PIN verrà copiato automaticamente in un nuovo messaggio di posta elettronica. Se invece si utilizza un altro client di posta elettronica, selezionare la casella di controllo **Mostra PIN** per visualizzare il PIN e quindi copiarlo nel messaggio di posta elettronica.

10. Fare clic su **Chiudi** .

## Assegnazione di un PIN utente mediante i cmdlet di Windows PowerShell

È possibile assegnare i numeri PIN anche tramite il cmdlet Set-CsClientPin. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per assegnare automaticamente un numero PIN a un utente

  - Il comando seguente assegna un numero PIN all'utente Ken Myer. Poiché non è incluso il parametro Pin, Lync Server genererà e assegnerà il numero PIN automaticamente.
    
        Set-CsClientPin -Identity "Ken Myer" 

## Per assegnare un numero PIN specifico a un utente

  - Questo comando usa il parametro Pin per assegnare il numero PIN 121989 all'utente Ken Myer.
    
        Set-CsClientPin -Identity "Ken Myer" -Pin 121989

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Set-CsClientPin](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClientPin).

## Vedere anche

#### Concetti

[Numero di accesso esterno](https://technet.microsoft.com/it-it/library/gg133674\(v=ocs.15\))  

#### Ulteriori risorse

[Configurare regole per il PIN della conferenza telefonica con accesso esterno in Lync Server 2013](lync-server-2013-configure-dial-in-conferencing-personal-identification-number-pin-rules.md)

