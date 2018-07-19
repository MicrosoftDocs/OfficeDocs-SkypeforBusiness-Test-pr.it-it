---
title: Approvare una regola di aggiornamento dispositivi
TOCTitle: Approvare una regola di aggiornamento dispositivi
ms:assetid: 9dbb1c9a-be0f-4e13-9234-05501ab43ac5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994053(v=OCS.15)
ms:contentKeyID: 52062255
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Approvare una regola di aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Dopo aver importato una regola di aggiornamento dispositivi, la regola viene installata nei dispositivi di prova. Se i test producono risultati corretti e si desidera distribuire l'aggiornamento nell'organizzazione, approvarlo tramite il Pannello di controllo di Lync Server o Windows PowerShell.

## Per approvare una regola di aggiornamento dispositivi tramite il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella pagina **Aggiornamento dispositivi** eseguire una delle operazioni seguenti:
    
      - Per approvare una sola regola, selezionarla.
    
      - Per approvare tutte le regole, fare clic su **Modifica** e quindi su **Seleziona tutto**.

4.  Fare clic su **Azione** e quindi su **Approva**.

## Approvazione di una regola di aggiornamento dispositivi tramite cmdlet di Windows PowerShell

Le regole di aggiornamento dispositivi possono essere approvate anche tramite Windows PowerShell e il cmdlet **Approve-CsDeviceUpdateRule**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.



## Per approvare una singola regola di aggiornamento dispositivi

  - Il comando seguente consente di approvare la regola di aggiornamento dispositivi d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 presente nel server Web atl-cs-001.litwareinc.com:
    
        Approve-CsDeviceUpdateRule -Identity service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9

## Per approvare più regole di aggiornamento dispositivi

  - Questo comando consente di approvare tutte le regole di aggiornamento dispositivi per i dispositivi con marchio Microsoft:
    
        Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "Microsoft"} | Approve-CsDeviceUpdateRule

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Approve-CsDeviceUpdateRule](https://docs.microsoft.com/en-us/powershell/module/skype/Approve-CsDeviceUpdateRule).

## Vedere anche

#### Attività

[Importare regole di aggiornamento dispositivi](lync-server-2013-import-device-update-rules.md)  
[Ripristinare una regola di aggiornamento dispositivi](lync-server-2013-restore-a-device-update-rule.md)

