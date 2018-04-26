---
title: Enable-CsPublicProvider
TOCTitle: Enable-CsPublicProvider
ms:assetid: 98370dfd-9a53-41a8-a1f3-bb7a516c3c5e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398780(v=OCS.15)
ms:contentKeyID: 49301402
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita un provider pubblico configurato per l'utilizzo nell'organizzazione. Un provider pubblico è un'organizzazione che offre al grande pubblico servizi di messaggistica istantanea, presenza e altri servizi correlati. Lync Server viene fornito con tre provider pubblici configurati, ma non abilitati: Yahoo\!, AIM (AOL) e Messenger (MSN). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 abilita il provider pubblico con l'identità Messenger. Se Messenger è già abilitato, il comando restituirà un errore.

    Enable-CsPublicProvider -Identity "Messenger"

## ESEMPIO 2

Nell'esempio 2 vengono abilitati tutti i provider pubblici attualmente disabilitati. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici configurati per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider in cui la proprietà Enabled è uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Enable-CsPublicProvider**, che abilita ogni provider della raccolta.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsPublicProvider

## ESEMPIO 3

Nell'esempio 3 vengono abilitati tutti i provider pubblici che attualmente non sono abilitati, purché il livello di verifica di tali provider sia impostato su AlwaysVerifiable. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici attualmente in uso nell'organizzazione. Questa raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona i provider che soddisfano i due criteri seguenti: 1) la proprietà VerificationLevel equivale a AlwaysVerifiable e 2) la proprietà Enabled è uguale a False. L'operatore -and indica al cmdlet **Where-Object** che gli oggetti dovranno essere selezionati solo se soddisfano tutti i criteri specificati. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Enable-CsPublicProvider**, che abilita tutti i provider in essa contenuti.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -eq "AlwaysVerifiable" -and $_.Enabled -eq $False} | Enable-CsPublicProvider

## Descrizione dettagliata

La federazione è un mezzo tramite il quale due organizzazioni possono stabilire una relazione di trust che facilita la comunicazione tra i due gruppi. Quando viene creata una federazione, gli utenti delle due organizzazioni possono scambiarsi messaggi istantanei, sottoscrivere le notifiche della presenza e comunicare tra loro in altri modi utilizzando applicazioni SIP, ad esempio Lync 2013. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

Un provider pubblico è un'organizzazione che fornisce servizi di comunicazione SIP al grande pubblico. Quando si stabilisce una relazione di federazione con un provider pubblico, in realtà si stabilisce una federazione con qualsiasi utente che disponga di un account ospitato da tale provider. Ad esempio, se si stabilisce una federazione con Messenger (MSN), gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di ﻿messaggistica istantanea di MSN Messenger.

Per poter stabilire una federazione con un provider pubblico, è necessario crearne e abilitarne uno nuovo, e il provider pubblico dovrà creare una relazione di federazione con l'utente o l'organizzazione. È possibile abilitare i provider pubblici al momento della creazione oppure una volta stabilita la federazione tramite il cmdlet **Enable-CsPublicProvider**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Enable-CsPublicProvider** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsPublicProvider"}

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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Un identificatore univoco per il provider pubblico da abilitare. L'identità è in genere il nome del sito Web che fornisce i servizi (ad esempio Yahoo!, AOL o MSN).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DisplayPublicProvider</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. Il cmdlet **Enable-CsPublicProvider** accetta istanze dell'oggetto provider pubblico inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet, invece, consente di abilitare le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

