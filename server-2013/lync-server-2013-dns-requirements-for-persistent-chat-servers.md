---
title: Requisiti DNS per il server chat persistente
TOCTitle: Requisiti DNS per il server chat persistente
ms:assetid: f7531374-d7ed-4b63-ae81-02294cb4496a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205391(v=OCS.15)
ms:contentKeyID: 49302515
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti DNS per il server chat persistente

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti i record DNS (Domain Name System) necessari per la distribuzione di server Chat persistente.

## Record DNS per i server chat persistente

Nella tabella seguente vengono specificati i requisiti DNS per la distribuzione di server Chat persistente.

### Requisiti DNS per un server chat persistente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scenario di distribuzione</th>
<th>Requisito DNS</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Un server chat persistente</p></td>
<td><p>Un record A interno che risolve il nome di dominio completo (FQDN) del server nel relativo indirizzo IP.</p></td>
</tr>
<tr class="even">
<td><p>Pool chat persistente</p></td>
<td><p>Un record A interno che risolve il nome di dominio completo (FQDN) dei server nel relativo indirizzo IP.</p>
<p><strong>Esempio</strong></p>
<p>PersistentChatServer01.contoso.com     10.10.10.1</p>
<p>PersistentChatServer02.contoso.com     10.10.10.2</p>
<p>Un record A interno che risolve il nome di dominio completo (FQDN) dei server nel relativo indirizzo IP.</p>
<p><strong>Esempio</strong></p>
<p>PersistentChatPool.contoso.com    10.10.10.1</p>
<p>PersistentChatPool.contoso.com    10.10.10.2</p></td>
</tr>
</tbody>
</table>

