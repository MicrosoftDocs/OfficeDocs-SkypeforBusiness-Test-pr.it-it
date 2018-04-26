---
title: New-CsTrustedApplicationComputer
TOCTitle: New-CsTrustedApplicationComputer
ms:assetid: 5c44a596-7fca-49d3-a7cf-e22656698a28
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398405(v=OCS.15)
ms:contentKeyID: 49300687
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplicationComputer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiunge un computer che ospita applicazioni attendibili a un pool esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsTrustedApplicationComputer -Identity <XdsGlobalRelativeIdentity> -Pool <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene aggiunto un nuovo computer con nome di dominio completo Trust1.litwareinc.com al pool TrustPool.litwareinc.com. È stato utilizzato il parametro Identity per specificare il nome di dominio completo del nuovo computer e il parametro Pool per specificare quello del pool. È necessario che il pool sia presente e che sia un pool di applicazioni attendibili. Si noti che per creare un pool di applicazioni attendibili, è necessario utilizzare il cmdlet **New-CsTrustedApplicationPool**.

    New-CsTrustedApplicationComputer -Identity Trust1.litwareinc.com -Pool TrustPool.litwareinc.com

## Descrizione dettagliata

È consigliabile che i computer che eseguono applicazioni attendibili all'interno di una distribuzione di Lync Server vengano aggiunti a un pool distinto, destinato unicamente a questo tipo di applicazioni. È tuttavia possibile aggiungere i computer con applicazioni attendibili a un pool esistente già utilizzato anche per altri scopi. Per impostazione predefinita, quando si crea un pool, viene creato anche un computer con lo stesso nome di dominio completo (FQDN) del pool. Utilizzare questo cmdlet per creare un nuovo computer e aggiungerlo a un pool.

Per fare in modo che questo cmdlet abbia esito positivo, è necessario che il pool di applicazioni attendibili sia già presente. Non è possibile inoltre aggiungere un ulteriore computer con applicazioni attendibili a un pool contenente ruoli del servizio diversi dal ruolo ExternalServer. Se ad esempio supporta anche il ruolo CentralMgmt o Registrazione avanzata, il pool può includere solo un computer con applicazioni attendibili. Se inoltre non si specifica un nome di dominio completo (FQDN) per il computer predefinito quando si crea il pool (chiamando il cmdlet **New-CsTrustedApplicationPool**), il computer avrà lo stesso FQDN del pool e non sarà possibile aggiungere un altro computer.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsTrustedApplicationComputer** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplicationComputer"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome di dominio completo del computer che ospita applicazioni attendibili.</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo del pool che ospita il computer con applicazioni attendibili. È possibile trovare pool disponibili utilizzando il cmdlet <strong>Get-CsTrustedApplicationPool</strong>.</p></td>
</tr>
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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
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

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayComputer.

## Vedere anche

#### Ulteriori risorse

[Remove-CsTrustedApplicationComputer](remove-cstrustedapplicationcomputer.md)  
[Get-CsTrustedApplicationComputer](get-cstrustedapplicationcomputer.md)  
[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)

