---
title: 'Lync Server 2013: Appendice A: utilizzo dei cmdlet per distribuire un Survivable Branch Appliance'
TOCTitle: 'Appendice A: utilizzo dei cmdlet per distribuire un Survivable Branch Appliance'
ms:assetid: 796a26cf-7ec9-453b-8757-6153a6dd86c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398598(v=OCS.15)
ms:contentKeyID: 49301056
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Appendice A: utilizzo dei cmdlet per distribuire un Survivable Branch Appliance in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-07_

Questo argomento illustra come distribuire un Survivable Branch Appliance attraverso Lync Server Management Shell. Eseguire questa procedura nel sito centrale.

## Per distribuire un Survivable Branch Appliance in remoto

1.  Per aggiungere un sito derivato, seguire la procedura in [Aggiungere siti di succursale alla topologia in Lync Server 2013](lync-server-2013-add-branch-sites-to-your-topology.md).

2.  Aggiungere il sito derivato al dominio.

3.  Aggiungere il gruppo RTCUniversalSBATechnicians al gruppo Administrators locale.

4.  Riavviare il server e accedervi con un account membro del gruppo RTCUniversalSBATechnicians.

5.  In Lync Server Management Shell digitare i comandi seguenti, sostituendo segnaposto con le informazioni corrette per l'organizzazione:
    
        Export-CsConfiguration -FileName C:\CSConfig.zip
        Import-CsConfiguration -LocalStore -FileName C:\CSConfig.zip -Verbose
        Enable-CSReplica -Verbose
        Enable-CsComputer -Verbose
        Request-CsCertificate -New -Type default -CA <YourCA> -Verbose
        Set-CsCertificate -Type Default -Thumbprint <YourCertThumbprint>
        Start-cswindowsservice -verbose

