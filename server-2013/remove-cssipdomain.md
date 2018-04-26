---
title: Remove-CsSipDomain
TOCTitle: Remove-CsSipDomain
ms:assetid: cccd344f-7744-46c5-b1e1-ca4e8a29772c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398865(v=OCS.15)
ms:contentKeyID: 49301992
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsSipDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un dominio SIP precedentemente configurato per l'utilizzo nell'organizzazione. I domini SIP sono domini autorizzati a inviare e a ricevere traffico SIP e vengono utilizzati per l'assegnazione degli indirizzi SIP agli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsSipDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nel'esempio 1 viene rimosso il dominio SIP con valore Identity fabrikam.com dall'elenco dei nomi di dominio supportati. Il comando avrà esito negativo se fabrikam.com è l'unico dominio SIP attualmente in uso nell'organizzazione. La topologia infatti deve includere almeno un dominio SIP.

    Remove-CsSipDomain -Identity fabrikam.com

## ESEMPIO 2

Il comando mostrato nell'esempio 2 elimina tutti i domini SIP all'interno dell'organizzazione, tranne il dominio predefinito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsSipDomain** per restituire una raccolta di tutti i domini SIP in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i domini con proprietà IsDefault non uguale a True. Il risultato è che il dominio predefinito viene filtrato e i restanti domini vengono successivamente inviati tramite pipe al cmdlet **Remove-CsSipDomain** ed eliminati.

    Get-CsSipDomain | Where-Object {$_.IsDefault -ne $True} | Remove-CsSipDomain

## Descrizione dettagliata

Per configurare gli indirizzi SIP per gli utenti (e abilitarli quindi all'utilizzo di software correlato a SIP, ad esempio Lync 2013), sono necessarie due informazioni: un ID utente (ad esempio Ken.Myer) e un dominio SIP (ad esempio litwareinc.com). Il dominio SIP utilizzato per creare un indirizzo SIP deve essere un dominio situato all'interno della foresta di Active Directory autorizzato per l'invio e la ricezione di traffico SIP. Si supponga ad esempio di disporre di domini denominati litwareinc.com, fabrikam.com e contoso.com, ma che solo litwareinc.com sia stato identificato come dominio SIP. In tal caso, non è possibile utilizzare un indirizzo SIP come sip:Ken.Myer@fabrikam.com o sip:Ken.Myer@contoso.com, almeno fino a quando fabrikam.com e contoso.com non siano stati configurati come domini SIP validi. Questa operazione può essere effettuata eseguendo il cmdlet **New-CsSipDomain**.

Dopo che un dominio SIP è stato autorizzato, l'autorizzazione può essere annullata utilizzando il cmdlet **Remove-CsSipDomain**. Questo cmdlet rimuove dall'elenco dei domini SIP approvati il dominio specificato. Non è possibile tuttavia rimuovere il dominio predefinito. Qualora sia necessario procedere in tal senso, configurare innanzitutto un altro dominio SIP come dominio predefinito. Se si dispone di un solo dominio SIP, esso verrà automaticamente configurato come dominio predefinito e non sarà possibile rimuoverlo.

Non è possibile inoltre rimuovere un dominio SIP a cui sono stati assegnati uno o più indirizzi SIP. Non è possibile ad esempio rimuovere Contoso.com come dominio SIP se Davide Garghentini dispone dell'indirizzo SIP "sip:davidegarghentini@contoso.com". Per rimuovere un dominio SIP attualmente in uso, è necessario innanzitutto assegnare nuovi indirizzi SIP a tutti gli utenti che utilizzano tale dominio nel proprio indirizzo SIP.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsSipDomain** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsSipDomain"}

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
<td><p>Nome di dominio completo (FQDN) del dominio SIP da rimuovere, ad esempio -Identity fabrikam.com.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.SipDomain. Il cmdlet **Remove-CsSipDomain** accetta le istanze da pipeline dell'oggetto dominio SIP.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsSipDomain** elimina piuttosto l'istanza esistente dell'oggetto Microsoft.Rtc.Management.Xds.SipDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsSipDomain](get-cssipdomain.md)  
[New-CsSipDomain](new-cssipdomain.md)  
[Set-CsSipDomain](set-cssipdomain.md)

