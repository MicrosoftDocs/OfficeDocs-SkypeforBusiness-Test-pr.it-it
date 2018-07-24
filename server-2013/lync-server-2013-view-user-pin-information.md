---
title: Visualizzare le informazioni sul PIN degli utenti
TOCTitle: Visualizzare le informazioni sul PIN degli utenti
ms:assetid: 59e38117-8112-4851-82ac-a746ffa0f89d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688067(v=OCS.15)
ms:contentKeyID: 49887575
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni sul PIN degli utenti

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Per partecipare a una conferenza telefonica con accesso esterno come utente autenticato, un utente di Lync Server 2013 con credenziali di Servizi di dominio Active Directory deve disporre di un PIN (Personal Identification Number). È possibile visualizzare le informazioni sul PIN di un utente dal Pannello di controllo di Lync Server 2013.


> [!NOTE]
> È possibile visualizzare informazioni sullo stato del PIN, ad esempio per scoprire se il PIN è stato impostato o quando è stato modificato l'ultima volta, ma non è possibile vedere il PIN corrente controllandone lo stato. Se un utente perde il PIN, è possibile reimpostarlo seguendo le procedure descritte in <A href="lync-server-2013-set-a-user-s-dial-in-conferencing-pin.md">Impostare il PIN di conferenza telefonica con accesso esterno di un utente in Lync Server 2013</A>



## Per visualizzare il PIN di un utente nel Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare interamente o la parte iniziale di nome visualizzato, nome, cognome, nome account SAM (Security Accounts Manager), indirizzo SIP o URI (Uniform Resource Identifier) dell'account utente desiderato e quindi fare clic su **Trova**.
    
      - Se è presente una query salvata, fare clic sull'icona **Apri query**, utilizzare la finestra di dialogo **Apri** per recuperare la query (file con estensione usf) e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare criteri di ricerca aggiuntivi per ridurre i risultati:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Immettere la proprietà utente digitandola o facendo clic sulla freccia nell'elenco a discesa e selezionando la proprietà.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore (ad esempio **Uguale a** o **Non uguale a**).
    
    4.  A seconda della proprietà utente selezionata, immettere i criteri che si desidera utilizzare per filtrare i risultati della ricerca digitandoli oppure facendo clic sulla freccia nell'elenco a discesa.
        
        > [!tip]  
        > Per aggiungere ulteriori clausole di ricerca alla query, fare clic su <strong>Aggiungi filtro</strong>.    
    5.  Fare clic su **Trova**.
    

    > [!NOTE]
    > Se il PIN è bloccato, è necessario sbloccarlo per poterlo impostare. Per sbloccare il PIN, fare clic sull'utente, su <STRONG>Azione</STRONG> e quindi su <STRONG>Sblocca PIN</STRONG>.



6.  Fare clic su un utente nei risultati della ricerca, su **Azione** e quindi su **Visualizza stato PIN**.

## Per visualizzare le informazioni sul PIN di un utente tramite i cmdlet di Lync Server Management Shell

Per visualizzare le informazioni sul PIN di un utente, è possibile utilizzare il cmdlet Get-CsClientPinInfo, che può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzazione informazioni sul PIN di un utente

  - Per visualizzare informazioni sul PIN di un utente, digitare un comando simile al seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsClientPinInfo -Identity "Ken Myer"
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity          : sip:kenmyer@litwareinc.com
        IsPinSet          : False
        IsLockedOut       : False
        LastPinChangeTime : 9/25/2012 1:35:03 PM
        PinExpirationTime :

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Get-CsConferenceDisclaimer](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsConferenceDisclaimer).

## Vedere anche

#### Attività

[Impostare il PIN di conferenza telefonica con accesso esterno di un utente in Lync Server 2013](lync-server-2013-set-a-user-s-dial-in-conferencing-pin.md)  
[Bloccare o sbloccare il PIN di un utente](lync-server-2013-lock-or-unlock-a-user-pin.md)

