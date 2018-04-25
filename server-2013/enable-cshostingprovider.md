---
title: Enable-CsHostingProvider
TOCTitle: Enable-CsHostingProvider
ms:assetid: 0ba76785-6c6d-4ee6-9418-5c77b2cbaedf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398166(v=OCS.15)
ms:contentKeyID: 49299645
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsHostingProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita un provider di hosting per l'utilizzo nella propria organizzazione. Un provider di hosting è un'organizzazione di terze parti che fornisce servizi di messaggistica istantanea, informazioni sulla presenza e altri servizi correlati a un dominio con il quale si desidera attuare una federazione. I provider di hosting come Microsoft Lync Online 2010 si differenziano dai provider pubblici, ad esempio Yahoo\!, MSN e AOL, in quanto non offrono servizi al pubblico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsHostingProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Enable-CsHostingProvider [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'Esempio 1, viene abilitato il provider di hosting con Identity Fabrikam.com. Si noti che questo comando restituisce un errore, se Fabrikam.com è già stato abilitato.

    Enable-CsHostingProvider -Identity Fabrikam.com

## ESEMPIO 2

Nell'esempio 2 viene mostrato come abilitare tutti i provider di hosting attualmente disabilitati. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsHostingProvider** senza parametri aggiuntivi per restituire una raccolta di tutti i provider di hosting attualmente configurati per l'utilizzo nell'organizzazione. La raccolta così ottenuta viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona i provider in cui la proprietà Enabled è uguale a False. Per definizione, si tratta di qualsiasi provider attualmente disabilitato. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Enable-CsHostingProvider**, che abilita ogni provider incluso nella raccolta.

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $False} | Enable-CsHostingProvider

## ESEMPIO 3

Nell'esempio 3 vengono abilitati per l'utilizzo tutti i provider di hosting utilizzati in una configurazione di "dominio diviso". Un dominio diviso è un dominio in cui alcuni account di Lync Server dell'organizzazione vengono gestiti localmente e altri account vengono gestiti dal provider di hosting. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsHostingProvider** per restituire una raccolta di tutti i provider di hosting attualmente configurati. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i provider che soddisfano due criteri: 1) la proprietà EnabledSharedAddressSpace è uguale a True e 2) la proprietà Enabled è uguale a False. A questo punto, la raccolta filtrata viene inviata tramite pipe al cmdlet **Enable-CsHostingProvider**, che abilita ogni provider incluso nella raccolta.

    Get-CsHostingProvider | Where-Object {$_.EnabledSharedAddressSpace -eq $True -and $_.Enabled -eq $False} | Enable-CsHostingProvider

## Descrizione dettagliata

La federazione consente a due organizzazioni di instaurare una relazione di trust che facilita la comunicazione tra i due gruppi. Quando si attua una federazione, gli utenti delle due organizzazioni federate possono inviarsi messaggi istantanei, sottoscrivere servizi di notifica della presenza e comunicare in altro modo utilizzando applicazioni SIP come Lync 2013. Lync Server consente tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

Un provider di hosting è un'organizzazione che fornisce servizi di comunicazione SIP ad altre organizzazioni, ad esempio Fabrikam, Inc. può ospitare utenti di Contoso, Northwind Traders e Wingtip Toys. Quando si instaura una federazione con un provider di hosting, la federazione viene in realtà estesa a qualunque organizzazione ospitata da quel provider. Ad esempio, se un'organizzazione si associa tramite federazione a Fabrikam, gli utenti dell'organizzazione potranno scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Contoso, Northwind Traders e Wingtip Toys.

I provider di hosting vengono utilizzati inoltre in scenari di dominio diviso. In uno scenario di dominio diviso alcuni utenti di Lync Server dispongono di account ospitati in locale, ovvero ospitati nell'implementazione locale di Lync Server. Altri utenti possono avere i propri account ospitati in remoto presso provider di hosting di terze parti. La federazione con il provider di hosting consente agli utenti in locale e in remoto di comunicare tra loro.

Per attuare la federazione con un provider di hosting di terze parti è necessario creare e abilitare un nuovo provider di hosting. A sua volta, il provider di hosting terzo dovrà creare una relazione federativa con la nuova organizzazione. È possibile abilitare un provider di hosting al momento della sua creazione; in alternativa, è possibile abilitare il provider successivamente tramite il cmdlet **Enable-CsHostingProvider**

Non è possibile attuare la federazione con un provider di hosting se gli server perimetrali sono configurati per utilizzare il routing predefinito anziché il routing del server DNS (Domain Name System).

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Enable-CsHostingProvider** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsHostingProvider"}

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
<td><p>Identificatore univoco del provider di hosting da abilitare. L'identità può essere il nome di dominio completo (FQDN) del provider di hosting (ad esempio, fabrikam.com) o il nome dell'azienda che fornisce i servizi (Fabrikam, Inc.).</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DisplayHostingProvider</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider. Il cmdlet **Enable-CsHostingProvider** accetta le istanze dell'oggetto provider di hosting inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet abilita invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Get-CsHostingProvider](get-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

