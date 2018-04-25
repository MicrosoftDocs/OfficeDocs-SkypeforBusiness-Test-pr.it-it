---
title: Get-CsLisPort
TOCTitle: Get-CsLisPort
ms:assetid: c755aa8c-e842-4bb8-bdbf-d61a364eb0bc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398820(v=OCS.15)
ms:contentKeyID: 49301915
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisPort

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più porte dal database delle configurazioni delle località. È possibile associare ogni porta a una località, nel qual caso questo cmdlet recupera anche le informazioni sulle località delle porte. Questa associazione è utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per segnalare la località del chiamante all'operatore del servizio di emergenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLisPort

## Esempi

## Esempio 1

Nell'esempio 1 vengono recuperate tutte le porte LIS (Location Information Server) e le posizioni associate che sono state definite nella distribuzione di Lync Server.

    Get-CsLisPort

## Esempio 2

Questo esempio consente di recuperare tutte le informazioni relative alle porte associate a una posizione nella città di Redmond. Il comando chiama innanzitutto il cmdlet **Get-CsLisPort** per recuperare tutte le associazioni di posizioni delle porte. La raccolta di posizioni delle porte viene inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** controlla la proprietà City di ogni elemento nella raccolta per stabilire se il valore è uguale a (-eq) Redmond.

    Get-CsLisPort | Where-Object {$_.City -eq "Redmond"}

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente a un operatore di servizi di emergenza di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata venga effettuata tramite connessione VoIP (Voice over Internet Protocol), questa informazione deve essere estratta in base a diversi fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Questo cmdlet recupera le informazioni sulle associazioni tra le posizioni fisiche e la porta attraverso cui è collegato il client.

Questo cmdlet non utilizza parametri, se non i parametri comuni di Windows PowerShell. Il cmdlet recupererà tutte le istanze della porta per i mapping delle posizioni. Per circoscrivere le informazioni recuperate, è necessario inviare l'output di questo cmdlet tramite pipe a un altro cmdlet di Windows PowerShell, ad esempio il cmdlet **Where-Object** o il cmdlet **Select-Object**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsLisPort** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisPort"}

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

Questo cmdlet consente di recuperare uno o più oggetti di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisPort](remove-cslisport.md)  
[Set-CsLisPort](set-cslisport.md)

