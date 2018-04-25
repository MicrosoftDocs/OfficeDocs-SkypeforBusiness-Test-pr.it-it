---
title: Get-CsTopology
TOCTitle: Get-CsTopology
ms:assetid: ad52f545-b8dd-411e-8584-b6e29fe8ef18
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412824(v=OCS.15)
ms:contentKeyID: 49301644
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTopology

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sull'infrastruttura di Lync Server, inclusi domini interni, siti, cluster, computer, servizi e istanze back-end di SQL Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsTopology [-AsXml <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituiti dettagli completi per la topologia di Lync Server. A tale scopo, viene chiamato il cmdlet **Get-CsTopology** senza parametri aggiuntivi.

    Get-CsTopology

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni sui computer rilevati nella topologia di Lync Server. A tale scopo, questo comando chiama innanzitutto il cmdlet **Get-CsTopology** per restituire la topologia di Lync Server completa. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per estrarre e visualizzare informazioni dettagliate per tutti i computer inclusi in tale topologia.

    Get-CsTopology | Select-Object -ExpandProperty Machines

## ESEMPIO 3

Il comando illustrato nell'esempio 3 restituisce informazioni sulla topologia di Lync Server e quindi salva tali informazioni in un file XML. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsTopology** insieme al parametro AsXml. In questo modo vengono restituiti dati XML formattati. Tali dati formattati vengono quindi inviati tramite pipe al cmdlet **Out-File**, che salva le informazioni nel file C:\\Logs\\Topology.xml.

    Get-CsTopology -AsXML | Out-File C:\Logs\Topology.xml

## Descrizione dettagliata

Il cmdlet **Get-CsTopology** restituisce informazioni su come è stato installato e configurato Lync Server. Se chiamato senza alcun parametro aggiuntivo, il cmdlet fornisce una panoramica dell'infrastruttura di Lync Server. In questo scenario il cmdlet offre una visione generale di elementi quali domini, siti e computer che eseguono servizi e ruoli del server di Lync Server. In alternativa, è possibile passare l'output del cmdlet **Get-CsTopology** al cmdlet **Select-Object**. In questo modo è possibile accedere a informazioni dettagliate su una parte della topologia. Il comando seguente ad esempio fornisce informazioni dettagliate sulle istanze di SQL Server utilizzate da Lync Server:

Get-CsTopology | Select-Object –ExpandProperty SqlInstances

È anche possibile utilizzare il parametro AsXml per restituire informazioni dettagliate sull'intera topologia in formato XML.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsTopology** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins.

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AsXml</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sulla topologia in formato XML. Combinando il cmdlet <strong>Get-CsTopology</strong>, il parametro AsXml e il cmdlet <strong>Out-File</strong>, è possibile esportare la topologia in un file XML.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati della topologia dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsTopology** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsTopology** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology.

## Vedere anche

#### Ulteriori risorse

[Enable-CsTopology](enable-cstopology.md)  
[Publish-CsTopology](publish-cstopology.md)  
[Test-CsTopology](test-cstopology.md)

