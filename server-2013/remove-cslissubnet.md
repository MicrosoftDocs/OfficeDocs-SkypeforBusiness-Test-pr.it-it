---
title: Remove-CsLisSubnet
TOCTitle: Remove-CsLisSubnet
ms:assetid: f8a87038-cc71-4fec-8496-574da0aa963f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413053(v=OCS.15)
ms:contentKeyID: 49302521
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisSubnet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una subnet del server Informazioni percorso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsLisSubnet -Subnet <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene rimossa la voce del percorso di subnet LIS per la subnet con indirizzo IP 192.10.10.0. Il comando nell'esempio include solo un parametro (obbligatorio): Subnet. Il valore del parametro Subnet riportato nell'esempio è un indirizzo IPv4, 192.10.10.0.

Se questa subnet è associata a una posizione, tale posizione non verrà rimossa. Dal mapping delle posizioni verrà rimossa solo la subnet.

    Remove-CsLisSubnet -Subnet 192.10.10.0

## ESEMPIO 2

In questo esempio vengono rimosse tutte le subnet associate alla posizione Bldg30/Room1000. L'esempio inizia con una chiamata al cmdlet **Get-CsLisSubnet**, che restituisce una raccolta di tutte le subnet LIS. La raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che trova gli elementi della raccolta con proprietà Location uguale (-eq) alla stringa Bldg30/Room1000. Tale raccolta di subnet con la proprietà Location in questione viene infine inviata tramite pipe al cmdlet **Remove-CsLisSubnet**, che rimuove tutto ciò che è presente nella raccolta.

Come nell'esempio 1, non viene rimossa alcuna posizione dal database di configurazione delle posizioni. Vengono rimosse solo le subnet che fanno riferimento a tali posizioni. È possibile rimuovere le posizioni chiamando il cmdlet **Remove-CsLisLocation**.

    Get-CsLisSubnet | Where-Object {$_.Location -eq "Bldg30/Room1000"} | Remove-CsLisSubnet

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente all'operatore dei servizi di emergenza di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata venga effettuata tramite connessione VoIP (Voice over Internet Protocol), questa informazione deve essere estratta in base a diversi fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Questo cmdlet rimuove una subnet dal database di configurazione delle posizioni. La rimozione della subnet non comporta la rimozione della posizione associata alla subnet. Utilizzare il cmdlet **Remove-CsLisLocation** per rimuovere una posizione.

Se si tenta di rimuovere una subnet che non esiste, non verrà eseguita alcuna azione e non verrà visualizzato alcun messaggio di errore o di avviso.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsLisSubnet** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisSubnet"}

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
<td><p><em>Subnet</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'indirizzo IP della subnet che si desidera rimuovere. Tale valore sarà un indirizzo IPv4 (cifre separate da punti, come 192.0.2.0).</p></td>
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

Accetta l'input da pipeline di oggetti subnet LIS (Location Information Server).

## Tipi restituiti

Questo cmdlet rimuove un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Set-CsLisSubnet](set-cslissubnet.md)  
[Get-CsLisSubnet](get-cslissubnet.md)  
[Remove-CsLisLocation](remove-cslislocation.md)

