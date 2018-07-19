---
title: 'Lync Server 2013: Creare o modificare una coda'
TOCTitle: Creare o modificare una coda
ms:assetid: b9d6366a-839f-4651-a01d-9254546cadeb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205207(v=OCS.15)
ms:contentKeyID: 49301787
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una coda in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Per creare o modificare una coda, utilizzare una delle procedure illustrate di seguito.

## Per creare o modificare una coda utilizzando il Pannello di controllo di Lync Server

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.
    

    > [!NOTE]
    > Se si è uno dei responsabili di Response Group delegati per un flusso di lavoro gestito, è possibile creare o modificare le code di Response Group e assegnarle ai flussi di lavoro gestiti personalmente.



2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Response Group** e quindi su **Coda** .

4.  Nella pagina **Coda** eseguire una delle operazioni seguenti:
    
      - Per creare una nuova coda, fare clic su **Nuovo** . In **Seleziona un servizio** digitare nel campo di ricerca parte oppure tutto il nome del servizio **ApplicationServer** in cui si intende aggiungere la coda. Nell'elenco di servizi risultante fare clic sul servizio desiderato e quindi su **OK** .
    
      - Per modificare una coda esistente, digitare tutto o una parte del nome della coda nel campo di ricerca. Nell'elenco di code risultante fare clic sulla coda desiderata, su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Nome** digitare un nome identificativo della coda.

6.  In **Descrizione** digitare una descrizione per la coda.

7.  In **Gruppi** specificare i gruppo che si desidera assegnare alla coda. Eseguire una delle operazioni seguenti:
    
      - Per aggiungere un gruppo alla coda, fare clic su **Seleziona** . Nel campo di ricerca **Seleziona gruppi** digitare tutto o parte del nome del gruppo di agenti che si intende assegnare alla coda, fare clic sul gruppo desiderato e quindi fare clic su **OK** .
    
      - Per rimuovere un gruppo dalla coda, nell'elenco di gruppi di agenti fare clic sul gruppo che si desidera rimuovere e quindi fare clic su **Rimuovi** .
    
      - Per modificare l'ordine in cui gli agenti vengono ricercati, nell'elenco di gruppi di agenti fare clic su un gruppo e quindi sulla freccia rivolta verso l'alto o verso il basso.
        

        > [!NOTE]
        > Per la ricerca di un agente disponibile per la coda, il server utilizza l'ordine dei gruppi. La ricerca pertanto viene eseguita prima nel primo gruppo, quindi nel secondo gruppo dell'elenco e così via.



8.  Per specificare un periodo di tempo massimo in cui un chiamante resta in attesa prima che un agente risponda alla chiamata, selezionare la casella di controllo **Abilita timeout coda** e quindi eseguire le operazioni seguenti:
    
    1.  In **Periodo di timeout (secondi)** specificare il numero massimo di secondi che un chiamante può attendere prima che un agente risponda alla chiamata.
    
    2.  In **Azione chiamata** selezionare l'azione che deve essere eseguita quando si verifica il timeout di una chiamata, come indicato di seguito:
    
    <!-- end list -->
    
      - Per disconnettere la chiamata dopo il timeout, fare clic su **Disconnetti** .
    
      - Per inoltrare la chiamata alla segreteria telefonica, fare clic su **Inoltra a segreteria telefonica** e quindi digitare un indirizzo di segreteria telefonica nel campo **Indirizzo SIP** nel formato sip: *\<nomeutente\>* @ *\<nomedominio\>* (ad esempio, sip:francesco@contoso.com).
    
      - Per inoltrare la chiamata a un altro numero di telefono, fare clic su **Inoltra a numero di telefono** e quindi digitare il numero di telefono nel campo **Indirizzo SIP** nel formato sip: *\<numero\>* @ *\<nomedominio\>* (ad esempio, sip:+14255550121@contoso.com).
    
      - Per inoltrare la chiamata a un altro utente, fare clic su **Inoltra a indirizzo SIP** e quindi digitare l'URI dell'utente nel campo **Indirizzo SIP** nel formato sip: *\<nomeutente\>* @ *\<nomedominio\>* .
    
      - Per inoltrare la chiamata a un'altra coda, fare clic su **Inoltra a un'altra coda** e quindi selezionare la coda che si desidera utilizzare.

9.  Per specificare il numero massimo di chiamate che possono essere contenute nella coda, selezionare la casella di controllo **Abilita overflow coda** e quindi eseguire le operazioni seguenti:
    
    1.  In **Numero massimo di chiamate** selezionare il numero massimo di chiamate che possono essere contenute nella coda.
    
    2.  In **Inoltra la chiamata** selezionare quale chiamata dovrà essere inoltrata quando la coda è piena, ovvero **Chiamata più recente** o **Chiamata meno recente** .
    
    3.  In **Azione chiamata** selezionare l'azione che deve essere eseguita quando viene raggiunta la soglia di overflow, come indicato di seguito:
    
    <!-- end list -->
    
      - Per disconnettere la chiamata dopo il timeout, fare clic su **Disconnetti** .
    
      - Per inoltrare la chiamata alla segreteria telefonica, fare clic su **Inoltra a segreteria telefonica** e quindi digitare un indirizzo di segreteria telefonica nel campo **Indirizzo SIP** nel formato sip: *\<nomeutente\>* @ *\<nomedominio\>* (ad esempio, sip:francesco@contoso.com).
    
      - Per inoltrare la chiamata a un altro numero di telefono, fare clic su **Inoltra a numero di telefono** e quindi digitare il numero di telefono nel campo **Indirizzo SIP** nel formato sip: *\<numero\>* @ *\<nomedominio\>* (ad esempio, sip:+14255550121@contoso.com).
    
      - Per inoltrare la chiamata a un altro utente, fare clic su **Inoltra a indirizzo SIP** e quindi digitare l'URI dell'utente nel campo **Indirizzo SIP** nel formato sip: *\<nomeutente\>* @ *\<nomedominio\>* .
    
      - Per inoltrare la chiamata a un'altra coda, fare clic su **Inoltra a un'altra coda** e quindi selezionare la coda che si desidera utilizzare.

