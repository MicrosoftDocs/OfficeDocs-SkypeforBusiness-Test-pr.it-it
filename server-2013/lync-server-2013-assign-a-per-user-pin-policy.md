---
title: Assegnare criteri PIN per utente
TOCTitle: Assegnare criteri PIN per utente
ms:assetid: d8211c64-0b63-4193-a074-673da7d14287
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182594(v=OCS.15)
ms:contentKeyID: 49302148
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri PIN per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

I criteri PIN per conferenze telefoniche con accesso esterno rientrano tra le singole impostazioni di un account utente che è possibile configurare nel Pannello di controllo di Lync Server 2013.

La distribuzione di uno o più criteri per il PIN per utente è facoltativa. È inoltre possibile distribuire solo criteri per il PIN globali o a livello di sito. Se si distribuiscono criteri per utente, è necessario assegnarli in modo esplicito a utenti, gruppi o oggetti contatto. I diritti e le autorizzazioni degli utenti relativamente all'utilizzo di PIN per conferenze telefoniche con accesso esterno sono impostati automaticamente su quelli definiti nei criteri per il PIN globali, quando non sono stati assegnati criteri specifici a livello di sito o per utente.

Dopo aver creato almeno un criterio PIN per utente, eseguire le procedure descritte in questo argomento per assegnare il criterio che specifica i vincoli che si desidera imporre ai PIN creati e utilizzati da un determinato utente.

Per informazioni dettagliate sulla creazione di criteri per il PIN per utente per conferenze telefoniche con accesso esterno, vedere [Creare o modificare le impostazioni del PIN di conferenza telefonica con accesso esterno in Lync Server 2013 per un sito o un gruppo di utenti](lync-server-2013-create-or-modify-dial-in-conferencing-pin-settings-for-a-site-or-group-of-users.md).

## Per assegnare criteri per il PIN per utente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare interamente o solo la prima parte del nome visualizzato, nome, cognome, nome dell'account Gestione account di protezione, indirizzo SIP o URI (Uniform Resource Identifier (URI) di linea dell'account utente e quindi fare clic su **Trova**.
    
      - Se è stata salvata una query, fare clic sull'icona **Apri query**, recuperare la query (file con estensione usf) tramite la finestra di dialogo **Apri** e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare altri criteri di ricerca per restringere i risultati:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Digitare la proprietà utente oppure fare clic sulla freccia nell'elenco a discesa per selezionarla.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore, ad esempio **Uguale a** o **Diverso da**.
    
    4.  A seconda della proprietà utente selezionata, digitare i criteri da utilizzare per filtrare i risultati della ricerca oppure selezionarli facendo clic sulla freccia nell'elenco a discesa.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per aggiungere altre clausole di ricerca alla query, fare clic su <strong>Aggiungi filtro</strong>.</td>
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
    <td>Se si desidera applicare gli stessi criteri per il PIN per utente a più utenti, selezionarli nei risultati di ricerca, fare clic su <strong>Azioni</strong> e quindi su <strong>Assegna criteri</strong>.</td>
    </tr>
    </tbody>
    </table>


7.  In **Assegna criteri** eseguire una delle operazioni seguenti in **Criteri PIN**:
    

    > [!NOTE]
    > Poiché è possibile configurare più criteri utilizzando la finestra di dialogo <STRONG>Assegna criteri</STRONG>, per impostazione predefinita è selezionata l'opzione <STRONG>&lt;Mantieni invariati&gt;</STRONG> per ogni criterio. Continuare a utilizzare i criteri assegnati in precedenza all'utente non effettuando modifiche a questa impostazione.

    
      - Consentire a Lync Server 2013 di scegliere automaticamente i criteri a livello globale o, se definiti, i criteri a livello di sito.
    
      - Fare clic sul nome di un criterio PIN per utente definito in precedenza nella pagina **Criteri PIN**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per decidere i criteri da assegnare, dopo aver fatto clic su un nome di criteri fare clic su <strong>Visualizza</strong> per visualizzare i diritti e le autorizzazioni utente che definisce.</td>
        </tr>
        </tbody>
        </table>


8.  Al termine, fare clic su **OK**.

## Assegnazione di criteri PIN per utente mediante i cmdlet di Lync Server Management Shell

È possibile assegnare criteri PIN per utente utilizzando Lync Server Management Shell e il cmdlet **Grant-CsPinPolicy**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per assegnare criteri PIN per utente a un singolo utente

  - Il comando seguente assegna il criterio PIN per utente RedmondPinPolicy all'utente Ken Myer.
    
        Grant-CsPinPolicy -Identity "Ken Myer" -PolicyName "RedmondPinPolicy"

## Per assegnare criteri PIN per utente a più utenti

  - Il comando seguente assegna il criterio PIN per utente RedmondUsersPinPolicy a tutti gli utenti che lavorano nella città di Redmond. Per informazioni dettagliate sul parametro LdapFilter utilizzato nel comando, vedere [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPinPolicy -PolicyName "RedmondUsersPinPolicy"

## Per annullare l'assegnazione di criteri PIN per utente

  - Il comando seguente annulla l'assegnazione del criterio PIN per utente precedentemente assegnato a Ken Myer. Dopo l'annullamento dell'assegnazione del criterio per utente, Ken Myer verrà gestito automaticamente utilizzando i criteri globali oppure l'eventuale criterio sito locale corrispondente. I criteri sito infatti hanno la priorità sui criteri globali.
    
        Grant-CsPinPolicy -Identity "Ken Myer" -PolicyName $Null

Per informazioni dettagliate, vedere [Grant-CsPinPolicy](grant-cspinpolicy.md).

## Vedere anche

#### Attività

[Creare nuovi criteri per il PIN](lync-server-2013-create-a-new-pin-policy.md)  

#### Ulteriori risorse

[Assegnazione di criteri per utente in Lync Server 2013](lync-server-2013-assigning-per-user-policies.md)

