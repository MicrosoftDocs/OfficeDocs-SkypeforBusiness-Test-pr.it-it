---
title: Rimuovere una regola di aggiornamento dispositivi
TOCTitle: Rimuovere una regola di aggiornamento dispositivi
ms:assetid: ad6e0c6a-cda4-4147-92d5-48bc393ac456
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994066(v=OCS.15)
ms:contentKeyID: 52062292
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere una regola di aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Una regola di aggiornamento dispositivi, se rimossa, viene definitivamente eliminata dalla coda di aggiornamenti dei dispositivi.

La rimozione di una regola è un'operazione diversa dalla disinstallazione di un aggiornamento dai dispositivi della distribuzione o dai dispositivi di test. Per disinstallare un aggiornamento approvato dalla distribuzione, è necessario *ripristinare* la regola di aggiornamento dispositivi. Per informazioni dettagliate, vedere [Ripristinare una regola di aggiornamento dispositivi](lync-server-2013-restore-a-device-update-rule.md). Per disinstallare un aggiornamento non approvato dai dispositivi di test, è necessario *reimpostarlo*. Per informazioni dettagliate, vedere [Reimpostare una regola di aggiornamento dispositivi](lync-server-2013-reset-a-device-update-rule.md).

È possibile rimuovere una regola di aggiornamento dispositivi utilizzando Pannello di controllo di Lync Server o Windows PowerShell.

## Per rimuovere le regole di aggiornamento dispositivi utilizzando il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Aggiornamento dispositivi**.

4.  Nella pagina **Aggiornamento dispositivi** eseguire una delle operazioni seguenti:
    
      - Per rimuovere una regola, selezionarla.
    
      - Per rimuovere tutte le regole, scegliere **Seleziona tutto** dal menu **Modifica**.

5.  Fare clic su **Modifica** e quindi scegliere **Elimina**.

## Rimozione di regole di aggiornamento dispositivi tramite i cmdlet di Windows PowerShell

Le regole di aggiornamento dispositivi possono essere rimosse anche mediante Windows PowerShell e il cmdlet **Remove-CsDeviceUpdateRule**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere una singola regola di aggiornamento dei dispositivi da un server

  - Il comando seguente rimuove la regola di aggiornamento dispositivi d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 dal server Web su atl-cs-001.litwareinc.com.
    
        Remove-CsDeviceUpdateRule -Identity "service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9"

## Per rimuovere tutte le regole di aggiornamento dispositivi da un server

  - Questo comando rimuove tutte le regole di aggiornamento dispositivi dal server Web su atl-cs-001.litwareinc.com:
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*" | Remove-CsDeviceUpdateRule

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Remove-CsDeviceUpdateRule](remove-csdeviceupdaterule.md).

## Vedere anche

#### Attività

[Approvare una regola di aggiornamento dispositivi](lync-server-2013-approve-a-device-update-rule.md)

