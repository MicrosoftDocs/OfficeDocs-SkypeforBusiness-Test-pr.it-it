---
title: Assegnare criteri di chat persistente per utente
TOCTitle: Assegnare criteri di chat persistente per utente
ms:assetid: e22168f2-fde1-4f0a-b194-1fc881436822
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721908(v=OCS.15)
ms:contentKeyID: 49887788
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri di chat persistente per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile assegnare criteri di chat persistente per utente sia nel Pannello di controllo di Lync Server 2013 che con Lync Server 2013 Management Shell. Per informazioni dettagliate sulla creazione di criteri utente per server Chat persistente, vedere [Creare criteri utente per Chat persistente in Lync Server 2013](lync-server-2013-create-a-user-policy-for-persistent-chat.md).

## Per assegnare criteri di chat persistente per utente nel Pannello di controllo di Lync Server

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
    
    4.  A seconda della proprietà utente selezionata, immettere il criterio da utilizzare per filtrare i risultati di ricerca digitandolo o facendo clic sulla freccia nell'elenco a discesa.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per aggiungere ulteriori clausole di ricerca alla query, fare clic su <strong>Aggiungi filtro</strong>.</td>
        </tr>
        </tbody>
        </table>
    
    5.  Fare clic su **Trova**.

6.  Fare clic su un utente nei risultati di ricerca, fare clic su **Azione** e quindi fare clic su **Assegna criteri**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si desidera applicare gli stessi criteri di chat persistente a più utenti, selezionare più utenti all'interno dei risultati di ricerca, fare clic su <strong>Azioni</strong> e quindi su <strong>Assegna criteri</strong>.</td>
    </tr>
    </tbody>
    </table>


7.  In **Assegna criteri** eseguire una delle operazioni seguenti in **Criteri chat persistente**:
    

    > [!NOTE]
    > Poiché vi sono più criteri che è possibile configurare utilizzando la finestra di dialogo <STRONG>Assegna criteri</STRONG>, l'opzione <STRONG>&lt;Mantieni invariati&gt;</STRONG> è selezionata per impostazione predefinita per ogni criterio nella finestra di dialogo. Continuare a utilizzare i criteri precedentemente assegnati all'utente senza apportare modifiche a questa impostazione.

    
      - Selezionare **\<Automatici\>** per consentire la selezione automatica dei criteri a livello globale o, se definiti, dei criteri a livello di sito in Lync Server 2013.
    
      - Fare clic sul nome dei criteri di chat persistente per utente precedentemente definiti nella pagina **Criteri chat persistente**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per decidere quali criteri assegnare, dopo aver selezionato un nome di criteri, fare clic su <strong>Visualizza</strong> per visualizzare i diritti utente e le autorizzazioni definite nei criteri.</td>
        </tr>
        </tbody>
        </table>


8.  Al termine, fare clic su **OK**.

## Assegnazione di criteri di chat persistente tramite i cmdlet di PowerShell per Lync Server

Per assegnare i criteri di chat persistente per utente, è inoltre possibile utilizzare PowerShell per Lync Server e il cmdlet Grant-CsPersistentChatPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Assegnazione di criteri di chat persistente per utente a un singolo utente

  - Il comando seguente consente di assegnare i criteri di chat persistente per utente denominati RedmondPersistentChatPolicy all'utente Ken Myer.
    
        Grant-CsPersistentChatPolicy -Identity "Ken Myer" -PolicyName "RedmondPersistentChatPolicy"

## Assegnazione di criteri di chat persistente per utente a più utenti

  - Questo comando consente di assegnare i criteri di chat persistente per utente RedmondUsersPersistentChatPolicy a tutti gli utenti che fanno parte del reparto IT. Per ulteriori informazioni sul parametro LdapFilter utilizzato in questo comando, vedere la documentazione per il cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -LdapFilter "Department=IT" | Grant-CsPersistentChatPolicy -PolicyName "RedmondUsersPersistentChatPolicy"

## Annullamento dell'assegnazione di criteri di chat persistente per utente

  - Il comando seguente consente di annullare l'assegnazione dei criteri di chat persistente per utente precedentemente assegnati all'utente Ken Myer. Dopo l'annullamento dell'assegnazione dei criteri per utente, Ken Myer verrà gestito automaticamente tramite i criteri globali oppure i criteri di sito locale, se esistenti. I criteri di sito sono prioritari rispetto ai criteri globali.
    
        Grant-CsPersistentChatPolicy -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md).

## Vedere anche

#### Concetti

[Creare criteri utente per Chat persistente in Lync Server 2013](lync-server-2013-create-a-user-policy-for-persistent-chat.md)

