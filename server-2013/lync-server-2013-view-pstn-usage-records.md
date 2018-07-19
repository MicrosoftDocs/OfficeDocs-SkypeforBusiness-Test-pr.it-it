---
title: 'Lync Server 2013: Visualizzare record utilizzo PSTN'
TOCTitle: Visualizzare record utilizzo PSTN
ms:assetid: 65025c78-c263-472c-9ff9-e170588f10b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398458(v=OCS.15)
ms:contentKeyID: 49300797
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare record utilizzo PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Un record di utilizzo PSTN (Public Switched Telephone Network) specifica una classe di chiamata (ad esempio, interna, locale o interurbana) che può essere effettuata da diversi utenti o gruppi di utenti di un'organizzazione. Per informazioni dettagliate, vedere [Record utilizzo PSTN in Lync Server 2013](lync-server-2013-pstn-usage-records.md) nella documentazione relativa alla pianificazione.

## Per visualizzare un record di utilizzo PSTN tramite il Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Utilizzo PSTN** .

4.  Nella pagina **Utilizzo PSTN** evidenziare i record di utilizzo PSTN che si desidera visualizzare, fare clic su **Modifica** e quindi su **Mostra dettagli** .
    

    > [!NOTE]
    > In una pagina di sola lettura per il record di utilizzo PSTN selezionato vengono visualizzati le route e i criteri vocali associati.



## Visualizzazione di informazioni sull'utilizzo PSTN tramite i cmdlet di Windows PowerShell

Per visualizzare gli utilizzi PSTN, è inoltre possibile utilizzare Windows PowerShell e il cmdlet **Get-CsPstnUsage**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare le informazioni sull'utilizzo PSTN tramite i cmdlet di Windows PowerShell

  - Per visualizzare informazioni su tutti gli utilizzi PSTN, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsPstnUsage
    
    Questo comando restituisce informazioni simili alle seguenti:
    
        Identity : Global
        Usage    : {Internal, Local, Long Distance}

Per informazioni dettagliate, vedere [Get-CsPstnUsage](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsPstnUsage).

## Vedere anche

#### Attività

[Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)

