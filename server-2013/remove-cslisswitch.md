---
title: Remove-CsLisSwitch
TOCTitle: Remove-CsLisSwitch
ms:assetid: 53456988-4b37-4f34-825d-bebee5124856
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398352(v=OCS.15)
ms:contentKeyID: 49300533
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisSwitch

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un commutatore di rete del server Informazioni percorso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsLisSwitch -ChassisID <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene rimosso il commutatore LIS con indirizzo MAC (ChassisID) 99-99-99-99-99-99.

Se una porta fa riferimento a questo ChassisID, l'operazione non riesce. Inoltre, se al commutatore era associata una posizione, quest'ultima non viene rimossa; solo il commutatore viene rimosso dalla mappatura delle posizioni.

    Remove-CsLisSwitch -ChassisID 99-99-99-99-99-99

## ESEMPIO 2

In questo esempio vengono rimossi tutti i commutatori per cui non è indicata una città. L'esempio inizia con una chiamata al cmdlet **Get-CsLisSwitch**, che restituisce una raccolta di tutti i commutatori. La raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che trova tutti gli elementi della raccolta con proprietà City vuota, ovvero una proprietà City uguale a (-eq) una stringa vuota (""). Questa raccolta di commutatori con proprietà City vuota infine viene inviata tramite pipe al cmdlet **Remove-CsLisSwitch**, che rimuove tutti gli oggetti della raccolta.

Analogamente all'esempio 1, dal database delle posizioni non viene rimossa alcuna posizione. Vengono rimossi unicamente i commutatori che fanno riferimento a tali posizioni. In questo caso, tutto ciò comporta che nel database delle posizioni ci saranno delle posizioni non valide, poiché la proprietà City è obbligatoria per le posizioni, che dovranno essere rimosse. È possibile rimuovere le posizioni chiamando il cmdlet **Remove-CsLisLocation**.

    Get-CsLisSwitch | Where-Object {$_.City -eq ""} | Remove-CsLisSwitch

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente all'operatore di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata sia effettuata da una connessione VoIP (Voice over Internet Protocol), queste informazioni devono essere estrapolate in base a diversi fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Questo cmdlet rimuove un commutatore dal database di configurazione delle posizioni. La rimozione di un commutatore non comporta la rimozione della posizione effettiva. Viene rimosso solo il commutatore. Per rimuovere la posizione, chiamare il cmdlet **Remove-CsLisLocation**.

Non è possibile rimuovere un commutatore se il valore ChassisID del commutatore è utilizzato da un'altra porta. Eseguire il comando seguente per trovare i valori ChassisID utilizzati dalle porte: Get-CsLisPort | Select-Object ChassisID. È necessario rimuovere per prima cosa tutte le porte con il ChassisID specificato, prima di poter rimuovere il commutatore.

Se si tenta di rimuovere un commutatore che non esiste, non viene intrapresa alcuna azione e non vengono visualizzati messaggi di errore o di avviso.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsLisSwitch** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisSwitch"}

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
<td><p><em>ChassisID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo MAC (Media Access Control) del commutatore di rete. Questo valore presenta il formato nn-nn-nn-nn-nn-nn, ad esempio, 12-34-56-78-90-ab.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Accetta l'input da pipeline di oggetti commutatore LIS.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuovere un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Set-CsLisSwitch](set-cslisswitch.md)  
[Get-CsLisSwitch](get-cslisswitch.md)  
[Remove-CsLisLocation](remove-cslislocation.md)  
[Get-CsLisPort](get-cslisport.md)

