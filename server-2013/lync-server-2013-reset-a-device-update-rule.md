---
title: Reimpostare una regola di aggiornamento dispositivi
TOCTitle: Reimpostare una regola di aggiornamento dispositivi
ms:assetid: d1f597e7-dffd-4756-af07-10613a5d8729
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994069(v=OCS.15)
ms:contentKeyID: 52062317
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Reimpostare una regola di aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Se si desidera modificare il funzionamento di un aggiornamento sui dispositivi di test, è possibile reimpostare la regola di aggiornamento dei dispositivi, che rimuove lo stato in sospeso della regola e disinstalla l'aggiornamento dai dispositivi di test.

È possibile rimuovere una regola di aggiornamento dei dispositivi utilizzando Pannello di controllo di Lync Server o Windows PowerShell.


> [!NOTE]
> Per disinstallare una regola già approvata (ovvero distribuita), ripristinarla. Per informazioni dettagliate, vedere <A href="lync-server-2013-restore-a-device-update-rule.md">Ripristinare una regola di aggiornamento dispositivi</A>.



## Per reimpostare una regola di aggiornamento dispositivi utilizzando Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Aggiornamento dispositivi**.

4.  Nella pagina **Aggiornamento dispositivi** eseguire una delle operazioni seguenti:
    
      - Per reimpostare una regola, selezionarla.
    
      - Per reimpostare tutte le regole, scegliere **Seleziona tutto** dal menu **Modifica**.
    
      - Per reimpostare tutte le regole per un marchio, utilizzare il menu della colonna **Marca**.

5.  Fare clic su **Azione** e quindi su **Annulla aggiornamenti in sospeso**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si è certi di non voler distribuire le regole di aggiornamento dispositivi annullate, è possibile eliminarle. Per informazioni dettagliate, vedere <a href="lync-server-2013-remove-a-device-update-rule.md">Rimuovere una regola di aggiornamento dispositivi</a>.</td>
    </tr>
    </tbody>
    </table>


## Reimpostazione di una regola di aggiornamento dispositivi tramite i cmdlet di Windows PowerShell

Le regole di aggiornamento dispositivi possono essere reimpostate anche mediante Windows PowerShell e il cmdlet **Reset-CsDeviceUpdateRule**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.



## Per reimpostare una regola di aggiornamento dispositivi specifica in un server

  - Il comando seguente reimposta la regola di aggiornamento dispositivi d5ce3c10-2588-420a-82ac-dc2d9b1222ff9 sul server Web atl-cs-001.litwareinc.com:
    
        Reset-CsDeviceUpdateRule -Identity "service:WebServer:atl-cs-001.litwareinc.com/d5ce3c10-2588-420a-82ac-dc2d9b1222ff9"

## Per reimpostare tutte le regole di aggiornamento dispositivi in un server

  - Questo comando reimposta tutte le regole di aggiornamento dispositivi nel server Web atl-cs-001.litwareinc.com:
    
        Get-CsDeviceUpdateRule -Filter "service:WebServer:atl-cs-001.litwareinc.com*"  | Reset-CsDeviceUpdateRule

## Per reimpostare tutte le regole di aggiornamento dispositivi con un marchio specifico

  - In questo esempio vengono reimpostati tutti gli aggiornamenti dispositivi dell'organizzazione che dispongono del marchio Microsoft:
    
        Get-CsDeviceUpdateRule | Where-Object {$_.Brand -eq "Microsoft"} | Reset-CsDeviceUpdateRule

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Reset-CsDeviceUpdateRule](https://docs.microsoft.com/en-us/powershell/module/skype/Reset-CsDeviceUpdateRule).

## Vedere anche

#### Attività

[Approvare una regola di aggiornamento dispositivi](lync-server-2013-approve-a-device-update-rule.md)

