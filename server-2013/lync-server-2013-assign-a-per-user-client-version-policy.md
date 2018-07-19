---
title: Assegnare criteri di versione client per utente
TOCTitle: Assegnare criteri di versione client per utente
ms:assetid: f7e8ba2f-62dc-4e7d-8b63-682986f10240
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182607(v=OCS.15)
ms:contentKeyID: 49302523
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri di versione client per utente

 

_**Ultima modifica dell'argomento:** 2013-02-22_

I criteri di versione client sono una delle singole impostazioni di un account utente che è possibile configurare nel Pannello di controllo di Lync Server.

La distribuzione di uno o più criteri di versione client per utente è facoltativa. È anche possibile distribuire solo un criterio di versione client a livello globale oppure criteri di versione client a livello di sito o di pool. Se si distribuiscono i criteri per utente, è necessario assegnarli in modo esplicito a utenti, gruppi o oggetti contatto. Quando non viene assegnato alcun criterio specifico a livello di sito, di pool o per utente, i client predefiniti a cui è consentita la registrazione a Lync Server 2013 sono quelli definiti nei criteri di versione client a livello globale.

Dopo aver creato almeno un criterio di versione client per utente, utilizzare le procedure riportate in questo argomento per assegnare i criteri che specificano le versioni client a cui si desidera consentire la registrazione a Lync Server.

Per informazioni dettagliate sulla creazione di criteri di versione client per utente, vedere [Specificazione delle applicazioni client utilizzabili per accedere a Lync Server 2013](lync-server-2013-specifying-the-client-applications-that-can-be-used-to-log-on-to-lync-server-2013.md).

## Per assegnare criteri di versione client per utente

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
    <td>Se si desidera applicare a più utenti gli stessi criteri di versione client per utente, selezionare più utenti nei risultati di ricerca, fare clic su <strong>Azioni</strong> e quindi su <strong>Assegna criteri</strong>.</td>
    </tr>
    </tbody>
    </table>


7.  In **Assegna criteri**, in **Criteri versione client** effettuare una delle operazioni seguenti:
    

    > [!NOTE]
    > Poiché vi sono più criteri che è possibile configurare utilizzando la finestra di dialogo <STRONG>Assegna criteri</STRONG>, l'opzione <STRONG>&lt;Mantieni invariati&gt;</STRONG> è selezionata per impostazione predefinita per ogni criterio nella finestra di dialogo. Continuare a utilizzare i criteri precedentemente assegnati all'utente senza apportare modifiche a questa impostazione.

    
      - Consentire a Lync Server di scegliere automaticamente i criteri a livello globale o, se definiti, i criteri a livello di sito o di pool.
    
      - Fare clic sul nome dei criteri di versione client per utente precedentemente definiti nella pagina **Criteri versione client**.
        
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

## Per assegnare criteri di versione client per utente utilizzando i cmdlet di Lync Server Management Shell

È possibile assegnare un criterio di versione client per utente utilizzando il cmdlet Grant-CsClientVersionPolicy. È possibile eseguire il cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per assegnare un criterio di versione client per utente a un unico utente

  - Il comando seguente assegna il criterio di versione client per utente RedmondClientVersionPolicy all'utente Davide Garghentini.
    
        Grant-CsClientVersionPolicy -Identity "Ken Myer" -PolicyName "RedmondClientVersionPolicy"

## Per assegnare un criterio di versione client per utente a più utenti

  - Il comando assegna il criterio di versione client per utente RedmondClientVersionPolicy a tutti gli utenti a cui è attualmente assegnato il criterio vocale RedmondVoicePolicy. Per ulteriori informazioni sul parametro Filter utilizzato in questo comando, consultare la documentazione relativa al cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -Filter {VoicePolicy -eq "RedmondVoicePolicy"} | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## Per annullare l'assegnazione dei criteri di versione client per utente

  - Il comando seguente annulla l'assegnazione del criterio di versione client per utente precedentemente assegnato a Davide Garghentini. Dopo che l'assegnazione del criterio per utente è stata annullata, Davide Garghentini verrà gestito automaticamente utilizzando il criterio globale, il relativo criterio sito globale (se esistente) o il criterio dell'ambito del servizio assegnato alla relativa Registrazione avanzata. Un criterio ambito del servizio ha la precedenza rispetto a un criterio sito e un criterio sito ha la precedenza rispetto al criterio globale.
    
        Grant-CsClientVersionPolicy -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Grant-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsClientVersionPolicy).

## Vedere anche

#### Ulteriori risorse

[Assegnazione di criteri per utente in Lync Server 2013](lync-server-2013-assigning-per-user-policies.md)  
[Gestione di dispositivi, telefoni e applicazioni client in Lync Server 2013](lync-server-2013-managing-devices-phones-and-client-applications.md)

