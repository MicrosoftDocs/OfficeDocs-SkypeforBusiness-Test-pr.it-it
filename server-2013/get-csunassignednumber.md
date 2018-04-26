---
title: Get-CsUnassignedNumber
TOCTitle: Get-CsUnassignedNumber
ms:assetid: a8e5cfc1-e7a0-4917-9cd9-f541fedb3a61
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412792(v=OCS.15)
ms:contentKeyID: 49301598
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUnassignedNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più intervalli di numeri non assegnati e le regole di routing applicabili a tali numeri. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsUnassignedNumber [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene restituita una raccolta di tutti i numeri non assegnati configurati per l'utilizzo nell'organizzazione.

    Get-CsUnassignedNumber

## ESEMPIO 2

Nell'esempio 2 il parametro Identity viene utilizzato per limitare i dati restituiti ai numeri non assegnati con Identity UNSet1. Poiché le identità devono essere univoche, il comando restituirà solo l'intervallo di numeri non assegnati specificato.

    Get-CsUnassignedNumber -Identity UNSet1

## ESEMPIO 3

In questo esempio viene utilizzato il parametro Filter per restituire una raccolta di tutte le impostazioni di numeri non assegnati il cui valore Identity include la stringa Redmond. Ad esempio, questo comando restituisce le impostazioni dei numeri non assegnati con identità, quali Redmond Numbers, Unassigned Redmond Numbers, UNRedmond, ecc.

    Get-CsUnassignedNumber -Filter *Redmond*

## ESEMPIO 4

Nell'esempio 4 vengono utilizzati i cmdlet **Get-CsUnassignedNumber** e **Where-Object** per recuperare una raccolta di tutte le impostazioni di numeri non assegnati che includono la parola Welcome nel nome dell'annuncio. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsUnassignedNumber** per recuperare tutte le impostazioni dei numeri non assegnati. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro che circoscrive i dati restituiti limitandoli ai numeri non assegnati che includono la parola Welcome nel nome dell'annuncio assegnato.

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"}

## Descrizione dettagliata

I numeri non assegnati sono numeri di telefono che sono stati assegnati a un'organizzazione, ma non a utenti o telefoni specifici. È possibile configurare Lync Server in modo da instradare le chiamate alle destinazioni appropriate quando viene chiamato un numero non assegnato. Questo cmdlet recupera uno o più intervalli di numeri non assegnati che definiscono questo routing.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsUnassignedNumber** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmin. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUnassignedNumber"}

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
<td><p>Esegue una ricerca con caratteri jolly che consente di limitare i risultati unicamente alle impostazioni dei numeri non assegnati le cui identità corrispondono alla stringa con caratteri jolly data.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome univoco dell'intervallo di numeri non assegnati da recuperare.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative ai numeri non assegnati dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange.

## Vedere anche

#### Ulteriori risorse

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)

