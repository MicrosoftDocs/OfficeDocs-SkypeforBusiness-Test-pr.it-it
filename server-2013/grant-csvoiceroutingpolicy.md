---
title: Grant-CsVoiceRoutingPolicy
TOCTitle: Grant-CsVoiceRoutingPolicy
ms:assetid: a7c7b6c4-925a-464c-a3ee-8373f4eb46b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205141(v=OCS.15)
ms:contentKeyID: 49301578
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsVoiceRoutingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio di routing vocale per utente a uno o più utenti. I criteri di routing vocale gestiscono gli utilizzi PSTN per gli utenti della funzionalità vocale ibrida. Questa funzionalità consente agli utenti presenti in Skype for Business online di usufruire delle funzionalità di VoIP aziendale disponibili in un'installazione locale di Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Grant-CsVoiceRoutingPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 assegna il criterio di routing vocale per utente RedmondVoiceRoutingPolicy all'utente con il nome visualizzato di Active Directory "Ken Myer".

    Grant-CsVoiceRoutingPolicy -Identity "Ken Myer" -PolicyName "RedmondVoiceRoutingPolicy"

## Esempio 2

Nell'esempio 2 viene annullata l'assegnazione di qualsiasi criterio di routing vocale per utente precedentemente assegnato all'utente Ken Myer. Tale utente verrà di conseguenza gestito dal criterio di routing vocale globale. Per annullare l'assegnazione di un criterio per utente, impostare PolicyName su un valore Null ($Null).

    Grant-CsVoiceRoutingPolicy -Identity "Ken Myer" -PolicyName $Null

## Esempio 3

Nell'esempio 3 viene assegnato il criterio di routing vocale per utente RedmondVoiceRoutingPolicy a tutti gli utenti inclusi nell'unità organizzativa Redmond di Active Directory. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsUser** insieme al parametro OU. Il valore di parametro "OU=Redmond,dc=litwareinc,dc=com" circoscrive i dati restituiti limitandoli agli account utente dell'unità organizzativa Redmond. Tali account utente vengono quindi inviati tramite pipe al cmdlet **Grant-CsVoiceRoutingPolicy**, che assegna a ogni utente il criterio di routing vocale RedmondVoiceRoutingPolicy.

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | Grant-CsVoiceRoutingPolicy -PolicyName "RedmondVoiceRoutingPolicy"

## Descrizione dettagliata

I criteri di routing vocale vengono utilizzati in scenari "ibridi", ovvero scenari in cui alcuni utenti sono situati nella versione locale di Lync Server e altri nella versione Skype for Business online. L'assegnazione di un criterio di routing vocale agli utenti di Skype for Business online consente loro di ricevere ed effettuare chiamate sulla rete PSTN (Public Switched Telephone Network) utilizzando i trunk SIP locali.

Si noti che la sola assegnazione di un criterio di routing vocale agli utenti non comporta l'abilitazione per le chiamate PSTN tramite Skype for Business online. Tali utenti dovranno essere abilitati anche per VoIP aziendale e dovranno disporre di un criterio vocale e di un dial plan appropriati.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsVoiceRoutingPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Grant-CsVoiceRoutingPolicy non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente a cui assegnare il criterio di routing vocale per utente. Le identità utente in genere vengono specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente come dominio\accesso (ad esempio, litwareinc\kenmyer) e 4) il nome visualizzato di Active Directory dell'utente (ad esempio, Ken Myer).</p>
<p>È possibile specificare le identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name come parametro Identity dell'utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>&quot;Nome&quot; del criterio da assegnare. PolicyName è semplicemente l'identità del criterio meno l'ambito (il prefisso &quot;tag:&quot;). Ad esempio, un criterio con Identity tag:Redmond ha PolicyName uguale a Redmond. Allo stesso modo, un criterio con Identity tag:RedmondVoiceRoutingPolicy ha PolicyName uguale a RedmondVoiceRoutingPolicy.</p>
<p>Per annullare l'assegnazione di un criterio per utente precedentemente assegnato a un utente, impostare PolicyName su un valore Null ($Null).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni utente. Per connettersi a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-dc-001) o dal nome di dominio completo (FQDN) (ad esempio, atl-dc-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite la pipeline un oggetto utente che rappresenta l'account utente a cui viene assegnato il criterio di routing vocale. Per impostazione predefinita, il cmdlet <strong>Grant-CsVoiceRoutingPolicy</strong> non passa oggetti tramite la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Grant-CsVoiceRoutingPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità (Identity) di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsVoiceRoutingPolicy** non restituisce un oggetto o un valore. Se però si include il parametro PassThru, il cmdlet restituirà le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsVoiceRoutingPolicy](get-csvoiceroutingpolicy.md)  
[New-CsVoiceRoutingPolicy](new-csvoiceroutingpolicy.md)  
[Remove-CsVoiceRoutingPolicy](remove-csvoiceroutingpolicy.md)  
[Set-CsVoiceRoutingPolicy](set-csvoiceroutingpolicy.md)

