---
title: Get-CsPstnUsage
TOCTitle: Get-CsPstnUsage
ms:assetid: 9dc82b88-303b-4678-8298-0dbc769f6781
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412734(v=OCS.15)
ms:contentKeyID: 49301494
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPstnUsage

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui record di utilizzo PSTN (Public Switched Telephone Network) in uso nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPstnUsage [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Questo comando restituisce l'elenco degli utilizzi globali della rete PSTN disponibili nell'organizzazione.

    Get-CsPstnUsage

## ESEMPIO 2

In questo esempio il comando restituisce un elenco di tutti gli utilizzi PSTN definiti, con ogni utilizzo elencato su una riga di output. La chiamata al cmdlet **Get-CsPstnUsage** restituisce il valore Identity e l'elenco degli utilizzi (Usage). Se l'elenco degli utilizzi include più di tre o quattro voci, verrà abbreviato nell'output in modo simile al seguente:

Usage : {Internal, Local, Long Distance, International...}

Utilizzare il comando di questo esempio per visualizzare solo un elenco di utilizzi. L'output sarà simile a questo:

Internal

Local

Long Distance

International

Restricted

    (Get-CsPstnUsage).Usage

## ESEMPIO 3

Questo comando restituisce tutti i nomi di utilizzo della rete PSTN che contengono la stringa "tern" all'interno del nome. Ad esempio, questo comando restituirà l'indicazione "Internal" e "International", ma non "Local" o "Long Distance".

La prima parte di questo comando è il cmdlet **Get-CsPstnUsage** tra parentesi e ciò significa che come prima cosa verranno recuperati tutti gli utilizzi della rete PSTN. La proprietà .Usage restituisce solo le informazioni di utilizzo per gli utilizzi della rete PSTN, ma non il valore Identity. L'elenco degli utilizzi è quindi inviato tramite pipe al cmdlet **ForEach-Object** che legge le stringhe di utilizzo una alla volta. L'istruzione If confronta la stringa di utilizzo corrente alla stringa "\*tern\*" (i simboli \* sono caratteri jolly) e visualizza le occorrenze che corrispondono a questo motivo.

    (Get-CsPstnUsage).Usage | ForEach-Object {if ($_ -like "*tern*") {$_}}

## Descrizione dettagliata

Gli utilizzi della rete PSTN sono valori stringa utilizzati per l'autorizzazione delle chiamate. Un utilizzo delle rete PSTN collega un criterio vocale a una route. Il cmdlet **Get-CsPstnUsage** consente di recuperare l'elenco di tutti gli utilizzi della rete PSTN disponibili nell'organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsPstnUsage** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPstnUsage"}

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
<td><p>Il parametro Filter consente di recuperare solo gli utilizzi della rete PSTN con un valore Identity che corrisponde a una determinata stringa di caratteri jolly. Tuttavia, l'unico valore Identity disponibile per gli utilizzi della rete PSTN è Global e di conseguenza questo parametro non è utilizzato con questo cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Il livello di applicazione di queste impostazioni. L'unica identità che può essere applicata agli utilizzi della rete PSTN è Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ottenere le informazioni sugli utilizzi della rete PSTN dall'archivio dati locale piuttosto che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsPstnUsage** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PSTNUsages.

## Vedere anche

#### Ulteriori risorse

[Set-CsPstnUsage](set-cspstnusage.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

