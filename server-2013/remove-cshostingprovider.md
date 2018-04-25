---
title: Remove-CsHostingProvider
TOCTitle: Remove-CsHostingProvider
ms:assetid: 309e472b-683c-47ed-9536-3b7aa50119d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425809(v=OCS.15)
ms:contentKeyID: 49300088
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsHostingProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove uno o più provider di hosting attualmente in uso nell'organizzazione. Un provider di hosting è un'organizzazione di terze parti che fornisce servizi di messaggistica istantanea, di presenza e altri servizi correlati per un dominio con il quale si desidera stabilire una federazione. I provider di hosting, ad esempio Microsoft Lync Online 2010, si differenziano dai provider pubblici, ad esempio Yahoo\!, MSN e AOL, in quanto non offrono servizi al pubblico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsHostingProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene eliminato il provider di hosting con identità Fabrikam.com. Dopo aver eliminato il provider di hosting, la federazione con Fabrikam.com (ed eventuali domini associati a Fabrikam.com) viene terminata.

    Remove-CsHostingProvider -Identity "Fabrikam.com"

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i provider di hosting configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsHostingProvider** per restituire una raccolta di tutti i provider di hosting attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsHostingProvider**, che elimina ogni elemento della raccolta. Al completamento del comando non vi saranno più provider di hosting configurati per l'utilizzo.

    Get-CsHostingProvider | Remove-CsHostingProvider

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i provider di hosting nella cui identità è incluso il valore stringa "Fabrikam". A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsHostingProvider** e il parametro Filter. Il valore di filtro "\*Fabrikam\*" assicura che vengano restituiti solo i dati relativi ai provider di hosting che includono "Fabrikam" nell'identità. Il comando seguente ad esempio restituisce provider come Fabrikam.com, Fabrikam.net e FabrikamUsers.com. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsHostingProvider**, che elimina ogni elemento della raccolta.

    Get-CsHostingProvider -Filter "*Fabrikam*" | Remove-CsHostingProvider

## ESEMPIO 4

Nell'esempio 4 vengono eliminati tutti i provider di hosting in cui il livello di verifica non è impostato su AlwaysVerifiable. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsHostingProvider** senza parametri aggiuntivi. Viene così restituita una raccolta di tutti i provider di hosting configurati per l'utilizzo nell'organizzazione. La raccolta risultante viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider in cui la proprietà VerificationLevel non è uguale a AlwaysVerifiable. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsHostingProvider**, che rimuove ogni provider della raccolta.

    Get-CsHostingProvider | Where-Object {$_.VerificationLevel -ne "AlwaysVerifiable"} | Remove-CsHostingProvider

## ESEMPIO 5

Nell'esempio 5 vengono rimossi tutti i provider di hosting attualmente disabilitati. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsHostingProvider** per restituire una raccolta di tutti i provider di hosting configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider disabilitati, ovvero solo i provider in cui la proprietà Enabled è uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsHostingProvider**, che elimina ogni provider di hosting disabilitato.

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsHostingProvider

## Descrizione dettagliata

La federazione consente di stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Quando si attua una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere servizi di notifica della presenza e comunicare in altro modo utilizzando applicazioni SIP come Lync 2013. Lync Server consente tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

Un provider di hosting è un'organizzazione che fornisce servizi di comunicazione SIP ad altre organizzazioni, ad esempio Fabrikam, Inc. può ospitare utenti di Contoso, Northwind Traders e Wingtip Toys. Quando si stabilisce una relazione di federazione con un provider di hosting, si definisce in realtà una federazione con tutte le organizzazioni ospitate da quel provider. Ad esempio, se un'organizzazione si associa tramite federazione a Fabrikam, gli utenti dell'organizzazione potranno scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Contoso, Northwind Traders e Wingtip Toys.

I provider di hosting vengono utilizzati anche in scenari di dominio diviso. In uno scenario di dominio diviso alcuni utenti dispongono di account ospitati in locale, ovvero nell'implementazione locale di Lync Server. Altri utenti dispongono invece di account gestiti in remoto da provider di hosting di terze parti. La federazione con il provider di hosting consente agli utenti in locale e in remoto di comunicare tra loro.

Per attuare la federazione con un provider di hosting di terze parti, è necessario creare e abilitare un nuovo provider di hosting. Il provider di terze parti inoltre dovrà creare una relazione di federazione con l'organizzazione. Se si decide più avanti di terminare questa relazione, è possibile utilizzare il cmdlet **Remove-CsHostingProvider** per eliminare il provider di hosting. Quando si elimina un provider di hosting, questo viene rimosso dall'elenco dei partner federati. A quel punto, l'unico modo per ristabilire la relazione è ricreare il provider. Se invece si desidera sospendere temporaneamente una relazione, è possibile utilizzare il cmdlet **Disable-CsHostingProvider**. Quando un provider di hosting viene disabilitato, non viene eliminato dall'elenco dei partner federati, ma viene semplicemente contrassegnato come disabilitato e la comunicazione tra l'organizzazione e il provider risulta disabilitata. Per ristabilire la relazione, è possibile utilizzare il cmdlet **Enable-CsHostingProvider** per abilitare di nuovo il provider.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsHostingProvider** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsHostingProvider"}

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
<td><p>Identificatore univoco del provider di hosting da rimuovere. L'identità è un valore stringa, ad esempio, può essere il nome di dominio completo (FQDN) per provider di hosting (ad esempio fabrikam.com) o il nome dell'azienda che fornisce i servizi (Fabrikam, Inc.).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider. Il cmdlet **Remove-CsHostingProvider** accetta le istanze dell'oggetto provider di hosting inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet, invece, consente di eliminare le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

