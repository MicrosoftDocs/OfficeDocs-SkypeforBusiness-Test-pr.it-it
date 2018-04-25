---
title: 'Lync Server 2013: Tabella Tenants'
TOCTitle: Tabella Tenants
ms:assetid: c1b070c1-2c59-4ca9-910b-43f673f97fda
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412950(v=OCS.15)
ms:contentKeyID: 49301858
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Tenants in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La tabella Tenants è una tabella di supporto in cui viene archiviato un elenco dei diversi tenant. Ogni record della tabella rappresenta un tenant.


> [!NOTE]
> Nelle distribuzioni on-premise, registrazione dettagli chiamata utilizza l'ID tenant predefinito per indicare tipi di autenticazione diversi, come connettività per messaggistica istantanea pubblica, autenticazione federata e autenticazione anonima.




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
<td><p><strong>TenantId</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero univoco che identifica questo ID tenant.</p></td>
</tr>
<tr class="even">
<td><p><strong>TenantKey</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Valori consentiti:</p>
<ul>
<li><p>00000000-0000-0000-0000-000000000000 - Aziendale</p></li>
<li><p>00000000-0000-0000-0000-000000000001 - Federato</p></li>
<li><p>00000000-0000-0000-0000-000000000002 - Anonimo</p></li>
<li><p>00000000-0000-0000-0000-000000000003 - Connettività per la messaggistica istantanea pubblica</p></li>
</ul></td>
</tr>
</tbody>
</table>

