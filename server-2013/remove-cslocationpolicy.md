---
title: Remove-CsLocationPolicy
TOCTitle: Remove-CsLocationPolicy
ms:assetid: 8fb98533-6474-4071-a74c-ce3f6fa2d326
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398727(v=OCS.15)
ms:contentKeyID: 49301307
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLocationPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il criterio percorso specificato. I criteri di questo tipo vengono utilizzati con il servizio di chiamate di emergenza Enhanced 9-1-1 per consentire a chi risponde alle chiamate di emergenza di determinare la posizione geografica del chiamante in base al numero del telefono o del dispositivo utilizzato per effettuare la chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsLocationPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 utilizza il cmdlet **Remove-CsLocationPolicy** per eliminare i criteri percorso con identità (Identity) Reno. Quando vengono rimossi criteri per utente, gli utenti o i gruppi ai quali erano stati assegnati tali criteri utilizzeranno automaticamente i criteri definiti per il proprio sito. Se non sono stati configurati criteri per il sito, questi utenti o gruppi utilizzeranno i criteri percorso globali.

    Remove-CsLocationPolicy -Identity Reno

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i criteri percorso in cui il valore della proprietà EnhancedEmergencyServicesEnabled è False. In altri termini verranno eliminati tutti criteri che non abilitano il servizio E9-1-1. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsLocationPolicy** per recuperare tutti i criteri percorso attualmente in uso nell'organizzazione. Questa raccolta vene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro per ottenere solo i dati relativi ai criteri in cui la proprietà EnhancedEmergencyServicesEnabled è uguale a (-eq) False ($False). Infine, questa raccolta filtrata viene passata al cmdlet **Remove-CsLocationPolicy**, che elimina ogni criterio della raccolta.

    Get-CsLocationPolicy | Where-Object {$_.EnhancedEmergencyServicesEnabled -eq $false} | Remove-CsLocationPolicy

## Descrizione dettagliata

I criteri percorso vengono usati per applicare impostazioni che mettono in relazione la funzionalità E9-1-1. I criteri percorso stabiliscono se un utente è abilitato per la funzionalità E9-1-1 e, in caso affermativo, quale comportamento tenere per una chiamata di emergenza. Ad esempio, è possibile usare i criteri percorso per definire quale numero costituisce una chiamata di emergenza (911 negli Stati Uniti), se la sicurezza aziendale deve essere automaticamente informata, come deve essere instradata la chiamata e così via. Questo cmdlet consente di rimuovere i criteri percorso esistenti.

Oltre che per rimuovere criteri percorso per sito e per utente, questo cmdlet può essere utilizzato per rimuovere anche criteri percorso globali. In questo caso, però, i criteri non vengono effettivamente rimossi; in realtà, il risultato è la reimpostazione dei valori predefiniti per le impostazioni dei criteri.

Se questo cmdlet viene eseguito nei confronti di criteri percorso per utente assegnati ad un utente, verrà richiesto di confermarne l'eliminazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsLocationPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLocationPolicy"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio percorso che si desidera rimuovere. Per rimuovere il criterio percorso globale (ripristinando così i valori predefiniti del criterio), utilizzare il valore Global. Per un criterio creato nell'ambito del sito, questo valore ha il formato site:&lt;nome sito&gt;, dove &quot;nome sito&quot; è il nome di un sito definito nella distribuzione di Lync Server (ad esempio, site:Redmond). Per un criterio creato nell'ambito del singolo utente, questo valore è il nome del criterio (ad esempio, Bldg30Floor3Sector1).</p></td>
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
<td><p>Specificando questo parametro si eviteranno tutti i messaggi di conferma e l'eliminazione avverrà senza alcuna notifica. Ad esempio, se criteri per utente sono assegnati ad uno o più utenti e questo parametro non viene inserito nel comando, verrà visualizzato un messaggio di conferma prima dell'eliminazione.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy. Accetta l'input da pipeline di oggetti criterio percorso.

## Tipi restituiti

Questo cmdlet non restituisce alcun oggetto o valore. Il cmdlet rimuove invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)

