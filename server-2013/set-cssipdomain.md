---
title: Set-CsSipDomain
TOCTitle: Set-CsSipDomain
ms:assetid: c19aaa3f-04d3-467e-b9d5-d574674eb4a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412949(v=OCS.15)
ms:contentKeyID: 49301889
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSipDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare i valori delle proprietà dei domini SIP dell'organizzazione. I domini SIP sono domini autorizzati a inviare e a ricevere traffico SIP e vengono utilizzati per l'assegnazione degli indirizzi SIP agli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsSipDomain [-Identity <XdsGlobalRelativeIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-IsDefault <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 indica il dominio SIP fabrikam.com come dominio SIP predefinito. Questa operazione viene eseguita tramite il parametro IsDefault e il valore di parametro $True. Una volta eseguito questo comando, Fabrikam.com diventerà il dominio predefinito e il precedente dominio predefinito verrà abbassato di livello. È possibile infatti disporre di un solo dominio predefinito.

    Set-CsSipDomain -Identity fabrikam.com -IsDefault $True

## Descrizione dettagliata

Per configurare gli indirizzi SIP per gli utenti (e abilitarli quindi all'utilizzo di software correlato a SIP, ad esempio Lync 2013), sono necessarie due informazioni: un ID utente (ad esempio Ken.Myer) e un dominio SIP (ad esempio litwareinc.com). Il dominio SIP utilizzato per creare un indirizzo SIP deve essere un dominio situato all'interno della foresta di Active Directory autorizzato per l'invio e la ricezione di traffico SIP. Si supponga ad esempio di disporre di domini denominati litwareinc.com, fabrikam.com e contoso.com, ma che solo litwareinc.com sia stato identificato come dominio SIP. In tal caso, non è possibile utilizzare un indirizzo SIP come sip:Ken.Myer@fabrikam.com o sip:Ken.Myer@contoso.com, almeno fino a quando fabrikam.com e contoso.com non siano stati configurati come domini SIP validi. Questa operazione può essere effettuata eseguendo il cmdlet **New-CsSipDomain**.

È necessario disporre sempre di un dominio SIP configurato come dominio predefinito. Il cmdlet **Set-CsSipDomain** consente di cambiare il dominio SIP predefinito.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsSipDomain** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

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
<td><p>Nome di dominio completo (FQDN) del dominio SIP da configurare come dominio predefinito, ad esempio -Identity fabrikam.com.</p></td>
</tr>
<tr class="even">
<td><p><em>IsDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il dominio specificato è il dominio SIP predefinito, ovvero il dominio utilizzato da Lync Server ogni volta che non viene esplicitamente specificato un dominio. Se impostato su True, il nuovo dominio diventerà il nuovo dominio predefinito Non è possibile impostare questo valore su False, poiché si rimarrebbe senza un dominio SIP predefinito.</p>
<p>Se si modifica il dominio SIP predefinito, è necessario riavviare i servizi RTCCAA e RTCCAS.</p></td>
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

Nessuno. Il cmdlet **Set-CsSipDomain** non accetta dati da pipeline.

## Tipi restituiti

Il cmdlet **Set-CsSipDomain** non restituisce alcun oggetto o valore. Il cmdlet viene piuttosto utilizzato per modificare le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.SipDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsSipDomain](get-cssipdomain.md)  
[New-CsSipDomain](new-cssipdomain.md)  
[Remove-CsSipDomain](remove-cssipdomain.md)

