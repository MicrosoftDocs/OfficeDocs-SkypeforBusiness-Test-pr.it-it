---
title: 'Lync Server 2013: Tabella Registration'
TOCTitle: Tabella Registration
ms:assetid: 05ff9dd3-1aaa-4af0-bd69-8789fb8eaeb3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398114(v=OCS.15)
ms:contentKeyID: 49299566
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella Registration in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta un evento di registrazione utente.


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
<td><p>Primaria, esterna</p></td>
<td><p>Ora della richiesta di sessione. Valore utilizzato in combinazione con <strong>SessionIdSeq</strong> per identificare in modo univoco una sessione. Vedere la <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a> per ulteriori informazioni.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionIdSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria, esterna</p></td>
<td><p>Numero di ID per identificare la sessione. Utilizzato in combinazione con <strong>SessionIdTime</strong> per identificare in modo univoco una sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-dialogs-table.md">Tabella Dialogs in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID utente. Per ulteriori informazioni, vedere la <a href="lync-server-2013-users-table.md">Tabella Users in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>EndpointId</strong></p></td>
<td><p>uniqueidentifier</p></td>
<td><p></p></td>
<td><p>GUID per identificare un endpoint di registrazione. L'evento di registrazione dallo stesso computer dello stesso utente in genere avrà lo stesso ID endpoint. Computer diversi hanno un ID endpoint diverso.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EndpointEra</strong></p></td>
<td><p>uniqueIdentifier</p></td>
<td><p></p></td>
<td><p>ID utilizzato per distinguere le registrazioni che interessano lo stesso utente e lo stesso endpoint.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersionId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Versione client dell'utente corrente. Per ulteriori informazioni, vedere la <a href="lync-server-2013-clientversions-table.md">Tabella ClientVersions in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RegistrarId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID del server di registrazione utilizzato per la registrazione. Per ulteriori informazioni, vedere la <a href="lync-server-2013-servers-table.md">Tabella Servers in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>PoolId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>ID del pool in cui è stata acquisita la sessione. Per ulteriori informazioni, vedere <a href="lync-server-2013-pools-table.md">Tabella Pools in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeServerId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Server perimetrale attraverso il quale passa la registrazione. Per ulteriori informazioni, vedere la <a href="lync-server-2013-edgeservers-table.md">Tabella EdgeServers in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>IsInternal</strong></p></td>
<td><p>Bit</p></td>
<td><p></p></td>
<td><p>Se l'utente è connesso o meno dall'interno.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsUserServiceAvailable</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Se il servizio utente è disponibile o meno.</p></td>
</tr>
<tr class="even">
<td><p><strong>IsPrimaryRegistrar</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Se registrare o meno nella funzione di registrazione principale.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IsPrimaryRegistrarCentral</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Indica se l'utente è registrato o meno con un Survivable Branch Appliance.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>RegisterTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Data/ora di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeRegisterTime</strong></p></td>
<td><p>datetime</p></td>
<td><p></p></td>
<td><p>Data/ora di annullamento della registrazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>ResponseCode</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Codice di risposta della richiesta di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DiagnosticId</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>ID diagnostica della richiesta di registrazione. Indica il tipo di informazioni diagnostiche.</p></td>
</tr>
<tr class="even">
<td><p><strong>DeviceId</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Dispositivo da cui proviene la richiesta di registrazione. Per ulteriori informazioni, vedere la <a href="lync-server-2013-devices-table.md">Tabella Devices in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeRegisterTypeId</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Esterna</p></td>
<td><p>Motivo dell'annullamento della registrazione, ad esempio 'user initiated' (avviato dall'utente), 'registration expired' (registrazione scaduta), 'client fail' (problema del client) e così via. Per ulteriori informazioni, vedere la <a href="lync-server-2013-deregistertype-table.md">Tabella DeRegisterType in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>IPAddress</strong></p></td>
<td><p>nvarchar(256)</p></td>
<td><p></p></td>
<td><p>Indirizzo IP dell'endpoint con cui l'utente è registrato. Può essere un indirizzo IPv4 o IPv6.</p>
<p>Questo campo è stato introdotto in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

