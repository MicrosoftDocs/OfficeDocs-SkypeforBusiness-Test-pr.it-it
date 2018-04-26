---
title: 'Lync Server 2013: Installazione di Windows PowerShell 3.0'
TOCTitle: Installazione di Windows PowerShell 3.0
ms:assetid: d87bf21e-0a43-41cb-8fdc-626cedec8538
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205328(v=OCS.15)
ms:contentKeyID: 49302155
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione di Windows PowerShell 3.0 per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-06-27_

Per distribuire correttamente Lync Server 2013, è necessario installare Windows PowerShell 3.0 su ciascun computer che fa parte della topologia di Lync Server.

Per i sistemi che eseguono Windows Server 2012 o Windows Server 2012 R2, questo passaggio non è più necessario ed è possibile continuare con la fase successiva della distribuzione, perché PowerShell 3.0 è incluso in questi sistemi operativi.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per i sistemi che eseguono Windows Server 2008 R2 SP1, invece, sarà necessario installare PowerShell 3.0 come prerequisito prima di installare Lync Server 2013. In caso contrario si verificheranno problemi di funzionamento. Per installare PowerShell 3.0, vedere <a href="http://go.microsoft.com/fwlink/p/?linkid=329800">Windows Management Framework 3.0</a>. Questo è un collegamento diretto alla pagina di download di PowerShell 3.0, con informazioni per l'installazione corretta di questo strumento.</td>
</tr>
</tbody>
</table>


Dopo aver completato l'installazione o se si vuole semplicemente controllare prima di continuare con la distribuzione di Lync Server, la verifica della disponibilità di PowerShell 3.0 in un server è piuttosto semplice con questa procedura:

1.  Nel server in cui eseguire il controllo fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Accessori**, **Windows PowerShell** e quindi **Windows PowerShell**.

2.  Al prompt dei comandi nella console di Windows PowerShell digitare il comando seguente e quindi premere INVIO:
    
        Get-Host | Select-Object Version

3.  Se Windows PowerShell 3.0 è installato, verrà restituito un output simile al seguente:
    
        Version
        -------
        3.0

