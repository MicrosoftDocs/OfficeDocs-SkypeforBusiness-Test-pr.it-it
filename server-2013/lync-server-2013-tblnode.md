---
title: 'Lync Server 2013: tblNode'
TOCTitle: tblNode
ms:assetid: a31d2961-aa83-4286-a12e-15d279c95f19
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615024(v=OCS.15)
ms:contentKeyID: 49301524
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# tblNode in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In tblNode è contenuto l'albero degli oggetti (con nodi di categorie o chat room) in base ai dati gestiti nel Pannello di controllo di Lync Server 2013 e nei cmdlet amministrativi.

### Colonne

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>nodeID</p></td>
<td><p>int, not null</p></td>
<td><p>ID nodo (numero univoco).</p></td>
</tr>
<tr class="even">
<td><p>nodeGuid</p></td>
<td><p>GUID, not null</p></td>
<td><p>GUID nodo.</p></td>
</tr>
<tr class="odd">
<td><p>parentID</p></td>
<td><p>int</p></td>
<td><p>ID nodo del padre. Il nodo radice (con ID 1) contiene se stesso come padre.</p></td>
</tr>
<tr class="even">
<td><p>nodeType</p></td>
<td><p>bit, not null</p></td>
<td><p>True se il nodo è una categoria.</p>
<p>False se il nodo è una chat room.</p></td>
</tr>
<tr class="odd">
<td><p>nodeName</p></td>
<td><p>nvarchar (256), not null</p></td>
<td><p>Nome nodo.</p></td>
</tr>
<tr class="even">
<td><p>nodeDesc</p></td>
<td><p>nvarchar (256), not null</p></td>
<td><p>Descrizione nodo.</p></td>
</tr>
<tr class="odd">
<td><p>invite</p></td>
<td><p>bit</p></td>
<td><p>Per le categorie:</p>
<ul>
<li><p>True se gli inviti sono attivi.</p></li>
<li><p>False se gli inviti sono inattivi.</p></li>
</ul>
<p>Per le chat room:</p>
<ul>
<li><p>False se gli inviti sono disattivati (la categoria padre viene ignorata).</p></li>
<li><p>Null se l'impostazione degli inviti viene ereditata dalla categoria padre.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>logged</p></td>
<td><p>bit</p></td>
<td><p>Per le categorie:</p>
<ul>
<li><p>True se la cronologia della chat è attiva.</p></li>
<li><p>False se la cronologia della chat è inattiva.</p></li>
</ul>
<p>Per le chat room:</p>
<ul>
<li><p>Null.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>filePost</p></td>
<td><p>bit</p></td>
<td><p>Per le categorie:</p>
<ul>
<li><p>True se i caricamenti di file sono consentiti.</p></li>
<li><p>False se i caricamenti di file non sono consentiti.</p></li>
</ul>
<p>Per le chat room:</p>
<ul>
<li><p>Null.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>disabled</p></td>
<td><p>bit, not null</p></td>
<td><p>True se la chat room è disabilitata. Si applica solo alle chat room. False per le categorie.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>behavior</p></td>
<td><p>smallint, not null</p></td>
<td><p>Comportamento (cercato nella tabella EnumValue):</p>
<ul>
<li><p>4: Normale (chat room normali)</p></li>
<li><p>5: Auditorium (chat room in modalità auditorium, solo i relatori possono contribuire)</p></li>
</ul>
<p>Si applica solo alle chat room.</p></td>
</tr>
<tr class="odd">
<td><p>visibility</p></td>
<td><p>smallint, not null</p></td>
<td><p>Visibilità (cercata nella tabella EnumValue):</p>
<ul>
<li><p>2: Privato</p></li>
<li><p>3: Con ambito</p></li>
<li><p>6: Aperto</p></li>
</ul>
<p>Si applica solo alle chat room.</p></td>
</tr>
<tr class="even">
<td><p>siopID</p></td>
<td><p>GUID</p></td>
<td><p>GUID del componente aggiuntivo, se alla chat room è associato un componente aggiuntivo. Le categorie non hanno componenti aggiuntivi.</p>
<p>Le informazioni relative al componente aggiuntivo vengono cercate nella tabella SiopWhiteList.</p></td>
</tr>
<tr class="odd">
<td><p>nodeAddedBy</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità che ha creato questo nodo.</p></td>
</tr>
<tr class="even">
<td><p>nodeAddedOn</p></td>
<td><p>bigint, not null</p></td>
<td><p>Indicatore di data e ora della creazione del nodo.</p></td>
</tr>
<tr class="odd">
<td><p>nodeUpdatedBy</p></td>
<td><p>int, not null</p></td>
<td><p>ID dell'entità che ha eseguito l'ultimo aggiornamento del nodo.</p></td>
</tr>
<tr class="even">
<td><p>nodeUpdatedOn</p></td>
<td><p>bigint, not null</p></td>
<td><p>Indicatore di data e ora dell'ultimo aggiornamento del nodo.</p></td>
</tr>
<tr class="odd">
<td><p>purgedOn</p></td>
<td><p>datetime</p></td>
<td><p>Ora dell'ultima operazione di eliminazione (rimozione degli ambiti dalla tabella tblScopedPrincipal e dei ruoli dalla tabella tblPrincipalRole) che ha interessato il nodo. Utilizzata dal meccanismo di aggiornamento della cache interna del servizio Chat.</p></td>
</tr>
</tbody>
</table>


### Chiavi

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Colonna</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>nodeID</p></td>
<td><p>Chiave primaria.</p></td>
</tr>
<tr class="even">
<td><p>behavior</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblEnumValue.valueID.</p></td>
</tr>
<tr class="odd">
<td><p>visibility</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblEnumValue.valueID.</p></td>
</tr>
<tr class="even">
<td><p>parentID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblNode.nodeID.</p></td>
</tr>
<tr class="odd">
<td><p>siopID</p></td>
<td><p>Chiave esterna con ricerca nella tabella tblSiopWhiteList.siopId.</p></td>
</tr>
</tbody>
</table>

