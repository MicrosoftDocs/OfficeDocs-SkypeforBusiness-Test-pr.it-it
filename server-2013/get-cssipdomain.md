---
title: Get-CsSipDomain
TOCTitle: Get-CsSipDomain
ms:assetid: 8a8def42-7b14-40c3-be5a-57905069b405
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398701(v=OCS.15)
ms:contentKeyID: 49301245
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSipDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui domini SIP configurati per l'utilizzo nell'organizzazione. I domini SIP sono domini autorizzati a inviare e a ricevere traffico SIP e vengono utilizzati per l'assegnazione degli indirizzi SIP agli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsSipDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsSipDomain [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene chiamato il cmdlet **Get-CsSipDomain** senza parametri. In questo modo vengono restituite informazioni su tutti i domini SIP configurati per l'utilizzo nell'organizzazione.

    Get-CsSipDomain

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce le informazioni di ogni dominio SIP con Identity fabrikam.com. Poiché le identità dei domini SIP devono essere univoche, questo comando non restituisce mai più di un elemento.

    Get-CsSipDomain -Identity fabrikam.com

## ESEMPIO 3

Nell'esempio 3 vengono utilizzati il cmdlet **Get-CsSipDomain** e il parametro Filter per restituire informazioni su tutti i domini SIP la cui identità inizia con la lettera "f", ad esempio fabrikam.com, fabrikam.org, fabrikam-users.com e così via.

    Get-CsSipDomain -Filter "f*"

## ESEMPIO 4

Il comando mostrato nell'esempio 4 restituisce informazioni sul dominio SIP predefinito. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsSipDomain** senza alcun parametro per restituire una raccolta di tutti i domini SIP configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe a **Where-Object**, che seleziona l'unico dominio in cui la proprietà IsDefault equivale a True.

    Get-CsSipDomain | Where-Object {$_.IsDefault -eq $True}

## Descrizione dettagliata

Per configurare gli indirizzi SIP per gli utenti (e per abilitarli all'utilizzo di software correlato a SIP, ad esempio Lync 2013), sono necessarie due informazioni: un ID utente (ad esempio Ken.Myer) e un dominio SIP (ad esempio litwareinc.com). Il dominio SIP utilizzato per costruire un indirizzo SIP deve essere un dominio situato all'interno della foresta di Active Directory e autorizzato per l'invio e la ricezione del traffico SIP. Si supponga ad esempio di disporre di domini denominati litwareinc.com, fabrikam.com e contoso.com, ma che solo litwareinc.com sia stato identificato come dominio SIP. In tal caso, non è possibile utilizzare un indirizzo SIP come sip:Ken.Myer@fabrikam.com o sip:Ken.Myer@contoso.com, almeno fino a quando fabrikam.com e contoso.com non saranno stati configurati come domini SIP validi. Questa operazione è possibile eseguendo il cmdlet **New-CsSipDomain**.

Il cmdlet **Get-CsSipDomain** consente di restituire le informazioni sui domini SIP autorizzati per l'utilizzo nell'organizzazione. Il cmdlet **Get-CsSipDomain** identifica inoltre il dominio SIP predefinito per l'organizzazione, ovvero il dominio che verrà utilizzato per impostazione predefinita da Lync Server se non viene specificato un dominio SIP.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsSipDomain** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSipDomain"}

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
<td><p>Consente di utilizzare caratteri jolly per specificare l'identità del dominio o dei domini SIP da restituire. Ad esempio, il valore di filtro &quot;*.org&quot; restituisce una raccolta di tutti i domini SIP autorizzati la cui identità termina con il valore stringa &quot;.org&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo del dominio SIP che si desidera venga restituito (ad esempio, fabrikam.com). Se non si specifica né questo parametro, né il parametro Filter, vengono restituiti tutti i domini SIP autorizzati per l'utilizzo nell'organizzazione.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsSipDomain** non accetta dati inviati tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsSipDomain** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Xds.SipDomain.

## Vedere anche

#### Ulteriori risorse

[New-CsSipDomain](new-cssipdomain.md)  
[Remove-CsSipDomain](remove-cssipdomain.md)  
[Set-CsSipDomain](set-cssipdomain.md)

