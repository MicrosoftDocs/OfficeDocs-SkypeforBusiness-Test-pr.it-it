---
title: Configurazione degli intervalli di porte per i server perimetrali
TOCTitle: Configurazione degli intervalli di porte per i server perimetrali
ms:assetid: 6f0ae442-6624-4e3f-849a-5b9e387fb8cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204996(v=OCS.15)
ms:contentKeyID: 49300925
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione degli intervalli di porte per i server perimetrali

 

_**Ultima modifica dell'argomento:** 2015-07-24_

Per i server perimetrali non è necessario configurare intervalli di porte separati per audio, video e condivisione applicazioni. Allo stesso modo, gli intervalli di porte utilizzati per i server perimetrali devono corrispondere agli intervalli di porte utilizzati con i server per le conferenze, i server applicazioni e i server Mediation. Tuttavia, per semplificare l'amministrazione, è possibile modificare gli intervalli di porte dei server perimetrali sugli altri server. Si supponga, ad esempio, di aver configurato i server per le conferenze, i server applicazioni e i server Mediation affinché utilizzino questi intervalli di porte:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di pacchetto</th>
<th>Numero di porta iniziale</th>
<th>Numero di porte riservate</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Condivisione applicazioni</p></td>
<td><p>40803</p></td>
<td><p>8348</p></td>
</tr>
<tr class="even">
<td><p>Audio</p></td>
<td><p>49152</p></td>
<td><p>8348</p></td>
</tr>
<tr class="odd">
<td><p>Video</p></td>
<td><p>57500</p></td>
<td><p>8034</p></td>
</tr>
<tr class="even">
<td><p><strong>Totali</strong></p></td>
<td><p>--</p></td>
<td><p>24730</p></td>
</tr>
</tbody>
</table>


Si può vedere che gli intervalli di porte per audio, video e condivisione applicazioni iniziano dalla porta 40803 e comprendono 24732 porte totali. Se lo si desidera, è possibile configurare un server perimetrale specifico affinché utilizzi questi valori generali, eseguendo un comando simile al seguente da Lync Server Management Shell:

    Set-CsEdgeServer -Identity EdgeServer:atl-edge-001.litwareinc.com -MediaCommunicationPortStart 40803 -MediaCommunicationPortCount 24730

Alternativamente, è possibile utilizzare il comando seguente per configurare simultaneamente tutti i server perimetrali all'interno dell'organizzazione:

    Get-CsService -EdgeServer | ForEach-Object {Set-CsEdgeServer -Identity $_.Identity -MediaCommunicationPortStart 40803 -MediaCommunicationPortCount 24730}

È possibile verificare le impostazioni correnti per le porte dei server perimetrali utilizzando questo comando di Lync Server Management Shell:

    Get-CsService -EdgeServer | Select-Object Identity, MediaCommunicationPortStart, MediaCommunicationPortCount

