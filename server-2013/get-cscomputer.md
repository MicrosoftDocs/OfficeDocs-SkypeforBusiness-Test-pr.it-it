---
title: Get-CsComputer
TOCTitle: Get-CsComputer
ms:assetid: 493931a9-1670-4a76-abba-7d3c7723d2e1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425959(v=OCS.15)
ms:contentKeyID: 49300443
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsComputer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui computer che eseguono i ruoli del servizio all'interno dell'infrastruttura di Lync Server in uso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Get-CsComputer** viene utilizzato per restituire informazioni su tutti i computer che eseguono i ruoli del servizio all'interno dell'infrastruttura di Lync Server in uso.

    Get-CsComputer

## ESEMPIO 2

Con il comando mostrato nell'esempio 2 viene utilizzato il parametro Filter per restituire unicamente i computer dei ruoli del servizio che fanno parte del dominio litwareinc.com. La stringa con caratteri jolly \*.litwareinc.com limita le informazioni restituite ai computer con nome di dominio completo (FQDN) che termina con il valore stringa ".litwareinc.com".

    Get-CsComputer -Filter "*.litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 il parametro Identity viene utilizzato per limitare i dati restituiti al computer con FQDN atl-cs-001.litwareinc.com.

    Get-CsComputer -Identity "atl-cs-001.litwareinc.com"

## ESEMPIO 4

Con l'esempio 4 viene utilizzato il parametro Pool per restituire informazioni su tutti i computer trovati nel pool atl-cs-001.litwareinc.com.

    Get-CsComputer -Pool "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Get-CsComputer** consente di identificare rapidamente i computer che eseguono ruoli del server o servizi di Lync Server. Se chiamato senza parametri, il cmdlet **Get-CsComputer** restituisce una raccolta di tutti i computer che eseguono ruoli del server o servizi di Lync Server. La raccolta include l'identità, il nome del pool e il nome di dominio completo (FQDN) di ogni computer. In alternativa, è possibile utilizzare parametri facoltativi come Identity, Filter o Pool per restituire solo i dati relativi a un singolo computer o a un insieme di computer.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsComputer** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare caratteri jolly per specificare l'identità del computer, o dei computer, da restituire. Ad esempio, questo comando restituisce informazioni su tutti i computer la cui identità inizia con il valore stringa &quot;atl-&quot;: -Filter &quot;atl-*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo del computer da restituire. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Se questo parametro non viene specificato, vengono restituiti tutti i computer che eseguono Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>Local</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, vengono restituite solo le informazioni relative al computer locale.</p></td>
</tr>
<tr class="even">
<td><p><em>Pool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>FQDN di un pool di Lync Server. Se si utilizza questo parametro, vengono restituite informazioni su tutti i computer presenti nel pool specificato.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsComputer** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsComputer** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.Machine.

## Vedere anche

#### Ulteriori risorse

[Disable-CsComputer](disable-cscomputer.md)  
[Enable-CsComputer](enable-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

