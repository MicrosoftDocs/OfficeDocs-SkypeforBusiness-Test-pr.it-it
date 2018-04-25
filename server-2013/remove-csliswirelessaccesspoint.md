---
title: Remove-CsLisWirelessAccessPoint
TOCTitle: Remove-CsLisWirelessAccessPoint
ms:assetid: 656190b0-bde0-4a92-a6b5-b96a389c4863
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398461(v=OCS.15)
ms:contentKeyID: 49300802
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisWirelessAccessPoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un punto di accesso wireless del server Informazioni percorso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsLisWirelessAccessPoint -BSSID <String> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene rimossa la posizione WAP del LIS con BSSID 99-99-99-99-99-99.

Se al punto WAP era associata una posizione, quest'ultima non viene rimossa; solo il punto di accesso wireless viene rimosso dalla mappatura delle posizioni.

    Remove-CsLisWirelessAccessPoint -BSSID 99-99-99-99-99-99

## ESEMPIO 2

In questo esempio vengono rimossi tutti i punti di accesso wireless (WAP) dell'edificio 30. In primo luogo viene effettuata la chiamata al cmdlet **Get-CsLisWirelessAccessPoint**, che restituisce una raccolta di tutti i punti WAP. La raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che individua gli elementi della raccolta la cui proprietà Location contiene la stringa Bldg30 all'interno del valore; in altri termini, una proprietà Location simile a Bldg30. Infine, la raccolta dei punti di accesso wireless dell'edificio 30 viene inviata tramite pipe al cmdlet **Remove-CsLisWirelessAccessPoint**, che rimuove tutti gli elementi della raccolta.

Si noti che, come per l'esempio 1, dal database di configurazione delle posizioni non viene rimossa alcuna posizione; viene rimosso unicamente il punto WAP cui la posizione fa riferimento.

    Get-CsLisWirelessAccessPoint | Where-Object {$_.Location -like "*Bldg30*"} | Remove-CsLisWirelessAccessPoint

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente all'operatore di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata sia effettuata da una connessione VoIP (Voice over Internet Protocol), queste informazioni devono essere estrapolate in base a diversi fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Questo cmdlet consente di rimuovere un punto di accesso wireless (WAP) dal database di configurazione delle posizioni. La rimozione del punto di accesso wireless non rimuove la posizione associata a tale punto. Utilizzare il cmdlet **Remove-CsLisLocation** per rimuovere una posizione.

Se si tenta di rimuovere un punto di accesso wireless (WAP) che non esiste, non viene intrapresa alcuna azione e non vengono visualizzati messaggi di errore o di avviso.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsLisWirelessAccessPoint** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisWirelessAccessPoint"}

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
<td><p><em>BSSID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'identificatore del set di servizi di base (BSSID) del punto di accesso wireless che si desidera rimuovere. Questo valore presenta il formato nn-nn-nn-nn-nn-nn, ad esempio, 12-34-56-78-90-ab.</p></td>
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

Consente di accettare l'input da pipeline di oggetti punto di accesso wireless LIS.

## Tipi restituiti

Questo cmdlet rimuove un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Set-CsLisWirelessAccessPoint](set-csliswirelessaccesspoint.md)  
[Get-CsLisWirelessAccessPoint](get-csliswirelessaccesspoint.md)  
[Remove-CsLisLocation](remove-cslislocation.md)

