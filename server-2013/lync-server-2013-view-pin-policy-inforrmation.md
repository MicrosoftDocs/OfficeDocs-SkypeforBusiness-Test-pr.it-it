---
title: Visualizzare le informazioni sui criteri PIN
TOCTitle: Visualizzare le informazioni sui criteri PIN
ms:assetid: 1d48b060-d77f-44ee-b70f-3ce128aedac4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687985(v=OCS.15)
ms:contentKeyID: 49887467
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni sui criteri PIN

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile utilizzare la scheda **Criteri PIN** per visualizzare l'autenticazione PIN (Personal Identification Number) degli utenti che si connettono a Lync 2013 con telefoni IP. Per utilizzare l'autenticazione PIN, assicurarsi che l'opzione **Abilita autenticazione PIN** sia selezionata nelle impostazioni Servizio Web. Per informazioni dettagliate, vedere [Modificare le impostazioni di configurazione del servizio Web esistente](lync-server-2013-modify-existing-web-service-configuration-settings.md).

Effettuare la procedura seguente per modificare i criteri PIN a livello di utente o a livello di sito.

## Per visualizzare informazioni sui criteri PIN in Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Sicurezza**, quindi scegliere **Criteri PIN**.

4.  Nella pagina **Criteri PIN** scegliere i criteri, fare clic su **Modifica** e quindi su **Mostra dettagli**.

## Visualizzazione dei criteri PIN utilizzando i cmdlet PowerShell di Lync Server

È inoltre possibile visualizzare i criteri PIN utilizzando Windows PowerShell e il cmdlet Get-CsPinPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione dei criteri PIN

  - Per visualizzare informazioni su tutti i criteri PIN, digitare il comando seguente in Lync Server Management Shell e premere INVIO:
    
        Get-CsPinPolicy
    
    restituirà informazioni simili alle seguenti:
    
        Identity             : Global
        Description          :
        MinPasswordLength    : 5
        PINHistoryCount      : 0
        AllowCommonPatterns  : False
        PINLifetime          : 0
        MaximumLogonAttempts :

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Get-CsPinPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsPinPolicy).

## Vedere anche

#### Attività

[Modificare le impostazioni di configurazione del servizio Web esistente](lync-server-2013-modify-existing-web-service-configuration-settings.md)  
[Creare nuovi criteri per il PIN](lync-server-2013-create-a-new-pin-policy.md)

