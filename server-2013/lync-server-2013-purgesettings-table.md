---
title: Tabella PurgeSettings in Lync Server 2013
TOCTitle: Tabella PurgeSettings in Lync Server 2013
ms:assetid: 9ff2c8fc-4ae8-4f22-96a8-1f4d5eecbf2d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205121(v=OCS.15)
ms:contentKeyID: 49301491
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella PurgeSettings in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella PurgeSettings sono incluse informazioni che specificano se e quando le registrazioni dettagli chiamata obsolete verranno eliminate automaticamente dal relativo database. È inoltre possibile ottenere da Microsoft Lync Server 2013 Management Shell le informazioni relative all'eliminazione eseguendo il comando seguente:

    Get-CsCdrConfiguration

La tabella PurgeSettings deve essere considerata di sola lettura dagli amministratori. Le modifiche relative alle impostazioni di eliminazione dei dettagli chiamata devono essere apportate solo mediante il cmdlet [New-CsCdrConfiguration](new-cscdrconfiguration.md) o [Set-CsCdrConfiguration](set-cscdrconfiguration.md).

Questa tabella è stata introdotta in Microsoft Lync Server 2013.


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
<th>Chiave/Indice</th>
<th>Dettagli</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Id</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Identificatore univoco della raccolta di impostazioni di eliminazione delle registrazioni dettagli chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>EnablePurge</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Se questa colonna è impostata su True (1), Microsoft Lync Server 2013 eliminerà periodicamente le registrazioni dettagli chiamata obsolete dal relativo database. L'eliminazione verrà eseguita ogni giorno all'orario specificato dall'impostazione PurgeHour. Se questa colonna è impostata su False (0), le registrazioni non verranno eliminate automaticamente dal database. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><strong>KeepCallDetailForDays</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Specifica il periodo di tempo (in giorni) per l'eliminazione delle registrazioni dettagli chiamata dal database. Se l'eliminazione è abilitata, verranno rimosse dal database le registrazioni dettagli chiamata esistenti da un numero di giorni superiore a tale valore. Il valore predefinito è 60 giorni.</p></td>
</tr>
<tr class="even">
<td><p><strong>KeepErrorReportForDays</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Specifica il periodo di tempo (in giorni) per l'eliminazione dei record di segnalazione errori dal database. Se l'eliminazione è abilitata, verranno rimossi dal database i record di segnalazione errori esistenti da un numero di giorni superiore a tale valore. Il valore predefinito è 60 giorni.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PurgeHour</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Specifica l'orario locale in cui verrà eseguita l'eliminazione delle registrazioni e dei record dal database. L'orario è specificato nel formato 24 ore, con 0 che rappresenta la mezzanotte e 23 che rappresenta le 11 di sera. Si noti che è possibile specificare solo l'ora e non i minuti. Il valore 10 (per indicare le 10 del mattino) è consentito, a differenza del valore 10:30 o 10.5 (per indicare le 10 e mezza del mattino). Il valore predefinito è 2 (2 del mattino).</p></td>
</tr>
</tbody>
</table>

