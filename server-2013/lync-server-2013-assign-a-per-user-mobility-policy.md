---
title: Assegnare criteri dispositivi mobili per utente
TOCTitle: Assegnare criteri dispositivi mobili per utente
ms:assetid: d8bf997f-4bc7-48d3-973b-323505f55e9d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721902(v=OCS.15)
ms:contentKeyID: 49887779
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri dispositivi mobili per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

I criteri dispositivi mobili rappresentano una delle singole impostazioni di un account utente che è possibile configurare nel Pannello di controllo di Lync Server o in Lync Server Management Shell.

## Per assegnare criteri dispositivi mobili per utente nel Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Utilizzare uno dei metodi seguenti per individuare un utente:
    
      - Nella casella **Cerca utenti** digitare interamente o la parte iniziale di nome visualizzato, nome, cognome, nome account SAM (Security Accounts Manager), indirizzo SIP o URI (Uniform Resource Identifier) dell'account utente desiderato e quindi fare clic su **Trova**.
    
      - Se è presente una query salvata, fare clic sull'icona **Apri query**, utilizzare la finestra di dialogo **Apri** per recuperare la query (file con estensione usf) e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare criteri di ricerca aggiuntivi per limitare i risultati:
    
    1.  Fare clic su **Aggiungi filtro**.
    
    2.  Immettere la proprietà utente digitandola o facendo clic sulla freccia nell'elenco a discesa e selezionando la proprietà.
    
    3.  Nell'elenco a discesa **Uguale a** fare clic sull'operatore, ad esempio **Uguale a** o **Diverso da**.
    
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

6.  Fare clic su un utente nei risultati della ricerca, su **Azione** e quindi su **Assegna criteri**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si desidera applicare lo stesso criterio dispositivi mobili per utente a più utenti, selezionare più utenti nei risultati della ricerca, fare clic su <strong>Azioni</strong> e quindi su <strong>Assegna criteri</strong>.</td>
    </tr>
    </tbody>
    </table>


7.  In **Criteri dispositivi mobili** in **Assegna criteri** eseguire una delle operazioni seguenti:
    

    > [!NOTE]
    > Poiché sono molti i criteri che è possibile configurare in <STRONG>Assegna criteri</STRONG>, l'opzione <STRONG>&lt;Mantieni invariati&gt;</STRONG> è selezionata per impostazione predefinita per tutti i criteri nella finestra di dialogo. Per continuare a utilizzare i criteri assegnati in precedenza all'utente, non apportare modifiche a questa impostazione.

    
      - Selezionare **\<Automatici\>** per consentire la selezione automatica dei criteri a livello globale o, se definiti, dei criteri a livello di sito in Lync Server 2013.
    
      - Fare clic sul nome di un criterio dispositivi mobili per utente precedentemente definito nella pagina **Criteri dispositivi mobili**.
        
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

## Assegnazione di criteri dispositivi mobili per utente mediante i cmdlet di Lync Server Management Shell

È possibile assegnare criteri dispositivi mobili per utente utilizzando Lync Server Management Shell e il cmdlet **Grant-CsMobilityPolicy**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per assegnare criteri dispositivi mobili per utente a un singolo utente

  - Il comando seguente assegna il criterio dispositivi mobili per utente RedmondMobilityPolicy all'utente Ken Myer.
    
        Grant-CsMobilityPolicy -Identity "Ken Myer" -PolicyName "RedmondMobilityPolicy"

## Per assegnare criteri dispositivi mobili per utente a più utenti

  - Il comando seguente assegna il criterio dispositivi mobili per utente RedmondMobilityPolicy a tutti gli utenti a cui è attualmente assegnato il criterio NorthAmericaMobilityPolicy. Per informazioni dettagliate sul parametro Filter utilizzato nel comando, vedere [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -Filter {MobilityPolicy -eq "NorthAmericaMobilityPolicy"} | Grant-CsMobilityPolicy -PolicyName "RedmondMobilityPolicy"

## Per annullare l'assegnazione di criteri dispositivi mobili per utente

  - Il comando seguente annulla l'assegnazione del criterio dispositivi mobili per utente precedentemente assegnato a Ken Myer. Dopo l'annullamento dell'assegnazione del criterio per utente, Ken Myer verrà gestito automaticamente utilizzando i criteri globali oppure l'eventuale criterio sito locale corrispondente. I criteri sito infatti hanno la priorità sui criteri globali.
    
        Grant-CsMobilityPolicy -Identity "Ken Myer" -PolicyName $Null

Per informazioni dettagliate, vedere [Grant-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsMobilityPolicy).

## Vedere anche

#### Attività

[Configurazione dei criteri per dispositivi mobili in Lync Server 2013](lync-server-2013-configuring-mobility-policy.md)

