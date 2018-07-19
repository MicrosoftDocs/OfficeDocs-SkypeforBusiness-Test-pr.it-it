---
title: Assegnare criteri di conferenza per utente
TOCTitle: Assegnare criteri di conferenza per utente
ms:assetid: 72f12c72-65f7-44fe-ab81-0f57cb2f87d1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521015(v=OCS.15)
ms:contentKeyID: 49300963
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri di conferenza per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

I criteri di conferenza rappresentano una delle singole impostazioni di un account utente che è possibile configurare in Pannello di controllo di Lync Server.

La distribuzione di uno o più criteri di conferenza per utente è facoltativa. È inoltre possibile distribuire solo criteri di conferenza a livello globale o a livello di sito. Se si distribuiscono criteri per utente, è necessario assegnarli in modo esplicito a utenti, gruppi o oggetti contatto. Le autorizzazioni e i diritti utente per le conferenze vengono impostati automaticamente su quelli definiti nei criteri di conferenza a livello globale quando non sono assegnati criteri a livello di sito o per utente specifici.

Dopo aver creato criteri di conferenza per utente, utilizzare le procedure incluse in questo argomento per assegnare i criteri che specificano le autorizzazioni e i diritti utente che si desidera vengano concessi dal server alle riunioni organizzate da un utente specifico.

Per un elenco di tutte le impostazioni disponibili per i criteri di conferenza, vedere [Guida di riferimento alle impostazioni dei criteri di conferenza di Lync Server 2013](lync-server-2013-conferencing-policy-settings-reference.md).

Per informazioni dettagliate sulla creazione di criteri di conferenza per utente, vedere [Creare o modificare criteri conferenza](lync-server-2013-create-or-modify-a-conferencing-policy.md).

## Per assegnare criteri di conferenza per utente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare interamente o la prima parte di nome visualizzato, nome, cognome, nome account SAM (Security Accounts Manager), indirizzo SIP o URI (Uniform Resource Identifier) linea dell'account utente e quindi fare clic su **Trova**.
    
      - Se è disponibile una query salvata, fare clic sull'icona **Apri query**, utilizzare la finestra di dialogo **Apri** per recuperare la query (file con estensione usf) e quindi fare clic su **Trova**.

5.  Facoltativo: specificare criteri di ricerca aggiuntivi per limitare i risultati:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Immettere la proprietà utente digitandola o facendo clic sulla freccia nell'elenco a discesa per selezionarla.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore, ad esempio **Uguale a** o **Diverso da**.
    
    4.  A seconda della proprietà utente selezionata, immettere i criteri che si desidera utilizzare per filtrare i risultati della ricerca digitandoli o facendo clic sulla freccia nell'elenco a discesa.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per aggiungere clausole di ricerca aggiuntive alla query, fare clic su <strong>Aggiungi filtro</strong>.</td>
        </tr>
        </tbody>
        </table>
    
    5.  Fare clic su **Trova**.

6.  Fare clic su un utente nei risultati della ricerca, fare clic su **Azione** e quindi su **Assegna criteri**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si desidera applicare gli stessi criteri di conferenza per utente a più utenti, selezionare i diversi utenti nei risultati della ricerca, fare clic su <strong>Azioni</strong> e quindi su <strong>Assegna criteri</strong>.</td>
    </tr>
    </tbody>
    </table>


7.  In **Criteri conferenza** in **Assegna criteri** eseguire una delle operazioni seguenti:
    

    > [!NOTE]
    > Poiché sono molti i criteri che è possibile configurare in <STRONG>Assegna criteri</STRONG>, l'opzione <STRONG>&lt;Mantieni invariati&gt;</STRONG> è selezionata per impostazione predefinita per tutti i criteri nella finestra di dialogo. Per continuare a utilizzare i criteri assegnati in precedenza all'utente, non apportare modifiche a questa impostazione.

    
      - Selezionare **\<Automatici\>** per consentire la selezione automatica dei criteri a livello globale o, se definiti, dei criteri a livello di sito in Lync Server 2013.
    
      - Fare clic sui nomi dei criteri di conferenza per utente definiti in precedenza nella pagina **Criteri conferenza**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per stabilire i criteri che si desidera assegnare, dopo avere fatto clic sui nomi dei criteri, fare clic su <strong>Visualizza</strong> per visualizzare le autorizzazioni e i diritti utente definiti nei criteri.</td>
        </tr>
        </tbody>
        </table>


8.  Al termine, fare clic su **OK**.

## Assegnazione di un criterio di conferenza per utente attraverso i cmdlet di Lync Server PowerShell

È possibile assegnare criteri di conferenza per utente anche attraverso Lync Server PowerShell e il cmdlet Grant-CsConferencingPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Assegnazione di un criterio di conferenza per utente a utenti singoli

  - Il comando seguente assegna il criterio di conferenza per utente RedmondConferencingPolicy all'utente Ken Myer.
    
        Grant-CsConferencingPolicy -Identity "Ken Myer" -PolicyName "RedmondConferencingPolicy"

## Assegnazione di un criterio di conferenza per utente a più utenti

  - Questo comando assegna il criterio di conferenza per utente HRConferencingPolicy a tutti gli utenti che lavorano nel dipartimento delle Risorse umane. Per maggiori informazioni sul parametro LdapFilter utilizzato in questo comando, vedere la documentazione relativa al cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -LdapFilter "Department=Human Resources" | Grant-CsConferencingPolicy -PolicyName "HRConferencingPolicy"

## Annullamento dell'assegnazione di un criterio di conferenza per utente

  - Il comando seguente annulla l'assegnazione di tutti i criteri di conferenza per utente precedentemente assegnati a Ken Myer. Dopo l'annullamento del criterio per utente, Ken Myer sarà gestito automaticamente dal criterio globale oppure dall'eventuale criterio del sito locale, che ha la precedenza sul criterio globale.
    
        Grant-CsConferencingPolicy -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Grant-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsConferencingPolicy).

## Vedere anche

#### Attività

[Creare o modificare criteri conferenza](lync-server-2013-create-or-modify-a-conferencing-policy.md)  

#### Ulteriori risorse

[Assegnazione di criteri per utente in Lync Server 2013](lync-server-2013-assigning-per-user-policies.md)

