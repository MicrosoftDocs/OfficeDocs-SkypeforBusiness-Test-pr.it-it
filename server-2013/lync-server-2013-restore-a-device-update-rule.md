---
title: Ripristinare una regola di aggiornamento dispositivi
TOCTitle: Ripristinare una regola di aggiornamento dispositivi
ms:assetid: ac490baf-c7a0-48d9-8fd0-ba5729489341
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994061(v=OCS.15)
ms:contentKeyID: 52062291
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristinare una regola di aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Per disinstallare una regola di aggiornamento dispositivi dai dispositivi della distribuzione, è necessario ripristinarla. Ripristinando una regola di aggiornamento dispositivi, viene disinstallato l'aggiornamento e viene reinstallata la versione precedente della regola.

È possibile ripristinare una regola di aggiornamento dispositivi utilizzando Pannello di controllo di Lync Server o Windows PowerShell.

## Per ripristinare le regole di aggiornamento dispositivi utilizzando il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Aggiornamento dispositivi**.

4.  Nella pagina **Aggiornamento dispositivi** eseguire una delle operazioni seguenti:
    
      - Per ripristinare una regola, selezionarla.
    
      - Per ripristinare tutte le regole, scegliere **Seleziona tutto** dal menu **Modifica**.

5.  Fare clic su **Azione** e scegliere **Ripristina**.

## Ripristino delle regole di aggiornamento dispositivi tramite i cmdlet di Windows PowerShell

Le regole di aggiornamento dispositivi possono essere ripristinate anche mediante Windows PowerShell e il cmdlet **Restore-CsDeviceUpdateRule**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.



## Per ripristinare una singola regola di aggiornamento dispositivi in un server

  - Il comando seguente ripristina la regola di aggiornamento dispositivi d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 nel server Web atl-cs-001.litwareinc.com:
    
        Restore-CsDeviceUpdateRule -Identity "service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9"

## Per ripristinare tutte le regole di aggiornamento dispositivi in un server

  - Questo comando ripristina tutte le regole di aggiornamento dispositivi nel server Web atl-cs-001.litwareinc.com:
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*" | Restore-CsDeviceUpdateRule

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Restore-CsDeviceUpdateRule](https://docs.microsoft.com/en-us/powershell/module/skype/Restore-CsDeviceUpdateRule).

