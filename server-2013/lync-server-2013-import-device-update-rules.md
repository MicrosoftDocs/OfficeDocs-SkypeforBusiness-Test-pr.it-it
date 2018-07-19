---
title: Importare regole di aggiornamento dispositivi
TOCTitle: Importare regole di aggiornamento dispositivi
ms:assetid: 919e9c87-912b-4bc9-92e7-5998fc2e0bf0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994056(v=OCS.15)
ms:contentKeyID: 52062230
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Importare regole di aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Le regole di aggiornamento dispositivi possono essere importate solo mediante Windows PowerShell e il cmdlet **Import-CsDeviceUpdate**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.




## Per importare le regole di aggiornamento dispositivi in un singolo server Web

  - Il comando seguente consente di importare le regole di aggiornamento dispositivi nel server Web atl-cs-001.litwareinc.com:
    
        Import-CsDeviceUpdate -Identity "service:WebServer:atl-cs-001.litwareinc.com" -FileName C:\Updates\UCUpdates.cab

## Per importare le regole di aggiornamento dispositivi in tutti i server Web

  - In questo esempio, le regole di aggiornamento dispositivi vengono importate in tutti i server Web distribuiti nell'organizzazione. Per il funzionamento di questo comando è necessario che la cartella \\\\atl-fs-001.litwareinc.com\\Updates sia condivisa e disponibile per tutti i server Web.
    
        Get-CsService -WebServer | ForEach-Object {Import-CsDeviceUpdate -Identity $_.Identity -FileName \\atl-fs-001.litwareinc.com\Updates\UCUpdates.cab}

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Import-CsDeviceUpdate](https://docs.microsoft.com/en-us/powershell/module/skype/Import-CsDeviceUpdate).

## Vedere anche

#### Attività

[Visualizzare informazioni sulle regole di aggiornamento dispositivi](lync-server-2013-view-information-about-device-update-rules.md)  
[Approvare una regola di aggiornamento dispositivi](lync-server-2013-approve-a-device-update-rule.md)