10. Fare clic su **Commit** .

## Per creare o modificare una coda utilizzando Windows PowerShell

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.
    

    > [!NOTE]
    > Se si è uno dei responsabili di Response Group delegati per un flusso di lavoro gestito, è possibile creare gruppi di agenti e code, nonché assegnare i gruppi di agenti alle code.



2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Creare la richiesta da riprodurre quando viene raggiunta la soglia di timeout della coda e salvarla in una variabile. Nella riga di comando eseguire il comando seguente:
    
        $promptTO = New-CsRgsPrompt -TextToSpeechPrompt "<text for TTS prompt>"
    
    Ad esempio:
    
        "All agents are currently busy. Please call back later."
    

    > [!NOTE]
    > Per utilizzare un file audio per il messaggio, eseguire il cmdlet <STRONG>Import-CsRgsAudioFile</STRONG>. Per informazioni dettagliate, vedere <A href="https://docs.microsoft.com/powershell/module/skype/Import-CsRgsAudioFile">Import-CsRgsAudioFile</A>.



4.  Definire l'azione da eseguire quando viene raggiunta la soglia di timeout della coda e salvarla in una variabile. Nella riga di comando eseguire il comando seguente:
    
        $actionTO = New-CsRgsCallAction -Prompt <saved prompt from previous step> -Action <action to be taken>
    

    > [!NOTE]
    > Per informazioni dettagliate sulle azioni possibili e sulla relativa sintassi, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction">New-CsRgsCallAction</A>.

    
    Ad esempio:
    
        $action = New-CsRgsCallAction -Prompt $promptTO -Action Terminate

5.  Creare la richiesta da riprodurre quando viene raggiunta la soglia di overflow della coda e salvarla in una variabile. Nella riga di comando eseguire il comando seguente:
    
        $promptOV = New-CsRgsPrompt -TextToSpeechPrompt "<text for TTS prompt>"
    
    Ad esempio:
    
        $promptOV = New-CsRgsPrompt -TextToSpeechPrompt "Too many calls are waiting. Please call back later."
    

    > [!NOTE]
    > Per utilizzare un file audio per il messaggio, eseguire il cmdlet <STRONG>Import-CsRgsAudioFile</STRONG>. Per informazioni dettagliate, vedere <A href="https://docs.microsoft.com/powershell/module/skype/Import-CsRgsAudioFile">Import-CsRgsAudioFile</A>.



6.  Definire l'azione da eseguire quando viene raggiunta la soglia di overflow della coda e salvarla in una variabile. Nella riga di comando eseguire il comando seguente:
    
        $actionOV = New-CsRgsCallAction -Prompt <saved prompt from previous step> -Action <action to be taken>
    

    > [!NOTE]
    > Per informazioni dettagliate sulle azioni possibili e sulla relativa sintassi, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction">New-CsRgsCallAction</A>.

    
    Ad esempio:
    
        $action = New-CsRgsCallAction -Prompt $promptOV -Action Terminate

7.  Recuperare il nome del servizio Response Group Service e assegnarlo a una variabile. Nella riga di comando digitare il comando seguente:
    
        $serviceId="service:"+(Get-CSService | ?{$_.Applications -Like "*RGS*"}).ServiceId;

8.  Ottenere l'identità del gruppo di agenti da assegnare alla coda. Nella riga di comando eseguire il comando seguente:
    
        $agid = (Get-CsRgsAgentGroup -Name "Help Desk").Identity;
    

    > [!NOTE]
    > Per informazioni dettagliate sulla creazione del gruppo di agenti, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsAgentGroup">New-CsRgsAgentGroup</A>.



9.  Creare la coda. Nella riga di comando eseguire il comando seguente:
    
        $q = New-CsRgsQueue -Parent <saved service ID from previous step> -Name "<name of queue>" [-Description "<description for queue>"] [-TimeoutThreshold <# seconds before call times out>] [-TimeoutAction <saved timeout action>] [-OverflowThreshold <# calls queue can hold>] [-OverflowCandidate <call to be acted on when overflow threshold met>] [-OverflowAction <saved overflow action>] [-AgentGroupIDList(<agent group identity>)];
    
    Ad esempio:
    
        $q = New-CsRgsQueue -Parent $serviceId -Name "Help Desk" -Description "Contoso Help Desk" -TimeoutThreshold 300 -TimeoutAction $actionTO -OverflowThreshold 10 -OverflowCandidate NewestCall -OverflowAction $actionOV -AgentGroupIDList($agid.Identity;

10. Verificare che la coda sia stata creata. Eseguire il comando seguente:
    
        Get-CsRgsQueue -Name "Help Desk"

## Vedere anche

#### Ulteriori risorse

[New-CsRgsQueue](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsQueue)  
[Set-CsRgsQueue](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsRgsQueue)  
[New-CsRgsPrompt](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsPrompt)  
[New-CsRgsCallAction](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsRgsCallAction)  
[Get-CsRgsQueue](https://docs.microsoft.com/powershell/module/skype/Get-CsRgsQueue)  
[Import-CsRgsAudioFile](https://docs.microsoft.com/powershell/module/skype/Import-CsRgsAudioFile)  
[Remove-CsRgsQueue](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsRgsQueue)

