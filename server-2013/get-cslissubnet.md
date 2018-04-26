---
title: Get-CsLisSubnet
TOCTitle: Get-CsLisSubnet
ms:assetid: 670b50b9-a5ab-4b70-bdb9-bdf3c1b09d0b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398473(v=OCS.15)
ms:contentKeyID: 49300821
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisSubnet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più subnet dal database delle configurazioni delle località. È possibile associare ogni subnet a una località, nel qual caso questo cmdlet recupera anche le informazioni sulle località delle subnet. Questa associazione è utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la località del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLisSubnet

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperate tutte le subnet del server Informazioni percorso definite nella distribuzione di Lync Server.

    Get-CsLisSubnet

## ESEMPIO 2

Con questo esempio vengono recuperate tutte le informazioni per la subnet con l'indirizzo IP 192.0.10.0. Il comando chiama innanzitutto il cmdlet **Get-CsLisSubnet** per recuperare tutte le associazioni tra subnet e posizione. Questa raccolta di posizioni delle subnet viene inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** controlla la proprietà Subnet di ogni elemento nella raccolta per determinare se il valore è uguale (-eq) a 192.0.10.0. Dal momento che gli ID di subnet devono essere univoci, questo comando restituisce al massimo un oggetto.

    Get-CsLisSubnet | Where-Object {$_.Subnet -eq "192.0.10.0"}

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente all'operatore di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata sia effettuata da una connessione VoIP (Voice over Internet Protocol), questa informazione deve essere estratta in base a vari fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Questo cmdlet consente di recuperare informazioni sulle associazioni tra le posizioni fisiche e la subnet attraverso cui vengono instradate le chiamate.

Questo cmdlet non accetta parametri (se non i parametri comuni di Windows PowerShell). Il cmdlet recupera tutte le istanze dei mapping tra subnet e posizione. Per circoscrivere le informazioni recuperate, è necessario inviare l'output di questo cmdlet tramite pipe a un altro cmdlet di Windows PowerShell, ad esempio **Where-Object** o **Select-Object**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsLisSubnet** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisSubnet"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Questo cmdlet fornisce unicamente i parametri comuni di Windows PowerShell.</p></td>
<td><p></p></td>
<td><p></p></td>
<td> </td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet consente di recuperare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisSubnet](remove-cslissubnet.md)  
[Set-CsLisSubnet](set-cslissubnet.md)

