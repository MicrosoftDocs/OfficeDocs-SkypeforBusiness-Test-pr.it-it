---
title: Set-CsApplicationServer
TOCTitle: Set-CsApplicationServer
ms:assetid: 74b3f941-df06-4fde-9487-eba081233723
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398562(v=OCS.15)
ms:contentKeyID: 49300988
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsApplicationServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare le proprietà di configurazione di uno o più server che eseguono il Servizio applicazione. Questi server (noti anche come server applicazioni) ospitano programmi software, come l'applicazione Parcheggio di chiamata, che sono stati sviluppati utilizzando il set di Microsoft Unified Communications Managed API (UCMA). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsApplicationServer [-Identity <XdsGlobalRelativeIdentity>] [-ApplicationDatabase <String>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AtsSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-CaaSipPort <UInt16>] [-CasSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-CpsSipPort <UInt16>] [-Force <SwitchParameter>] [-PdpSipPort <UInt16>] [-PdpTurnPort <UInt16>] [-Registrar <String>] [-RgsSipPort <UInt16>] [-RgsWcfMtlsPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di configurare la porta SIP per applicazione Annuncio conferenza sul server applicazioni ApplicationServer:atl-cs-001.litwareinc.com to 5074.

    Set-CsApplicationServer -Identity "ApplicationServer:atl-cs-001.litwareinc.com" -CasSipPort 5074 

## ESEMPIO 2

Nell'esempio 2 vengono configurate le porte audio per il server applicazioni ApplicationServer:atl-cs-001.litwareinc.com. In questo esempio la porta audio iniziale è impostata su 49500 e in totale sono 5500 le porte riservate al traffico audio.

    Set-CsApplicationServer -Identity "ApplicationServer:atl-cs-001.litwareinc.com" -AudioPortStart 49500 -AudioPortCount 5500 

## ESEMPIO 3

Nell'esempio 3 la porta SIP dell'applicazione Annuncio conferenza viene impostata su 5074 per tutti i server applicazioni dell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsService** per ottenere una raccolta di tutti i server applicazioni attualmente in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object** che, per ogni singolo server nella raccolta, utilizza il cmdlet **Set-CsApplicationServer** per impostare la porta SIP dell'applicazione Annuncio conferenza su 5074.

    Get-CsService -ApplicationServer | ForEach-Object {Set-CsApplicationServer -Identity $_.Identity -CasSipPort 5074} 

## Descrizione dettagliata

Il Servizio applicazione ospita alcuni programmi di Lync Server che non fanno parte dei componenti server di base. Tra questi programmi vi sono l'applicazione Response Group, l'applicazione Operatore Conferenza e l'applicazione Annuncio conferenza. Il Servizio applicazione accetta questi programmi e li integra completamente nell'ambiente Lync Server.

Il cmdlet **Set-CsApplicationServer** consente agli amministratori di modificare le impostazioni di configurazione di qualunque server applicazioni distribuito nell'organizzazione. Ad esempio, è possibile modificare le porte usate per audio, video e condivisione delle applicazioni oppure assegnare nuovi valori alle porte usate per singole applicazioni, come applicazione Operatore Conferenza o applicazione Annuncio conferenza. Si noti che ogni volta che si modificano le porte sarà poi necessario riavviare i relativi servizi.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsApplicationServer** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsApplicationServer"}

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
<td><p><em>ApplicationDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio di database applicazione. Ad esempio: -ApplicationDatabase &quot;ApplicationDatabase:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero totale di porte allocate per la condivisione delle applicazioni. Il numero di porte effettive da aprire inizia con il valore configurato per AudioPortStart e continua con il numero di porte specificato per AudioPortCount. Ad esempio, se AppSharingPortStart è impostato su 60000 e AppSharingPortCount è impostato su 100, per la condivisione delle applicazioni verranno utilizzate le porte da 60000 a 60099.</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La prima di una serie di porte allocate per la condivisione delle applicazioni. Ad esempio: –AppSharingPortStart 60000.</p></td>
</tr>
<tr class="even">
<td><p><em>AtsSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata dal servizio test audio.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero totale di porte allocate per l'invio e la ricezione di traffico audio. Il numero di porte effettive da aprire inizia con il valore configurato per AudioPortStart e continua con il numero di porte specificato per AudioPortCount. Ad esempio, se AudioPortStart è impostato su 60000 e AudioPortCount è impostato su 100, per il traffico audio verranno utilizzate le porte da 600000 a 60099.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La prima di una serie di porte allocate per l'invio e la ricezione di traffico audio. Ad esempio: –AudioPortStart 60000.</p></td>
</tr>
<tr class="odd">
<td><p><em>CaaSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata da applicazione Operatore Conferenza, usata per collegare gli utenti ad una conferenza telefonica con accesso esterno.</p></td>
</tr>
<tr class="even">
<td><p><em>CasSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata da applicazione Annuncio conferenza, usata per riprodurre gli annunci (ad esempio, &quot;Davide Garghentini ha lasciato la conferenza&quot;) durante una conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CpsSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La porta SIP utilizzata per il servizio Parcheggio di chiamata. Il servizio Parcheggio di chiamata consente di mettere in attesa una chiamata su un telefono e riprendere la stessa chiamata da un altro telefono.</p></td>
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
<td><p>Percorso di installazione del server applicazioni da modificare. Ad esempio: -Identity &quot;ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Si noti che è possibile non utilizzare il prefisso &quot;ApplicationServer:&quot; quando si specifica un server applicazioni. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>PdpSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata dal server PDP (Policy Decision Point, punto di decisione criteri). Il server PDP (Policy Decision Point, punto di decisione criteri) viene utilizzato per la gestione della larghezza di banda.</p></td>
</tr>
<tr class="even">
<td><p><em>PdpTurnPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La porta traffico Turn utilizzata dal server PDP (Policy Decision Point, punto di decisione criteri).</p></td>
</tr>
<tr class="odd">
<td><p><em>Registrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo della funzione di registrazione associata al server PDP (Policy Decision Point, punto di decisione criteri).</p></td>
</tr>
<tr class="even">
<td><p><em>RgsSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata da applicazione Response Group. applicazione Response Group consente di indirizzare le chiamate telefoniche in arrivo a uno specifico gruppo di persone, come, ad esempio, il gruppo di supporto tecnico di una organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>RgsWcfMtlsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico di (Windows Communication Foundation) WCF (mutual TLS) MTLS utilizzato da applicazione Response Group.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero totale di porte allocate per l'invio e la ricezione di traffico video. Il numero di porte effettive da aprire inizia con il valore configurato per VideoPortStart e continua con il numero di porte specificato per VideoPortCount. Ad esempio, se VideoPortStart è impostato su 60000 e VideoPortCount è impostato su 100, per il traffico video verranno utilizzate le porte da 60000 a 60099.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La prima di una serie di porte allocate per l'invio e la ricezione di traffico video. Ad esempio, –VideoPortStart 60000.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Set-CsApplicationServer** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsApplicationServer** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayApplicationServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsServerApplication](get-csserverapplication.md)

