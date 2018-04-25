---
title: Get-CsTrustedApplicationComputer
TOCTitle: Get-CsTrustedApplicationComputer
ms:assetid: 360796d8-48c7-4ce2-9bb4-1f8967562f24
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425843(v=OCS.15)
ms:contentKeyID: 49300163
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplicationComputer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su uno o più computer che ospitano applicazioni attendibili. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsTrustedApplicationComputer [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsTrustedApplicationComputer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Local <SwitchParameter>] [-Pool <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperati tutti i computer assegnati a un pool di applicazioni attendibili all'interno della distribuzione di Lync Server.

    Get-CsTrustedApplicationComputer

## ESEMPIO 2

Nell'esempio 2 vengono recuperate le informazioni sul computer con nome di dominio completo (FQDN) Trust1.litwareinc.com.

    Get-CsTrustedApplicationComputer -Identity Trust1.litwareinc.com

## ESEMPIO 3

In questo esempio viene utilizzato il parametro Filter per eseguire una ricerca con caratteri jolly di tutti i computer con nome di dominio completo (FQDN) che inizia con la stringa Trust, assegnata ai pool di applicazioni attendibili. Il parametro Filter ricerca la proprietà Identity di tutti i computer con applicazioni attendibili. Il carattere jolly (\*) alla fine della stringa indica che il parametro Filter deve ricercare le identità che iniziano con la stringa Trust seguita da un carattere qualsiasi.

    Get-CsTrustedApplicationComputer -Filter Trust*

## ESEMPIO 4

Nell'esempio 4 viene recuperato un elenco di tutti i computer assegnati al pool di applicazioni attendibili TrustPool.litwareinc.com.

    Get-CsTrustedApplicationComputer -Pool TrustPool.litwareinc.com

## ESEMPIO 5

Nell'esempio 3 è stato utilizzato il parametro Filter per eseguire una ricerca con caratteri jolly in base al valore Identity, ovvero all'FQDN del computer. In questo esempio la ricerca con caratteri jolly viene però eseguita in base al pool anziché in base all'identità. È innanzitutto necessario chiamare il cmdlet **Get-CsTrustedApplicationComputer** per recuperare una raccolta di tutti i computer con applicazioni attendibili. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** consente di circoscrivere la raccolta che gli è stata inviata tramite pipe. In questo caso, si desidera ottenere unicamente i computer con applicazioni attendibili presenti nei pool del dominio litwareinc.com. A tale scopo, viene verificata la proprietà Pool di ogni elemento della raccolta ($\_.Pool) per determinare se corrisponde (-like) alla stringa con caratteri jolly \*.litwareinc.com. Un valore corrisponde a tale stringa se inizia con una qualsiasi serie di caratteri e termina con la stringa .litwareinc.com.

    Get-CsTrustedApplicationComputer | Where-Object {$_.Pool -like "*.litwareinc.com"}

## Descrizione dettagliata

È consigliabile aggiungere i computer che eseguono applicazioni attendibili in una distribuzione di Lync Server a un pool distinto, destinato unicamente a questo tipo di applicazioni. È tuttavia possibile aggiungere i computer con applicazioni attendibili a un pool esistente già utilizzato anche per altri scopi. Utilizzare questo cmdlet per recuperare il parametro Identity (FQDN) e il relativo pool per uno o più computer contenenti applicazioni attendibili.

È possibile utilizzare questo cmdlet per recuperare i computer in base al nome di dominio completo (FQDN) del computer o per recuperare tutti i computer facenti parte di un pool specifico.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsTrustedApplicationComputer** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplicationComputer"}

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
<td><p>Una stringa che include i caratteri jolly e che consente di recuperare i computer attendibili in base ai valori Identity corrispondenti alla stringa di caratteri jolly specificata.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome di dominio completo (FQDN) del computer da recuperare.</p></td>
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
<td><p>Nome di dominio completo (FQDN) del pool di applicazioni attendibili per il quale si desidera recuperare le informazioni sul computer.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Recupera uno o più oggetti di tipo Microsoft.Rtc.Management.Xds.DisplayComputer.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)  
[Remove-CsTrustedApplicationComputer](remove-cstrustedapplicationcomputer.md)

