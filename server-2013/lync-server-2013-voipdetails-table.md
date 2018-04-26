---
title: 'Lync Server 2013: Tabella VoipDetails'
TOCTitle: Tabella VoipDetails
ms:assetid: 74ffbb71-569b-4018-be1f-4db2bbafcf36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398566(v=OCS.15)
ms:contentKeyID: 49300994
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella VoipDetails in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta una chiamata con due partecipanti di cui almeno uno è un utente VoIP.


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
<td><p><strong>SessionIdTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria/o</p></td>
<td><p>Ora della richiesta di sessione. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco una sessione. Vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Numero di ID per identificare la sessione. Utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromNumberId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p><strong>PhoneId</strong> del chiamante. Per maggiori informazioni, vedere <a href="lync-server-2013-phones-table.md">Tabella Phones in Lync Server 2013</a>. Se questo valore è diverso da NULL e <strong>FromGatewayId</strong> è diverso da NULL, il chiamante è un utente PSTN.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConnectedNumberId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p><strong>PhoneId</strong> del destinatario della chiamata. Per maggiori informazioni, vedere <a href="lync-server-2013-phones-table.md">Tabella Phones in Lync Server 2013</a>. Se questo valore è diverso da NULL e <strong>ToGatewayId</strong> è diverso da NULL, il destinatario della chiamata è un utente PSTN.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromMediationServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Mediation Server da cui proviene la chiamata. Per maggiori informazioni, vedere <a href="lync-server-2013-mediationservers-table.md">Tabella MediationServers in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ToMediationServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Mediation Server a cui andrà la chiamata. Per maggiori informazioni, vedere <a href="lync-server-2013-mediationservers-table.md">Tabella MediationServers in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FromGatewayId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Gateway da cui proviene la chiamata. Per maggiori informazioni, vedere <a href="lync-server-2013-gateways-table.md">Tabella Gateways in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ToGatewayId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Gateway a cui andrà la chiamata. Per maggiori informazioni, vedere <a href="lync-server-2013-gateways-table.md">Tabella Gateways in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DisconnectedbyURIId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>URI dell'utente che ha disconnesso la chiamata, se l'utente dispone di un URI. Per maggiori informazioni, vedere <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DisconnectedbyPhoneId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID del telefono che ha disconnesso la chiamata se la chiamata è stata disconnessa da un telefono. Per maggiori informazioni, vedere <a href="lync-server-2013-phones-table.md">Tabella Phones in Lync Server 2013</a>.</p></td>
</tr>
</tbody>
</table>

