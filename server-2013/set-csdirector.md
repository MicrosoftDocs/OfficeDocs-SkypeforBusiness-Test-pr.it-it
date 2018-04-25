---
title: Set-CsDirector
TOCTitle: Set-CsDirector
ms:assetid: 74eb6f17-812f-47df-84ee-fa6e42990f2e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398565(v=OCS.15)
ms:contentKeyID: 49300993
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDirector

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le proprietà di uno o più Director. È possibile utilizzare i Director per autenticare le richieste degli utenti, ma non per ospitare gli account degli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDirector [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingServer <String>] [-Confirm [<SwitchParameter>]] [-EdgeServer <String>] [-Force <SwitchParameter>] [-MirrorMonitoringDatabase <String>] [-MonitoringDatabase <String>] [-MonitoringServer <String>] [-SipHealthPort <UInt16>] [-SipPort <UInt16>] [-SipServerTcpPort <UInt16>] [-WebPort <UInt16>] [-WebServer <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di modificare server di archiviazione associato con Server Director Director:atl-cs-001.litwareinc.com. In questo esempio, server di archiviazione viene modificato in ArchivingServer:dublin-cs-001.litwareinc.com.

    Set-CsDirector -Identity "Director:atl-cs-001.litwareinc.com" -ArchivingServer "ArchivingServer:dublin-cs-001.litwareinc.com"

## ESEMPIO 2

Nell'esempio 2 viene cambiata la porta SIP di tutti i server Director attualmente in uso nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsService** e il parametro Director per ottenere una raccolta di tutti i server Director dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. A sua volta, il cmdlet **ForEach-Object** esegue il cmdlet **Set-CsDirector** per ogni sito della raccolta, cambiando in 5072 il valore della proprietà SipPort.

    Get-CsService -Director | ForEach-Object {Set-CsDirector -Identity $_.Identity -SipPort 5072}

## Descrizione dettagliata

Server Director autentica gli utenti e risponde alle richieste degli utenti senza ospitare realmente gli account utente. In genere, i Director vengono utilizzati per organizzazioni che consentono l'accesso esterno alla rete attraverso gli Edge Server. In questo tipo di scenario, i Director contribuiscono non solo ad alleggerire la pressione esercitata sui server di front end gestendo le richieste di autenticazione, ma anche a proteggere la rete interna da attacchi di tipo denial-of-service e da altro traffico dannoso. I Director sono utili anche quando più server di front end vengono distribuiti in un sito centralizzato. In questo caso, i Director ricevono tutte le richieste degli utenti e quindi le incanalano al pool di server appropriato. Ancora una volta, ciò consente di alleggerire al pressione esercitata sui server di front end.

Il cmdlet **Set-CsDirector** consente di modificare i valori delle proprietà dei Director attualmente in uso nella propria organizzazione. Ciò include la modifica di elementi quali server di archiviazione o server perimetrale associati a Server Director o la modifica della porta utilizzata per inviare e ricevere il traffico SIP.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsDirector** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDirector"}

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
<td><p><em>ArchivingServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del server di archiviazione da associare con Server Director. Ad esempio: -ArchivingServer &quot;ArchivingServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del server perimetrale da associare con Server Director. Ad esempio: -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Percorso di installazione del Server Director da modificare. Ad esempio: -Identity &quot;Director:atl-cs-001.litwareinc.com&quot;.</p>
<p>Si noti che è possibile non utilizzare il prefisso &quot;Director&quot; quando si specifica un Director. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorMonitoringDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del database di monitoraggio mirror da associare al Server Director.</p></td>
</tr>
<tr class="odd">
<td><p><em>MonitoringDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio del database di monitoraggio da associare al Server Director.</p></td>
</tr>
<tr class="even">
<td><p><em>MonitoringServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del Monitoring Server da associare con Server Director. Ad esempio: -MonitoringServer &quot;MonitoringServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipHealthPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il monitoraggio dell'integrità del server.</p></td>
</tr>
<tr class="even">
<td><p><em>SipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La porta utilizzata per il traffico SIP (Session Initiation Protocol).</p></td>
</tr>
<tr class="odd">
<td><p><em>SipServerTcpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa SIP. Il valore predefinito è 5060.</p></td>
</tr>
<tr class="even">
<td><p><em>WebPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>La porta utilizzata per la comunicazione con servizi Web.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del server servizi Web da associare con Server Director. Ad esempio: -WebServer &quot;WebServer:atl-cs-001.litwareinc.com&quot;</p></td>
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

Nessuno. Il cmdlet **Set-CsDirector** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsDirector** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayDirector.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

