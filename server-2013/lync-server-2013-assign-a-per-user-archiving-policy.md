---
title: Assegnare criteri di archiviazione per utente
TOCTitle: Assegnare criteri di archiviazione per utente
ms:assetid: a12ca483-b235-460f-b3fe-130fb3087264
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182560(v=OCS.15)
ms:contentKeyID: 49301520
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri di archiviazione per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

I criteri di archiviazione sono una delle impostazioni singole di un account utente che è possibile configurare nel Pannello di controllo di Lync Server 2013.

La distribuzione di uno o più criteri di archiviazione per utente è facoltativa. È inoltre possibile distribuire criteri di archiviazione solo a livello globale o a livello di sito. Se si distribuiscono i criteri per utente, è necessario assegnarli in modo esplicito agli utenti, ai gruppi o agli oggetti contatto. Se non sono assegnati criteri a livello di sito o per utente specifici, come requisiti di archiviazione predefiniti vengono impostati automaticamente quelli definiti nei criteri di conferenza a livello globale.

Dopo la creazione di almeno un criterio di archiviazione per utente, utilizzare le procedure descritte in questo argomento per assegnare i criteri in modo da stabilire per ogni utente se il server deve archiviare le comunicazioni interne, le comunicazioni esterne o le comunicazioni di entrambi i tipi.

Per informazioni dettagliate sulla creazione di criteri di archiviazione per utente, vedere [Creazione di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per specifici siti o utenti](lync-server-2013-creating-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-specific-sites-or-users.md).

## Per assegnare criteri di archiviazione per utente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare per intero nome visualizzato, nome, cognome, nome account SAM (Security Accounts Manager), indirizzo SIP o URI linea dell'account utente desiderato, oppure digitare la prima parte di questi e quindi fare clic su **Trova**.
    
      - Se è disponibile una query salvata, fare clic sull'icona **Apri query**, recuperare la query (file con estensione usf) mediante la finestra di dialogo **Apri** e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare ulteriori criteri di ricerca per limitare i risultati:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Immettere una proprietà utente digitandola o selezionandola dall'elenco a discesa dopo aver fatto clic sulla freccia.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore, ad esempio **Uguale a** o **Non uguale a**).
    
    4.  A seconda della proprietà utente selezionata, immettere i criteri da utilizzare per filtrare i risultati della ricerca digitandoli o facendo clic sulla freccia dell'elenco a discesa.
        
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

6.  Fare clic su un utente all'interno dei risultati della ricerca, fare clic su **Azione** e quindi fare clic su **Assegna criteri**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si desidera applicare gli stessi criteri di archiviazione a più utenti, selezionare più utenti all'interno dei risultati di ricerca, fare clic su <strong>Azioni</strong> e quindi su <strong>Assegna criteri</strong>.</td>
    </tr>
    </tbody>
    </table>


7.  In **Assegna criteri**, in **Criteri di archiviazione**, eseguire una delle operazioni seguenti:
    

    > [!NOTE]
    > Poiché nella finestra di dialogo <STRONG>Assegna criteri</STRONG> è possibile configurare più criteri, per impostazione predefinita per tutti i criteri presenti nella finestra di dialogo è selezionata l'opzione <STRONG>&lt;Mantieni invariati&gt;</STRONG>. Per continuare a utilizzare i criteri assegnati in precedenza all'utente, non modificare l'impostazione.

    
      - Consentire a Lync Server 2013 di scegliere automaticamente tra i criteri a livello globale e i criteri a livello di sito, se definiti.
    
      - Fare clic sul nome di criteri di archiviazione per utente precedentemente definiti nella pagina **Criteri di archiviazione**.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Per agevolare la scelta dei criteri da assegnare, fare clic su un nome di criteri e quindi fare clic su <strong>Visualizza</strong> per visualizzare i diritti utente e le autorizzazioni definiti nei criteri.</td>
        </tr>
        </tbody>
        </table>


8.  Al termine, fare clic su **OK**.

## Assegnazione di criteri di archiviazione per utente tramite i cmdlet di Windows PowerShell

È possibile assegnare criteri di archiviazione per utente anche utilizzando Windows PowerShell e il cmdlet **Grant-CsArchivingPolicy**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell oppure da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Assegnazione di criteri di archiviazione per utente a un singolo utente

  - Il comando seguente assegna il criterio di archiviazione per utente RedmondArchivingPolicy all'utente Ken Myer:
    
        Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName "RedmondArchivingPolicy"

## Assegnazione di criteri di archiviazione per utente a più utenti

  - Questo comando assegna il criterio di archiviazione per utente RedmondArchivingPolicy a tutti gli utenti i cui account si trovano nel pool di registrazione atl-cs-001.litwareinc.com. Per ulteriori informazioni sul parametro Filter utilizzato nel comando, vedere la documentazione relativa al cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsArchivingPolicy -PolicyName "RedmondArchivingPolicy"

## Annullamento dell'assegnazione di criteri di archiviazione per utente

  - Il comando seguente annulla l'assegnazione di qualsiasi criterio di archiviazione per utente precedentemente assegnato a Ken Myer. Dopo l'annullamento dell'assegnazione dei criteri per utente, Ken Myer verrà gestito automaticamente mediante l'utilizzo dei criteri globali o dei criteri del sito locale, se esistenti. I criteri del sito hanno la precedenza sui criteri globali.
    
        Grant-CsarchivingPolicy -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Grant-CsArchivingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsArchivingPolicy).

## Vedere anche

#### Attività

[Creazione di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per specifici siti o utenti](lync-server-2013-creating-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-specific-sites-or-users.md)  

#### Ulteriori risorse

[Assegnazione di criteri per utente in Lync Server 2013](lync-server-2013-assigning-per-user-policies.md)

