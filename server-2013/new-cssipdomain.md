---
title: New-CsSipDomain
TOCTitle: New-CsSipDomain
ms:assetid: 385f0f23-397b-4d8d-b9b7-ec942cda4a99
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425857(v=OCS.15)
ms:contentKeyID: 49300219
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo dominio SIP da utilizzare nell'organizzazione. I domini SIP sono domini autorizzati a inviare e a ricevere traffico SIP e vengono utilizzati per l'assegnazione degli indirizzi SIP agli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-IsDefault <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare un nuovo dominio SIP che ha come identità fabrikam.com.

    New-CsSipDomain -Identity fabrikam.com

## ESEMPIO 2

Nell'esempio 2 viene creato un nuovo dominio SIP denominato fabrikam.com, che viene impostato come dominio SIP predefinito. Impostando fabrikam.com come dominio predefinito, il comando "abbassa di livello" il dominio che in precedenza rappresentava il dominio SIP predefinito. È infatti possibile disporre di un solo dominio SIP predefinito.

    New-CsSipDomain -Identity fabrikam.com -IsDefault $True

## Descrizione dettagliata

Per configurare gli indirizzi SIP per gli utenti e abilitarli quindi all'utilizzo del software correlato, ad esempio Lync 2013, sono necessarie due informazioni: un ID utente, ad esempio Ken.Myer, e un dominio SIP, ad esempio litwareinc.com. Il dominio SIP utilizzato per creare un indirizzo SIP deve essere un dominio situato all'interno della foresta di Active Directory e autorizzato per l'invio e la ricezione del traffico SIP. Si supponga ad esempio di disporre di domini denominati litwareinc.com, fabrikam.com e contoso.com, ma che solo litwareinc.com sia stato identificato come dominio SIP. In tal caso, non è possibile utilizzare un indirizzo SIP come sip:Ken.Myer@fabrikam.com o sip:Ken.Myer@contoso.com, almeno fino a quando fabrikam.com e contoso.com non siano stati configurati come domini SIP validi. Questa operazione può essere eseguita utilizzando il cmdlet **New-CsSipDomain**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsSipDomain** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipDomain"}

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
<td><p>Nome di dominio completo per il nuovo dominio SIP. Ad esempio: -Identity fabrikam.com.</p></td>
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
<td><p><em>IsDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il dominio specificato è il dominio SIP predefinito, ovvero il dominio utilizzato da Lync Server ogni volta che non viene esplicitamente specificato un nome di dominio. Se si imposta questo parametro su True, il nuovo dominio diventerà anche il nuovo dominio predefinito</p>
<p>Il valore predefinito per IsDefault è False. Se non si vuole rendere il nuovo dominio il dominio predefinito, lasciare il parametro vuoto.</p>
<p>Se si cambia il dominio SIP predefinito, sarà necessario riavviare i servizi RTCCAA e RTCCAS.</p></td>
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

Nessuno. Il cmdlet **New-CsSipDomain** non accetta dati da pipeline.

## Tipi restituiti

Il cmdlet **New-CsSipDomain** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.Xds.SipDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsSipDomain](get-cssipdomain.md)  
[Remove-CsSipDomain](remove-cssipdomain.md)  
[Set-CsSipDomain](set-cssipdomain.md)

