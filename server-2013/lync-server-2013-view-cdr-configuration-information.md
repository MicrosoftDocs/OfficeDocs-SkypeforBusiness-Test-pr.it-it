---
title: Visualizzare le informazioni sulla configurazione di registrazione dettagli chiamata
TOCTitle: Visualizzare le informazioni sulla configurazione di registrazione dettagli chiamata
ms:assetid: 77bd553f-da89-4c84-a5d0-2f7e91d04383
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688096(v=OCS.15)
ms:contentKeyID: 49887613
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni sulla configurazione di registrazione dettagli chiamata

 

_**Ultima modifica dell'argomento:** 2013-02-23_

La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle sessioni di messaggistica istantanea peer-to-peer, delle chiamate telefoniche VoIP (Voice over Internet Protocol) e delle conferenze telefoniche. Questi dati sull'utilizzo includono informazioni sui chiamanti, sugli utenti chiamati, sulla data della chiamata e sulla durata della conversazione.

Quando si installa Microsoft Lync Server 2013, viene creata automaticamente una raccolta globale singola di impostazioni di configurazione per la registrazione dettagli chiamata. Gli amministratori possono inoltre creare raccolte di impostazioni personalizzate che possono essere applicate a singoli siti. È possibile visualizzare le impostazioni di configurazione per la registrazione dettagli chiamata utilizzate nella propria organizzazione, attraverso il Pannello di controllo di Lync Server o il cmdlet [Get-CsCdrConfiguration](get-cscdrconfiguration.md).

## Visualizzare le informazioni di configurazione della registrazione dettagli chiamata attraverso Pannello di controllo di Lync Server

1.  In Pannello di controllo di Lync Server fare clic su **Monitoraggio e archiviazione**.

2.  Nella scheda **Registrazione dettagli chiamata** viene visualizzato un elenco delle impostazioni di configurazione per la registrazione dettagli chiamata; per ciascuna raccolta di impostazioni comparirà il **Nome** della raccolta, se la Registrazione dettagli chiamata è abilitata o meno (la proprietà **CDR** property), e se l'eliminazione è abilitata (la proprietà **Eliminazione CDR**). Per visualizzare informazioni dettagliate su una raccolta, fare doppio clic sulla raccolta o selezionare la raccolta appropriata, fare clic su **Modifica** e quindi su **Mostra dettagli**. Si noti che è possibile visualizzare le informazioni dettagliate per una raccolta singola di impostazioni di configurazione per la registrazione dettagli chiamata alla volta.

## Visualizzare le informazioni di configurazione della registrazione dettagli chiamata attraverso i cmdlet di Lync Server Management Shell

È inoltre possibile visualizzare le impostazioni di configurazione della registrazione dettagli chiamata utilizzando Lync Server Management Shell e il cmdlet Get-CsCdrConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzare le informazioni di configurazione della registrazione dettagli chiamata

  - Per visualizzare le informazioni relative alle impostazioni di configurazione della registrazione dettagli chiamata, digitare il seguente comando in Lync Server Management Shell e premere INVIO:
    
        Get-CsCdrConfiguration
    
    Le informazioni restituite saranno simili a questa:
    
        Identity               : Global
        EnableCDR              : True
        EnablePurging          : True
        KeepCallDetailForDays  : 90
        KeepErrorReportForDays : 60
        PurgeHourOfDay         : 2

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsCdrConfiguration](get-cscdrconfiguration.md).

