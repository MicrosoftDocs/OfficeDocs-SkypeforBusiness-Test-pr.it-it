---
title: Abilitazione o disabilitazione delle notifiche Push per Windows Phone
TOCTitle: Abilitazione o disabilitazione delle notifiche Push per Windows Phone
ms:assetid: a34f0c5c-4228-40e3-9d93-bc0b5df4895d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688162(v=OCS.15)
ms:contentKeyID: 49887688
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione o disabilitazione delle notifiche Push per Windows Phone

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le notifiche Push, sotto forma di riquadri, icone o avvisi, possono essere inviate a un Windows Phone anche se l'applicazione per dispositivi mobili è inattiva. Le notifiche Push avvisano gli utenti in caso di eventi quali inviti a sessioni di messaggistica istantanea nuovi o senza risposta e di messaggi in segreteria telefonica. È possibile abilitare o disabilitare le notifiche Push per i dispositivi Windows Phone utilizzando il Pannello di controllo di Lync Server 2013 o Lync Server 2013 Management Shell.

## Per abilitare le notifiche Push per Windows Phone dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione notifiche Push**.

4.  Nella pagina **Configurazione notifiche Push** fare clic sul sito che si desidera modificare e quindi scegliere **Mostra dettagli** dal menu **Modifica**.

5.  Selezionare la casella di controllo **Abilita notifiche Push di Microsoft**.

6.  Fare clic su **Commit**.

## Per disabilitare le notifiche Push per Windows Phone dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione notifiche Push**.

4.  Nella pagina **Configurazione notifiche Push** fare clic sul sito che si desidera modificare e quindi scegliere **Mostra dettagli** dal menu **Modifica**.

5.  Deselezionare la casella di controllo **Abilita notifiche Push di Microsoft**.

6.  Fare clic su **Commit**.

## Per abilitare o disabilitare le notifiche Push per Windows Phone mediante i cmdlet di Windows PowerShell

È possibile abilitare o disabilitare le notifiche Push per Windows Phone utilizzando il cmdlet **Set-CsPushNotificationConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell oppure da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare le notifiche Push per Windows Phone

  - Per abilitare le notifiche Push per Windows Phone, impostare il valore della proprietà EnableMicrosoftPushNotificationService su True ($True). Ad esempio:
    
        Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableMicrosoftPushNotificationService $True

## Per disabilitare le notifiche Push per Windows Phone

  - Per disabilitare le notifiche Push per Windows Phone, impostare il valore della proprietà EnableMicrosoftPushNotificationService su False ($False). Ad esempio:
    
        Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableMicrosoftPushNotificationService $False

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsPushNotificationConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPushNotificationConfiguration).

## Vedere anche

#### Attività

[Configurazione delle notifiche push in Lync Server 2013](lync-server-2013-configuring-for-push-notifications.md)

