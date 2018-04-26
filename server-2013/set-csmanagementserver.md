---
title: Set-CsManagementServer
TOCTitle: Set-CsManagementServer
ms:assetid: 6607580d-f111-4dff-961a-71525bf2e482
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398465(v=OCS.15)
ms:contentKeyID: 49300808
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsManagementServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica la porta di replica utilizzata dal servizio di gestione centrale di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsManagementServer [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReplicationServicePort <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 effettua la connessione al servizio di gestione centrale con valore Identity ManagementServer:atl-cs-001.litwareinc.com e imposta la porta del servizio di replica sul numero di porta 5076.

    Set-CsManagementServer -Identity "ManagementServer:atl-cs-001.litwareinc.com" -ReplicationServicePort 5076

## Descrizione dettagliata

Il servizio di gestione centrale è responsabile della replica dei dati tra l' archivio di gestione centrale e i computer che eseguono i servizi o i ruoli del server di Lync Server. Il servizio di gestione centrale viene eseguito in un singolo pool Front End o in un singolo server Standard Edition e facilita la replica nell'infrastruttura di Lync Server.

Il cmdlet **Set-CsManagementServer** consente di specificare la porta utilizzata dal servizio di gestione centrale per la replica.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsManagementServer** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsManagementServer"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco del servizio di gestione centrale. Ad esempio: -Identity &quot;ManagementServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>È possibile omettere il prefisso &quot;ManagementServer:&quot; quando si specifica un server di gestione centrale, ad esempio -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicationServicePort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero della porta di replica utilizzata dal servizio di gestione centrale.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsManagementServer** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Set-CsManagementServer** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayManagementServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)  
[Move-CsManagementServer](move-csmanagementserver.md)

