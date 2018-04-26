---
title: 'Lync Server 2013: Requisiti DNS per un server Standard Edition'
TOCTitle: Requisiti DNS per un server Standard Edition
ms:assetid: 5d1daf54-6e60-4ce0-9254-7d57a0835fa4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204936(v=OCS.15)
ms:contentKeyID: 49300700
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti DNS per un server Standard Edition in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti i record DNS (Domain Name System) necessari per la distribuzione di server Standard Edition.

## Record DNS per server Standard Edition

Nella tabella seguente vengono specificati i requisiti DNS per la distribuzione di server Standard Edition Lync Server 2013.


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
<td><p>Server Standard Edition</p></td>
<td><p>Un record A interno che risolve il nome di dominio completo (FQDN) del server nel relativo indirizzo IP.</p></td>
</tr>
<tr class="even">
<td><p>Accesso client automatico</p></td>
<td><p>Per ogni dominio SIP supportato, un record SRV per _sipinternaltls._tcp.&lt;domain&gt; sulla porta 5061 corrispondente all'FQDN del server Standard Edition che esegue l'autenticazione e il reindirizzamento delle richieste di accesso dei client. Per informazioni dettagliate, vedere <a href="lync-server-2013-dns-requirements-for-automatic-client-sign-in.md">Requisiti DNS per l'accesso automatico dei client in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Individuazione del servizio Web Aggiornamento dispositivi tramite dispositivi per comunicazioni unificate</p></td>
<td><p>Un record A interno con nome ucupdates-r2.&lt;SIP domain&gt; che si risolve nell'indirizzo IP del server Standard Edition che ospita il servizio Web Aggiornamento dispositivi. Se viene attivato un dispositivo per comunicazioni unificate, ma un utente non ha mai effettuato l'accesso al dispositivo, il record A consente al dispositivo di individuare il server che ospita il servizio Web Aggiornamento dispositivi e ottenere gli aggiornamenti. In caso contrario, i dispositivi ottengono le informazioni del server tramite provisioning di tipo in-band al primo accesso di un utente. Per informazioni dettagliate, vedere <a href="lync-server-2013-device-update-web-service.md">Servizio Web aggiornamento dispositivi in Lync Server 2013</a> nella documentazione relativa alle operazioni.</p></td>
</tr>
<tr class="even">
<td><p>Un proxy inverso per il supporto del traffico HTTP</p></td>
<td><p>Un record A esterno che risolve il nome di dominio completo (FQDN) della Web farm esterna nell'indirizzo IP esterno del proxy inverso. Per informazioni dettagliate, vedere <a href="lync-server-2013-determine-dns-requirements.md">Determinare i requisiti di DNS per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Requisiti DNS per l'accesso automatico dei client in Lync Server 2013](lync-server-2013-dns-requirements-for-automatic-client-sign-in.md)  
[Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md)  

#### Ulteriori risorse

[Servizio Web aggiornamento dispositivi in Lync Server 2013](lync-server-2013-device-update-web-service.md)

