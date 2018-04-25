---
title: Requisiti DNS per server Standard Edition
TOCTitle: Requisiti DNS per server Standard Edition
ms:assetid: 3d6bbe65-e7ce-491b-a0bd-d2f7197f240d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425900(v=OCS.15)
ms:contentKeyID: 49300277
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti DNS per server Standard Edition

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questa sezione vengono descritti i record DNS (Domain Name System) necessari per la distribuzione di server Standard Edition.

## Record DNS per server Standard Edition

Nella tabella seguente vengono specificati i requisiti DNS per la distribuzione di server Standard Edition Lync Server 2013.

### Requisiti DNS per un server Standard Edition

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
<td><p>Per ogni dominio SIP supportato, un record SRV per _sipinternaltls._tcp.<em>&lt;dominio&gt;</em> sulla porta 5061 che esegue il mapping all'FQDN del server Standard Edition che autentica e reindirizza le richieste client per l'accesso. Per informazioni dettagliate, vedere <a href="lync-server-2013-dns-requirements-for-automatic-client-sign-in.md">Requisiti DNS per l'accesso automatico dei client in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Individuazione del servizio Web Aggiornamento dispositivi da parte di dispositivi per comunicazioni unificate</p></td>
<td><p>Un record A interno con nome ucupdates-r2.<em>&lt;dominio SIP&gt;</em> che si risolve nell'indirizzo IP del server Standard Edition che ospita il servizio Web Aggiornamento dispositivi. Se viene attivato un dispositivo per comunicazioni unificate, ma un utente non ha mai effettuato l'accesso al dispositivo, il record A consente al dispositivo di individuare il server che ospita il servizio Web Aggiornamento dispositivi e ottenere gli aggiornamenti. In caso contrario, i dispositivi ottengono le informazioni del server tramite provisioning di tipo in-band al primo accesso di un utente.</p></td>
</tr>
<tr class="even">
<td><p>Proxy inverso per il supporto del traffico HTTP</p></td>
<td><p>Un record A esterno che risolve l'FQDN della Web farm esterna nell'indirizzo IP esterno del proxy inverso. I client e i dispositivi per comunicazioni unificate utilizzano questo record per la connessione al proxy inverso. Per informazioni dettagliate, vedere <a href="lync-server-2013-determine-dns-requirements.md">Determinare i requisiti di DNS per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</p></td>
</tr>
</tbody>
</table>

