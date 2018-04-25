---
title: Disable-CsPublicProvider
TOCTitle: Disable-CsPublicProvider
ms:assetid: df1338ea-fe6d-45da-a39c-86108bb54ef5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398984(v=OCS.15)
ms:contentKeyID: 49302216
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsPublicProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Disabilita un provider pubblico configurato per l'utilizzo nell'organizzazione. Un provider pubblico è un'organizzazione che offre al grande pubblico servizi di messaggistica istantanea, presenza e altri servizi correlati. Lync Server viene fornito con tre provider pubblici configurati, ma non abilitati: Yahoo, AIM (AOL) e Messenger (MSN). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Disable-CsPublicProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Disable-CsPublicProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene disabilitato il provider pubblico con identità Messenger. Se MSN è già disabilitato, il comando restituirà un errore.

    Disable-CsPublicProvider -Identity "Messenger"

## ESEMPIO 2

In questo esempio vengono disabilitati tutti i provider pubblici attualmente abilitati. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider in cui la proprietà Enabled è uguale a True. La raccolta filtrata a sua volta viene inviata tramite pipe al cmdlet **Disable-CsPublicProvider**, che disabilita ogni provider presente nella raccolta.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $True} | Disable-CsPublicProvider

## ESEMPIO 3

Il comando mostrato nell'esempio 3 disabilita tutti i provider pubblici attualmente abilitati e il cui livello di verifica è impostato su AlwaysVerifiable. Per eseguire questa attività, nel comando viene innanzitutto chiamato il cmdlet **Get-CsPublicProvider** per restituire una raccolta di tutti i provider pubblici attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona i provider che soddisfano due criteri: 1) la proprietà VerificationLevel è uguale a AlwaysVerifiable e 2) la proprietà Enabled è uguale a True. L'operatore -and indica al cmdlet **Where-Object** che gli oggetti saranno selezionati solo se soddisfano tutti i criteri specificati. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Disable-CsPublicProvider**, che disabilita ogni provider presente nella raccolta.

    Get-CsPublicProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable" -and $_.Enabled -eq $True} | Disable-CsPublicProvider

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Una volta stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere l'opzione per notifiche di presenza e comunicare tra loro in altri modi utilizzando le applicazioni SIP come Lync 2013. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico; e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

Un provider pubblico è un'organizzazione che offre al pubblico servizi di comunicazione SIP (Session Initiation Protocol). Quando si stabilisce una relazione di federazione con un provider pubblico, in realtà si stabilisce una federazione con qualsiasi utente che disponga di un account ospitato da tale provider. Ad esempio, se si stabilisce una federazione con Messenger (MSN), gli utenti potranno scambiare messaggi istantanei e informazioni sulla presenza con chiunque disponga di un account di ﻿messaggistica istantanea Messenger.

Per poter stabilire una federazione con un provider pubblico, è necessario crearne e abilitarne uno nuovo, e il provider pubblico dovrà creare una relazione di federazione con l'utente o l'organizzazione. Quando si crea un provider pubblico, vi è la possibilità di abilitare o disabilitare la relazione federativa. Se un provider viene abilitato, gli utenti presenti nell'organizzazione potranno scambiare messaggi istantanei e informazioni sulla presenza con persone che sono titolari di account con il provider pubblico. Se un provider pubblico viene disabilitato, non sarà più possibile comunicare con i titolari di account con il provider pubblico in questione; tale condizione persisterà fino a quando il provider non verrà nuovamente abilitato. Se è necessario sospendere temporaneamente la relazione con un provider, utilizzare il cmdlet **Disable-CsPublicProvider**. Se si preferisce eliminare del tutto il provider, utilizzare il cmdlet **Remove-CsPublicProvider**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Disable-CsPublicProvider** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsPublicProvider"}

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
<td><p>Identificatore univoco per il provider pubblico da disabilitare. l'identità in genere corrisponde al nome del sito Web che fornisce i servizi, ad esempio Yahoo!, AOL, MSN e così via.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider. Il cmdlet **Disable-CsPublicProvider** accette istanze da pipeline dell'oggetto provider pubblico.

## Tipi restituiti

Nessuno. Questo cmdlet piuttosto disabilita le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider.

## Vedere anche

#### Ulteriori risorse

[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Remove-CsPublicProvider](remove-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)

