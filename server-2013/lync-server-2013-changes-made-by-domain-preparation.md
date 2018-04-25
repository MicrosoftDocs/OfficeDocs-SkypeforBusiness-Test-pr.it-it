---
title: Modifiche apportate durante la preparazione del dominio in Lync Server 2013
TOCTitle: Modifiche apportate durante la preparazione del dominio in Lync Server 2013
ms:assetid: 9191221e-6166-4c2b-837e-fa73d90fdf80
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398742(v=OCS.15)
ms:contentKeyID: 49301326
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifiche apportate durante la preparazione del dominio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella tabella riportata di seguito vengono elencate le voci di controllo di accesso create durante la preparazione del dominio nella radice del dominio. Se non diversamente specificato, tutte le voci di controllo di accesso vengono ereditate.

### Voci di controllo di accesso aggiunte alla radice del dominio

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>ACE</th>
<th>RTCUniversal-UserReadOnly-Group</th>
<th>RTCUniversal-ServerReadOnly-Group</th>
<th>RTCUniversal-UserAdmins</th>
<th>RTCHSUniversal-Services</th>
<th>Authenticated-Users</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Read Container (not inherited)</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Read User PropertySet User-Account-Restrictions</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Read User PropertySet Personal-Information</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Read User PropertySet General-Information</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Read User PropertySet Public-Information</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Read User PropertySet RTCUserSearchProperty-Set</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p><strong>Sì</strong></p></td>
</tr>
<tr class="odd">
<td><p>Read User PropertySet RTCPropertySet</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Write User Property Proxy-Addresses</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Write User PropertySet RTCUserSearchProperty-Set</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Write User PropertySet RTCPropertySet</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Read PropertySet DS-Replication-Get-Changes of all Active Directory objects</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


Nella tabella seguente vengono elencate le voci di controllo di accesso create durante la preparazione del dominio nei tre contenitori predefiniti, ovvero Utenti, Computer e Controller di dominio. Se non diversamente specificato, tutte le voci di controllo di accesso vengono ereditate.

### Voci di controllo di accesso aggiunte ai contenitori predefiniti

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>ACE</th>
<th>RTCUniversal-UserReadOnly-Group</th>
<th>RTCUniversal-ServerReadOnly-Group</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Read Container (non ereditata)</p></td>
<td><p><strong>Sì</strong></p></td>
<td><p><strong>Sì</strong></p></td>
</tr>
</tbody>
</table>

