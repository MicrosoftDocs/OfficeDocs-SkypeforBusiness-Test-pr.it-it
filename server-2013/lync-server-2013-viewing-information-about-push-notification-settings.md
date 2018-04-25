---
title: Visualizzazione di informazioni sulle impostazioni di notifica Push
TOCTitle: Visualizzazione di informazioni sulle impostazioni di notifica Push
ms:assetid: be5c6b01-4294-4d17-9772-fed40201e8a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721868(v=OCS.15)
ms:contentKeyID: 49887730
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione di informazioni sulle impostazioni di notifica Push

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le notifiche Push, sotto forma di riquadri, icone o avvisi, possono essere inviate a un dispositivo mobile anche se l'applicazione per dispositivi mobili è inattiva. Le notifiche Push avvisano gli utenti in caso di eventi quali inviti a sessioni di messaggistica istantanea nuovi o senza risposta e di messaggi in segreteria telefonica. È possibile visualizzare le impostazioni delle notifiche Push per i dispositivi mobili utilizzando il Pannello di controllo di Lync Server 2013 o Lync Server 2013 Management Shell.

## Per visualizzare le informazioni relative alle notifiche Push dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione notifiche Push**.

4.  Nella pagina **Configurazione notifiche Push** fare clic sul sito che si desidera visualizzare e quindi scegliere **Mostra dettagli** dal menu **Modifica**.

## Per visualizzare le informazioni relative alla configurazione delle notifiche Push mediante i cmdlet di Windows PowerShell

È possibile visualizzare le impostazioni di configurazione delle notifiche Push anche utilizzando Lync Server Management Shell e il cmdlet **Get-CsPushNotificationConfiguration**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell oppure da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare le informazioni di configurazione delle notifiche Push

  - Per visualizzare le informazioni relative a tutte le impostazioni di configurazione delle notifiche Push, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsPushNotificationConfiguration
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity                               : Global
        EnableApplePushNotificationService     : False
        EnableMicrosoftPushNotificationService : False

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsPushNotificationConfiguration](get-cspushnotificationconfiguration.md).

## Vedere anche

#### Attività

[Configurazione delle notifiche push in Lync Server 2013](lync-server-2013-configuring-for-push-notifications.md)

