---
title: Set-CsMediationServer
TOCTitle: Set-CsMediationServer
ms:assetid: 13efdd9d-ba26-4c93-b0b9-b6e4739bb630
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398213(v=OCS.15)
ms:contentKeyID: 49299754
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMediationServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le proprietà di uno o più server Mediation Server. I server Mediation Server vengono utilizzati per instradare il traffico tra l'infrastruttura interna di VoIP aziendale e un gateway PSTN (Public Switched Telephone Network) o un trunk SIP. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsMediationServer [-Identity <XdsGlobalRelativeIdentity>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-Confirm [<SwitchParameter>]] [-EdgeServer <String>] [-Force <SwitchParameter>] [-Registrar <String>] [-SipClientTcpPort <UInt16>] [-SipClientTlsPort <UInt16>] [-SipServerPort <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di impostare la porta TCP del client SIP su 5072 per il server Mediation Server MediationServer:atl-cs-001.litwareinc.com. Dopo aver modificato la porta sarà necessario riavviare Mediation service di Lync Server.

    Set-CsMediationServer -Identity "MediationServer:atl-cs-001.litwareinc.com" -SipClientTcpPort 5072

## ESEMPIO 2

Nell'esempio 2 vengono configurate le impostazioni delle porte audio per il server Mediation Server MediationServer:atl-cs-001.litwareinc.com. In questo esempio la porta audio iniziale è impostata su 60000 e il numero totale di porte allocate per l'audio è 1000

    Set-CsMediationServer -Identity "MediationServer:atl-cs-001.litwareinc.com" -AudioPortStart 60000 -AudioPortCount 1000

## Descrizione dettagliata

I Mediation Server fungono da collegamento tra la configurazione di VoIP aziendale interna e un gateway PSTN, IP-PBX o trunk SIP. In questo modo, gli utenti di VoIP aziendale che utilizzano dispositivi VoIP possono comunicare con persone che utilizzano cellulari o telefoni con linea terrestre standard. Il cmdlet **Set-CsMediationServer** consente di apportare modifiche a un Mediation Server esistente. In particolare, è possibile modificare le porte utilizzate per comunicare con i dispositivi client, i Front End Server e i peer gateway. Se necessario, è possibile utilizzare il cmdlet **Set-CsMediationServer** anche per associare un server Mediation Server a un nuovo server di registrazione o server perimetrale.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsMediationServer** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMediationServer"}

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
<td><p><em>AudioPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero totale di porte allocate per l'invio e la ricezione di traffico audio. Il numero di porte effettive da aprire inizia con il valore configurato per AudioPortStart e continua con il numero di porte specificato per AudioPortCount. Ad esempio, se AudioPortStart è impostato su 60000 e AudioPortCount è impostato su 100, per il traffico audio verranno utilizzate le porte da 600000 a 60099 incluse.</p>
<p>Sono necessarie minimo sette porte multimediali per l'inoltro di una singola chiamata audio:</p>
<p>Due porte gateway. Una porta è necessaria per il traffico con protocollo RTP (real-time transport protocol) e una è necessaria per il traffico con protocollo RTPC (real-time transport control protocol).</p>
<p>Due porte di trasmissione UDP (User Datagram Protocol), una per il traffico RTP e una per il traffico RTCP.</p>
<p>Una porta di trasmissione TCP (Transmission Control Protocol). Una singola porta di trasmissione TCP può gestire sia il traffico RTP che RTCP.</p>
<p>Due porte locali per l'interfaccia di rete, una per il traffico RTP e una per il traffico RTCP</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La prima di una serie di porte allocate per l'invio e la ricezione di traffico audio. Ad esempio: –AudioPortStart 60000.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EdgeServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità del servizio di server perimetrale da associare con Mediation Server. Ad esempio: -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p></td>
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
<td><p>Percorso di installazione del Mediation Server da modificare. Ad esempio: -Identity &quot;MediationServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Si noti che è possibile non utilizzare il prefisso &quot;MediationServer:&quot; quando si specifica un Mediation Server. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Registrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità del servizio di Registrar da associare con Mediation Server. Ad esempio: -Registrar &quot;Registrar:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>SipClientTcpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa utilizzata per la comunicazione con il gateway peer utilizzando TCP. Per impostazione predefinita, non viene definita nessuna porta TCP; tuttavia una porta TCP con numero di porta 5068 verrà creata automaticamente durante la creazione del gateway PSTN. Se si modifica SipClientTcpPort sarà necessario riavviare il servizio Mediation Server prima che la nuova porta venga realmente utilizzata.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipClientTlsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa utilizzata per comunicare con i gateway peer utilizzando il protocollo TLS (Transport Layer Security). Per impostazione predefinita, SipClientTlsPort viene configurato per utilizzare la porta 5067. Se si modifica SipClientTlsPort sarà necessario riavviare il servizio Mediation Server prima che la nuova porta venga realmente utilizzata.</p></td>
</tr>
<tr class="even">
<td><p><em>SipServerPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa utilizzata per comunicare con Front End Server. Per impostazione predefinita, il parametro SipServerPort viene configurato per utilizzare la porta 5070. Se si modifica il valore di SipServerPort, sarà necessario riavviare il servizio Mediation Server prima che la nuova porta venga utilizzata.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsMediationServer** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Set-CsMediationServer** non restituisce oggetti o valori. Il cmdlet invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayMediationServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

