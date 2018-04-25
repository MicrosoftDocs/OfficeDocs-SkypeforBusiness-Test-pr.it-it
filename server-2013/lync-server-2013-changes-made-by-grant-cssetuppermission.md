---
title: Modifiche apportate da Grant-CsSetupPermission in Lync Server 2013
TOCTitle: Modifiche apportate da Grant-CsSetupPermission in Lync Server 2013
ms:assetid: c5801f48-14e3-4fdd-8f14-d52e7af07a57
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205250(v=OCS.15)
ms:contentKeyID: 49301933
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifiche apportate da Grant-CsSetupPermission in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per delegare la configurazione, è possibile concedere autorizzazioni al gruppo universale RTCUniversalServerAdmins per un'unità organizzativa di Active Directory specifica, consentendo ai membri del gruppo RTCUniversalServerAdmins in tale unità organizzativa di installare Lync Server 2013 nel dominio specificato anche senza essere membri del gruppo Domain Admins.

Il cmdlet **Grant-CsSetupPermission** concede al gruppo RTCUniversalServerAdmins le autorizzazioni per un'unità organizzativa, come specificato nella tabella seguente:

### Autorizzazioni concesse a oggetti nell'unità organizzativa

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Le autorizzazioni si applicano a:</th>
<th>Autorizzazioni concesse:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RTCUniversalServerAdmins</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Leggi servicePrincipalName</p></li>
<li><p>Scrivi in servicePrincipalName</p></li>
<li><p>Elimina albero</p></li>
<li><p>Replica modifiche directory</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Oggetti serviceConnectionPoint discendenti</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Autorizzazioni di lettura</p></li>
<li><p>Autorizzazioni di scrittura</p></li>
<li><p>Crea elemento figlio</p></li>
<li><p>Elimina elemento figlio</p></li>
<li><p>Elenca contenuto</p></li>
<li><p>Proprietà di scrittura</p></li>
<li><p>Proprietà di lettura</p></li>
<li><p>Elimina albero</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Oggetti msRTCSIP-Server discendenti</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Proprietà di scrittura</p></li>
<li><p>Proprietà di lettura</p></li>
<li><p>Elimina albero</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Oggetti msRTCSIP-WebComponents discendenti</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Proprietà di scrittura</p></li>
<li><p>Proprietà di lettura</p></li>
<li><p>Elimina albero</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Oggetti msRTCSIP-MCU discendenti</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Proprietà di scrittura</p></li>
<li><p>Proprietà di lettura</p></li>
<li><p>Elimina albero</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Oggetti msRTCSIP-MediationServer discendenti</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Proprietà di scrittura</p></li>
<li><p>Proprietà di lettura</p></li>
<li><p>Elimina albero</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Oggetti msRTCSIP-ApplicationServer discendenti</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Proprietà di scrittura</p></li>
<li><p>Proprietà di lettura</p></li>
<li><p>Elimina albero</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Oggetti msRTCSIP-ConnectionPoint discendenti</p></td>
<td><p>Accesso speciale:</p>
<ul>
<li><p>Proprietà di scrittura</p></li>
<li><p>Proprietà di lettura</p></li>
<li><p>Elimina albero</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Oggetti Computer discendenti</p></td>
<td><p>Accesso speciale per serviceConnectionPoint:</p>
<ul>
<li><p>Crea oggetti figli</p></li>
<li><p>Elimina oggetti figli</p></li>
<li><p>Elimina albero</p></li>
</ul>
<p>Accesso speciale per informazioni pubbliche:</p>
<ul>
<li><p>Proprietà di lettura</p></li>
</ul>
<p>Accesso speciale per il nome host DNS:</p>
<ul>
<li><p>Proprietà di lettura</p></li>
</ul></td>
</tr>
</tbody>
</table>

