---
title: Set-CsEdgeServer
TOCTitle: Set-CsEdgeServer
ms:assetid: cbe140a4-8ce6-4e20-913b-b1ffb58e6698
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398859(v=OCS.15)
ms:contentKeyID: 49301987
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsEdgeServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà per uno o più server perimetrali. Tali server vengono utilizzati per fornire connettività tra la rete interna e Internet. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsEdgeServer [-Identity <XdsGlobalRelativeIdentity>] [-AccessEdgeClientSipPort <UInt16>] [-AccessEdgeExternalSipPort <UInt16>] [-AccessEdgeInternalSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomClientPort <UInt16>] [-DataPsomServerPort <UInt16>] [-Force <SwitchParameter>] [-MediaCommunicationPortCount <UInt16>] [-MediaCommunicationPortStart <UInt16>] [-MediaRelayAuthEdgePort <UInt16>] [-MediaRelayExternalTurnTcpPort <UInt16>] [-MediaRelayExternalTurnUdpPort <UInt16>] [-MediaRelayInternalTurnTcpPort <UInt16>] [-MediaRelayInternalTurnUdpPort <UInt16>] [-Registrar <String>] [-WhatIf [<SwitchParameter>]] [-XmppInternalPort <UInt16>] [-XmppListeningPort <UInt16>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono cambiate le porte SIP interne ed esterne del server perimetrale "EdgeServer:atl-edge-001.litwareinc.com".

    Set-CsEdgeServer -Identity "EdgeServer:atl-edge-001.litwareinc.com" -AccessEdgeInternalSipPort 5062 -AccessEdgeExternalSipPort 5062

## ESEMPIO 2

Nell'esempio 2 vengono modificate le porte SIP interne ed esterne per tutti i server perimetrali situati nel sito di Redmond. A tale scopo, vengono utilizzati innanzitutto il cmdlet **Get-CsService** e il parametro EdgeServer per restituire una raccolta di tutti i server perimetrali attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i server perimetrali del sito Redmond, ovvero i siti con proprietà SiteId uguale a site:Redmond. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **For-Each-Object**. Questo cmdlet esegue il cmdlet **Set-CsEdgeServer** in ogni server della raccolta, cambiando i valori assegnati alle proprietà AccessInternalSipPort e AccessExternalSipPort.

    Get-CsService -EdgeServer | Where-Object {$_.SiteId -eq "site:Redmond"} | ForEach-Object {Set-CsEdgeServer -Identity $_.Identity -AccessEdgeInternalSipPort 5062 -AccessEdgeExternalSipPort 5062}

## Descrizione dettagliata

La connettività con il mondo esterno, ovvero Internet, è un aspetto importante di Lync Server. Senza questa connettività, gli utenti dovrebbero connettersi alla rete interna per poter accedere a Lync Server. In questo modo per gli utenti che lavorano fuori sede sarebbe difficile utilizzare il software e impedirebbe agli utenti che non dispongono di account nel dominio di partecipare alle conferenze. Analogamente, senza la connettività con il mondo esterno gli utenti non sarebbero in grado di scambiare messaggi istantanei con i partner federati o con le persone che dispongono di account in un sistema pubblico di messaggistica istantanea, ad esempio Yahoo\!, AOL o MSN.

I server perimetrali garantiscono la connettività tra la rete interna e Internet. Il cmdlet **Set-CsEdgeServer** consente di modificare le impostazioni di configurazione dei server perimetrali, un'attività che consiste principalmente nel modificare i numeri di porta utilizzati per trasmettere il traffico di rete.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsEdgeServer** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsEdgeServer"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AccessEdgeClientSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per le comunicazioni SIP tra server perimetrale e i dispositivi client. Il valore iniziale viene impostato in Generatore di topologie, ma può essere modificato specificando un nuovo valore per il parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>AccessEdgeExternalSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico SIP esterno. Il valore predefinito è 5061.</p></td>
</tr>
<tr class="odd">
<td><p><em>AccessEdgeInternalSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico SIP interno. Il valore predefinito è 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DataPsomClientPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per le comunicazioni PSOM (Persistent Shared Object Model) tra server perimetrale e i dispositivi client. Il valore iniziale viene impostato in Generatore di topologie, ma può essere modificato specificando un nuovo valore per il parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomServerPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per le comunicazioni PSOM tra il server perimetrale e altri server.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Posizione del servizio del server perimetrale da modificare. Ad esempio: -Identity &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p>
<p>È possibile omettere il prefisso &quot;EdgeServer:&quot; quando si specifica un server perimetrale, ad esempio -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>MediaCommunicationPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero totale di porte allocate per le comunicazioni multimediali nel perimetro esterno. Il valore predefinito è 10000.</p></td>
</tr>
<tr class="even">
<td><p><em>MediaCommunicationPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero di porta iniziale per le comunicazioni multimediali nel perimetro esterno. Il valore predefinito è 50000.</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaRelayAuthEdgePort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per l'autenticazione Media Relay. Il valore predefinito è 5062.</p></td>
</tr>
<tr class="even">
<td><p><em>MediaRelayExternalTurnTcpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico esterno di Media Relay tramite TCP (Transmission Control Protocol). Il valore predefinito è 444 se al server perimetrale è associato un solo indirizzo IP. Se al server perimetrale sono associati più indirizzi IP, il valore predefinito è 443. Questi valori vengono impostati inizialmente in Generatore di topologie, ma possono essere modificati specificando un nuovo valore per il parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaRelayExternalTurnUdpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico esterno di Media Relay tramite UDP (User Datagram Protocol). Il valore predefinito è 3478.</p></td>
</tr>
<tr class="even">
<td><p><em>MediaRelayInternalTurnTcpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico interno di Media Relay tramite TCP. Il valore predefinito è 443.</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaRelayInternalTurnUdpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico interno di Media Relay tramite UDP. Il valore predefinito è 3478.</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio di registrazione da associare al server perimetrale. Ad esempio: -Registrar &quot;Registrar:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
<tr class="even">
<td><p><em>XmppInternalPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico XMPP interno. XMPP (extensible Messaging and Presence Protocol) è un protocollo di comunicazione standard aperto per lo scambio di messaggi XML. Un partner consentito è un provider di presenza e messaggistica istantanea i cui utenti possono scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Lync Server. Il valore predefinito è 5098.</p></td>
</tr>
<tr class="odd">
<td><p><em>XmppListeningPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa per il traffico XMPP.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsEdgeServer** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsEdgeServer** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayEdgeServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

