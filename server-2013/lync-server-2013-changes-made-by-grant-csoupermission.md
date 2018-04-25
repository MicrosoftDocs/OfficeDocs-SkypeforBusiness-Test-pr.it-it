---
title: Modifiche apportate da Grant-CsOUPermission in Lync Server 2013
TOCTitle: Modifiche apportate da Grant-CsOUPermission in Lync Server 2013
ms:assetid: d744d352-1ad9-4447-8e2b-28e768d2ed1b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205310(v=OCS.15)
ms:contentKeyID: 49302134
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifiche apportate da Grant-CsOUPermission in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per delegare l'amministrazione di Lync Server 2013, è possibile aggiungere autorizzazioni a unità organizzative specifiche in modo che i membri dei gruppi universali RTC creati con la preparazione della foresta possano accedervi anche se non sono membri del gruppo Domain Admins.

Il cmdlet **Grant-CsOuPermission** concede autorizzazioni a oggetti dell'unità organizzativa specifica come indicato nelle tabelle seguenti.

## Concessione di autorizzazioni per gli oggetti User

Quando si esegue il cmdlet **Grant-CsOuPermission** per gli oggetti User di un'unità organizzativa, ai gruppi vengono concesse autorizzazioni come illustrato nella tabella seguente.

### Autorizzazioni concesse per gli oggetti User

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo</th>
<th>Autorizzazione</th>
<th>Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>Replica modifiche directory</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Leggi RTCUserSearchPropertySet</p>
<p>Leggi RTCUserProvisioningPropertySet</p>
<p>Leggi RTCPropertySet</p>
<p>Leggi Public-Information</p>
<p>Leggi General-Information</p>
<p>Leggi User-Account-Restrictions</p></td>
<td><p>Oggetti User discendenti</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Scrivi in RTCUserSearchPropertySet</p>
<p>Scrivi in msExchUCVoiceMailSettings</p>
<p>Scrivi in RTCUserProvisioningPropertySet</p>
<p>Scrivi in RTCPropertySet</p>
<p>Scrivi in proxyAddresses</p></td>
<td><p>Oggetti User discendenti</p></td>
</tr>
</tbody>
</table>


## Concessione di autorizzazioni per gli oggetti Computer

Quando si esegue il cmdlet **Grant-CsOuPermission** per gli oggetti Computer di un'unità organizzativa, ai gruppi vengono concesse autorizzazioni come illustrato nella tabella seguente.

### Autorizzazioni concesse per gli oggetti Computer

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo</th>
<th>Autorizzazione</th>
<th>Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>Replica modifiche directory</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Leggi Public-Information</p>
<p>Leggi Validated-DNS-Host-Name</p></td>
<td><p>Oggetti Computer discendenti</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Leggi Public-Information</p>
<p>Leggi Validated-DNS-Host-Name</p></td>
<td><p>Oggetti Computer discendenti</p></td>
</tr>
</tbody>
</table>


## Concessione di autorizzazioni per oggetti Contact o AppContact

Quando si esegue il cmdlet **Grant-CsOuPermission** per gli oggetti Contact o AppContact in un'unità organizzativa, ai gruppi vengono concesse autorizzazioni come illustrato nella tabella seguente.

### Autorizzazioni concesse per gli oggetti Contact o AppContact

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo</th>
<th>Autorizzazione</th>
<th>Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>Replica modifiche directory</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Leggi RTCUserSearchPropertySet</p>
<p>Leggi RTCUserProvisioningPropertySet</p>
<p>Leggi RTCPropertySet</p>
<p>Leggi Public-Information</p>
<p>Leggi General-Information</p>
<p>Leggi Public-Information</p>
<p>Leggi User-Account-Restrictions</p></td>
<td><p>Oggetti Contact discendenti</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Scrivi in RTCUserSearchPropertySet</p>
<p>Scrivi in otherIpPhone</p>
<p>Scrivi in displayName</p>
<p>Scrivi in description</p>
<p>Scrivi in telephoneNumber</p>
<p>Scrivi in msExchUCVoiceMailSettings</p>
<p>Scrivi in RTCUserProvisioningPropertySet</p>
<p>Scrivi in RTCPropertySet</p>
<p>Scrivi in proxyAddresses</p></td>
<td><p>Oggetti Contact discendenti</p></td>
</tr>
</tbody>
</table>


## Concessione di autorizzazioni per gli oggetti Device

Quando si esegue il cmdlet **Grant-CsOuPermission** per gli oggetti Device di un'unità organizzativa, ai gruppi vengono concesse autorizzazioni come illustrato nella tabella seguente.

### Autorizzazioni concesse per gli oggetti Device

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo</th>
<th>Autorizzazione</th>
<th>Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>Replica modifiche directory</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Leggi RTCUserSearchPropertySet</p>
<p>Leggi RTCUserProvisioningPropertySet</p>
<p>Leggi RTCPropertySet</p>
<p>Leggi Public-Information</p>
<p>Leggi Public-Information</p>
<p>Leggi General-Information</p>
<p>Leggi User-Account-Restrictions</p></td>
<td><p>Oggetti Contact discendenti</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Crea elemento figlio</p>
<p>Elimina elemento figlio</p>
<p>Elimina albero</p></td>
<td><p>Contact</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Scrivi in displayName</p>
<p>Scrivi in description</p>
<p>Scrivi in telephoneNumber</p></td>
<td><p>Oggetti User discendenti</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Scrivi in RTCUserSearchPropertySet</p>
<p>Scrivi in otherIpPhone</p>
<p>Scrivi in displayName</p>
<p>Scrivi in description</p>
<p>Scrivi in telephoneNumber</p>
<p>Scrivi in msExchUCVoiceMailSettings</p>
<p>Scrivi in RTCUserProvisioningPropertySet</p>
<p>Scrivi in RTCPropertySet</p>
<p>Scrivi in proxyAddresses</p></td>
<td><p>Oggetti Contact discendenti</p></td>
</tr>
</tbody>
</table>


## Concessione di autorizzazioni per gli oggetti InetOrgPerson

Quando si esegue il cmdlet **Grant-CsOuPermission** per gli oggetti InetOrgPerson di un'unità organizzativa, ai gruppi vengono concesse autorizzazioni come illustrato nella tabella seguente.

### Autorizzazioni concesse per gli oggetti InetOrgPerson

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Gruppo</th>
<th>Autorizzazione</th>
<th>Si applica a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCHSUniversalServices</p></td>
<td><p>Replica modifiche directory</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalServerReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Elenca contenuto</p>
<p>Leggi tutte le proprietà</p>
<p>Autorizzazioni di lettura</p></td>
<td><p>Solo a questo oggetto</p></td>
</tr>
<tr class="even">
<td><p>RTCUniversalUserReadOnlyGroup</p></td>
<td><p>Leggi RTCUserSearchPropertySet</p>
<p>Leggi RTCUserProvisioningPropertySet</p>
<p>Leggi RTCPropertySet</p>
<p>Leggi Public-Information</p>
<p>Leggi Public-Information</p>
<p>Leggi General-Information</p>
<p>Leggi User-Account-Restrictions</p></td>
<td><p>Oggetti inetOrgPerson discendenti</p></td>
</tr>
<tr class="odd">
<td><p>RTCUniversalUserAdmins</p></td>
<td><p>Scrivi in RTCUserSearchPropertySet</p>
<p>Scrivi in RTCUserProvisioningPropertySet</p>
<p>Scrivi in RTCPropertySet</p>
<p>Scrivi in proxyAddresses</p></td>
<td><p>Oggetti inetOrgPerson discendenti</p></td>
</tr>
</tbody>
</table>

