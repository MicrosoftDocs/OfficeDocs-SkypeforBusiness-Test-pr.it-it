---
title: 'Lync Server 2013: Tabella MediaLine'
TOCTitle: Tabella MediaLine
ms:assetid: 414b1d63-ae97-4c27-bac0-c9ad0f808ff0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425920(v=OCS.15)
ms:contentKeyID: 49300328
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tabella MediaLine in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni record rappresenta una linea multimediale. In una sessione audio in genere è inclusa una linea multimediale audio, mentre in una sessione audio e video (A/V) in genere sono incluse una linea multimediale audio e una linea multimediale video, anche se vi potrebbero essere due linee multimediali video in caso di utilizzo del dispositivo per conferenze o della visualizzazione Raccolta.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Colonna</strong></th>
<th><strong>Tipo di dati</strong></th>
<th><strong>Chiave/indice</strong></th>
<th><strong>Dettagli</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConferenceDateTime</strong></p></td>
<td><p>datetime</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-session-table.md">Tabella Session in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionSeq</strong></p></td>
<td><p>int</p></td>
<td><p>Primaria/o</p></td>
<td><p>Riferimento dalla <a href="lync-server-2013-session-table.md">Tabella Session in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MediaLineLabel</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Primaria/o</p></td>
<td><p>0 indica audio principale, 1 indica video principale, 2 indica panoramica e 3 indica condivisione appliczione/desktop. Questa etichetta deve essere univoca in una singola sessione.</p></td>
</tr>
<tr class="even">
<td><p><strong>ConnectivityIce</strong></p></td>
<td><p>tinyint</p></td>
<td><p> </p></td>
<td><p>Questa colonna è presente ma non utilizzata in Microsoft Lync Server 2013. Le informazioni sulla connettività utilizzata per una linea multimediale vengono acquisite nelle colonne CallerConnectivityICE e CalleeConnectivityICE.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerIceWarningFlags</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Informazioni sul processo ICE (Interactive Connectivity Establishment) descritto nei flag di bit. Per informazioni dettagliate, vedere la <em>Specifica del protocollo Quality of Experience Monitoring Server</em> , disponibile per il download.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeIceWarningFlags</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Uguale a CallerIceWarningFlags, ma sul lato del destinatario della chiamata. Per informazioni dettagliate, vedere la <em>Specifica del protocollo Quality of Experience Monitoring Server</em> , disponibile per il download.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Security</strong></p></td>
<td><p>tinyint</p></td>
<td><p> </p></td>
<td><p>Profilo di sicurezza in uso. 0 per NESSUNA, 1 per SRTP, 2 per V1.</p></td>
</tr>
<tr class="even">
<td><p><strong>Transport</strong></p></td>
<td><p>tinyint</p></td>
<td><p> </p></td>
<td><p>0 per UDP, 1 per TCP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo IP del chiamante. Per ulteriori informazioni, vedere la <a href="lync-server-2013-ipaddress-table.md">Tabella IPAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerPort</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Porta utilizzata dal chiamante.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerSubnet</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Subnet del chiamante. Per ulteriori informazioni, vedere la <a href="lync-server-2013-ipaddress-table.md">Tabella IPAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerInside</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>1 indica che il chiamante è all'interno della rete aziendale, 0 invece indica che è all'esterno della rete.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerMacAddress</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo MAC del chiamante. Riferimento dalla <a href="lync-server-2013-macaddress-table.md">Tabella MacAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerRelayIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo IP del servizio A/V Edge Lync Server utilizzato dal chiamante. Per ulteriori informazioni, vedere la <a href="lync-server-2013-ipaddress-table.md">Tabella IPAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerRelayPort</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Porta utilizzata nel servizio A/V Edge dal chiamante.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerCaptureDev</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Dispositivo di acquisizione utilizzato dal chiamante. Riferimento dalla <a href="lync-server-2013-device-table.md">Tabella Device in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerRenderDev</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Dispositivo di rendering utilizzato dal chiamante. Riferimento dalla <a href="lync-server-2013-device-table.md">Tabella Device in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerCaptureDevDriver</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Driver del dispositivo di acquisizione del chiamante. Riferimento dalla <a href="lync-server-2013-devicedriver-table.md">Tabella DeviceDriver in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerRenderDevDriver</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Driver del dispositivo di rendering del chiamante. Riferimento dalla <a href="lync-server-2013-devicedriver-table.md">Tabella DeviceDriver in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerNetworkConnectionType</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Esterna</p></td>
<td><p>Indica il tipo di connessione di rete utilizzato dal chiamante. I valori sono tratti dalla <a href="lync-server-2013-networkconnectiondetail-table.md">Tabella NetworkConnectionDetail in Lync Server 2013</a>. I valori tipici sono 0 per una connessione cablata, 1 per una connessione WiFi e 3 per una connessione Ethernet.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerBssid</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>BSSID del chiamante se viene utilizzata una rete wireless. Riferimento dalla <a href="lync-server-2013-macaddress-table.md">Tabella MacAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerVPN</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Collegamento del chiamante. 1 indica una rete privata virtuale (VPN), 0 indica una rete non VPN.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerLinkSpeed</strong></p></td>
<td><p>decimal(18,0)</p></td>
<td><p></p></td>
<td><p>Velocità del collegamento delle rete, in bps, per l'endpoint del chiamante.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo IP del destinatario della chiamata. Per ulteriori informazioni, vedere la <a href="lync-server-2013-ipaddress-table.md">Tabella IPAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleePort</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Porta utilizzata dal destinatario della chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeSubnet</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Subnet del destinatario della chiamata. Per ulteriori informazioni, vedere la <a href="lync-server-2013-ipaddress-table.md">Tabella IPAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeInside</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>1 indica che il destinatario della chiamata è all'interno della rete aziendale, 0 invece indica che è all'esterno della rete.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeMacAddress</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo MAC del destinatario della chiamata. Riferimento dalla <a href="lync-server-2013-macaddress-table.md">Tabella MacAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeRelayIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo IP del servizio A/V Edge utilizzato dal destinatario della chiamata. Per ulteriori informazioni, vedere la <a href="lync-server-2013-ipaddress-table.md">Tabella IPAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeRelayPort</strong></p></td>
<td><p>int</p></td>
<td><p> </p></td>
<td><p>Porta utilizzata nel servizio A/V Edge dal destinatario della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeCaptureDev</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Dispositivo di acquisizione utilizzato dal destinatario della chiamata. Riferimento dalla <a href="lync-server-2013-device-table.md">Tabella Device in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeRenderDev</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Dispositivo di rendering utilizzato dal destinatario della chiamata. Riferimento dalla <a href="lync-server-2013-device-table.md">Tabella Device in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeCaptureDevDriver</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Driver del dispositivo di acquisizione del destinatario della chiamata. Riferimento dalla <a href="lync-server-2013-devicedriver-table.md">Tabella DeviceDriver in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeRenderDevDriver</strong></p></td>
<td><p>varchar(256)</p></td>
<td><p>Esterna</p></td>
<td><p>Driver del dispositivo di rendering del destinatario della chiamata. Riferimento dalla <a href="lync-server-2013-devicedriver-table.md">Tabella DeviceDriver in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeNetworkConnectionType</strong></p></td>
<td><p>tinyint</p></td>
<td><p>Esterna</p></td>
<td><p>Indica il tipo di connessione di rete utilizzato dal destinatario della chiamata. I valori sono tratti dalla <a href="lync-server-2013-networkconnectiondetail-table.md">Tabella NetworkConnectionDetail in Lync Server 2013</a>. I valori tipici sono 0 per una connessione cablata, 1 per una connessione WiFi e 3 per una connessione Ethernet.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeBssid</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>BSSID del destinatario della chiamata se viene utilizzata una rete wireless. Riferimento dalla <a href="lync-server-2013-macaddress-table.md">Tabella MacAddress in Lync Server 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeVPN</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Collegamento del destinatario della chiamata. 1 indica una rete privata virtuale (VPN), 0 indica una rete non VPN.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeLinkSpeed</strong></p></td>
<td><p>decimal(18,0)</p></td>
<td><p> </p></td>
<td><p>Velocità del collegamento delle rete, in bps, per l'endpoint del destinatario della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConversationalMOS</strong></p></td>
<td><p>decimal(3,2)</p></td>
<td><p> </p></td>
<td><p>Conversational MOS a banda stretta delle sessioni audio (basato su entrambi i flussi audio).</p></td>
</tr>
<tr class="even">
<td><p><strong>AppliedBandwidthLimit</strong></p></td>
<td><p>int</p></td>
<td><p></p></td>
<td><p>Questa è la larghezza di banda effettivamente applicata al flusso sul lato dell'invio secondo diverse impostazioni di criteri (TURN, API, SDP, server dei criteri e così via). Da non confondere con la larghezza di banda effettiva, perché può esistere una larghezza di banda effettiva inferiore basata sulla stima della larghezza di banda. Si tratta in pratica della larghezza di banda massima che può essere utilizzata dal flusso di invio escludendo i limiti imposti dalla stima della larghezza di banda.</p></td>
</tr>
<tr class="odd">
<td><p><strong>AppliedBandwidthSourceKey</strong></p></td>
<td><p>smallint</p></td>
<td><p></p></td>
<td><p>Questa è l'origine del limite di larghezza di banda imposto. Descrive la provenienza del limite della larghezza di banda, ovvero server dei criteri, server TURN, modalità e così via. Riferimento dalla <a href="lync-server-2013-appliedbandwidthsource-table.md">Tabella AppliedBandwidthSource in Lync Server 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Caller</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Indica se è stata ricevuta la metrica del chiamante. 1 indica sì, un valore Null indica no.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Callee</strong></p></td>
<td><p>bit</p></td>
<td><p> </p></td>
<td><p>Indica se è stata ricevuta la metrica del destinatario della chiamata. 1 indica sì, un valore Null indica no.</p></td>
</tr>
<tr class="even">
<td><p><strong>MidCallReport</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Indica se il rapporto riguarda l'intera sessione o una parte di essa.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClassifiedPoorCall</strong></p></td>
<td><p>bit</p></td>
<td><p></p></td>
<td><p>Indica se una chiamata è stata classificata come insufficiente (valore 1) o come buona (0).</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerConnectivityICE</strong></p></td>
<td><p>tinyInt</p></td>
<td><p></p></td>
<td><p>Indica se il chiamante connesso alla rete sta utilizzando il protocollo ICE (Internet Connectivity Establishment).</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeConnectivityICE</strong></p></td>
<td><p>tinyint</p></td>
<td><p></p></td>
<td><p>Indica se il chiamante connesso alla rete sta utilizzando il protocollo ICE (Internet Connectivity Establishment).</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerReflexiveLocalIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo IP riflessivo dell'utente che ha effettuato la chiamata. Nelle organizzazioni che utilizzano NAT (network address translation), l'indirizzo IP riflessivo è l'indirizzo IP del server proxy.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CallerWiFiDriverDevicesDesc</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Descrizione del dispositivo per il driver WiFi impiegato dall'utente che ha effettuato la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>CallerWiFiDriverVersion</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero di versione del driver WiFi impiegato dall'utente che ha effettuato la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleReflexiveLocalIPAddr</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Indirizzo IP riflessivo dell'utente che ha ricevuto la chiamata. Nelle organizzazioni che utilizzano NAT (network address translation), l'indirizzo IP riflessivo è l'indirizzo IP del server proxy.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><strong>CalleeWiFiDriverDevicesDesc</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Descrizione del dispositivo per il driver WiFi impiegato dall'utente che ha ricevuto la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CalleeWiFiDriverVersion</strong></p></td>
<td><p>int</p></td>
<td><p>Esterna</p></td>
<td><p>Numero di versione del driver WiFi impiegato dall'utente che ha ricevuto la chiamata.</p>
<p>Questa colonna è stata introdotta in Microsoft Lync Server 2013.</p></td>
</tr>
</tbody>
</table>

