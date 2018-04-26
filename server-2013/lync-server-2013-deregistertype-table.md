---
title: 'Lync Server 2013: Tabella DeRegisterType'
TOCTitle: Tabella DeRegisterType
ms:assetid: 09148118-6209-4fd7-a494-99118689a245
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398142(v=OCS.15)
ms:contentKeyID: 49299610
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella DeRegisterType in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella DeRegisterType è una tabella statica in cui è archiviato un elenco dei possibili tipi di annullamento della registrazione utente, ad esempio 'client initiated' (client avviato), 'registration expired' (registrazione scaduta) o 'client stopped responding' (nessuna risposta dal client).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo di dati</th>
<th>Chiave/indice</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DeRegisterTypeId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p><strong>DeRegisterReason</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Valori consentiti:</p>
<ul>
<li><p>0 - Sconosciuto</p></li>
<li><p>1 - Annullamento della registrazione avviato dal client</p></li>
<li><p>2 - Registrazione scaduta</p></li>
<li><p>3 - Client che non risponde più</p></li>
<li><p>4 - Attributi utente cambiati</p></li>
<li><p>5 - Funzione di registrazione preferita cambiata</p></li>
<li><p>6 - Client legacy in modalità Eliminazione</p></li>
</ul></td>
</tr>
</tbody>
</table>

