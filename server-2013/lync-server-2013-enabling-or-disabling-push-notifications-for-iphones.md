---
title: Abilitazione o disabilitazione delle notifiche Push per iPhone
TOCTitle: Abilitazione o disabilitazione delle notifiche Push per iPhone
ms:assetid: 8bbf531a-807f-4a8f-814a-94bfed8f97ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688122(v=OCS.15)
ms:contentKeyID: 49887642
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione o disabilitazione delle notifiche Push per iPhone

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le notifiche push, sotto forma di notifiche, icone o avvisi, possono essere inviate a un iPhone anche se l'applicazione mobile è inattiva. Le notifiche push consentono di notificare a un utente eventi quali inviti di messaggistica immediata nuovi o senza risposta e i messaggi vocali. È possibile abilitare o disabilitare le notifiche push per iPhone mediante il Pannello di controllo di Lync Server 2013 o la Lync Server 2013 Management Shell.

## Per abilitare le notifiche push per iPhone dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione sinistra fare clic su **Client** e quindi fare clic sul pulsante **Configurazione notifiche Push**.

4.  Nella pagina **Configurazione notifiche Push** fare clic sul sito da modificare e scegliere **Mostra dettagli** dal menu **Modifica**.

5.  Selezionare la casella di controllo **Abilita notifiche push di Apple**.

6.  Fare clic su **Commit** .

## Per disabilitare le notifiche push per iPhone dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione sinistra fare clic su **Client** e quindi fare clic sul pulsante **Configurazione notifiche Push**.

4.  Nella pagina **Configurazione notifiche Push** fare clic sul sito da modificare e scegliere **Mostra dettagli** dal menu **Modifica**.

5.  Deselezionare la casella di controllo **Abilita notifiche push di Apple**.

6.  Fare clic su **Commit** .

## Per abilitare o disabilitare le notifiche push in iPhone mediante i cmdlet di Windows PowerShell

È possibile abilitare o disabilitare le notifiche push per Apple iPhone mediante il cmdlet **Set-CsPushNotificationConfiguration**. È possibile eseguire questo cmdlet dalla Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare le notifiche push per iPhone

  - Per abilitare le notifiche push per iPhone impostare il valore della proprietà EnableApplePushNotificationService su True ($True). Esempio:
    
        Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $True

## Per disabilitare le notifiche push per iPhone

  - Per disabilitare le notifiche push per iPhone impostare il valore della proprietà EnableApplePushNotificationService su False ($False). Esempio:
    
        Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $False

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsPushNotificationConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsPushNotificationConfiguration).

## Vedere anche

#### Attività

[Configurazione delle notifiche push in Lync Server 2013](lync-server-2013-configuring-for-push-notifications.md)

