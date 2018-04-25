---
title: Set-CsConferenceServer
TOCTitle: Set-CsConferenceServer
ms:assetid: 90f9f1f1-0029-4f97-a8f4-719523cfad56
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398738(v=OCS.15)
ms:contentKeyID: 49301325
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le proprietà di un A/V Conferencing Server, noto anche come server per conferenze. Il server per conferenze fornisce le funzionalità audio e video (A/V) per le conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsConferenceServer [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AppSharingSipPort <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-AudioVideoSipPort <UInt16>] [-Confirm [<SwitchParameter>]] [-DataPsomPort <UInt16>] [-EdgeServer <String>] [-Force <SwitchParameter>] [-ImSipPort <UInt16>] [-MeetingPsomPort <UInt16>] [-PhoneSipPort <UInt16>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di modificare la porta SIP di messaggistica istantanea per il componente Conference Server ConferencingServer:atl-cs-001.litwareinc.com. In questo esempio la porta viene impostata su 5075.

    Set-CsConferenceServer -Identity "ConferencingServer:atl-cs-001.litwareinc.com" -ImSipPort 5075

## ESEMPIO 2

L'esempio 2 è una variante del comando illustrato nell'esempio 1. In questo caso però la porta SIP di messaggistica istantanea viene cambiata per tutti i componenti Conference Server dell'organizzazione. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsService** e il parametro ConferencingServer per restituire una raccolta di tutti i server per conferenze attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che esegue il cmdlet **Set-CsConferenceServer** per ogni server della raccolta, impostando ImSipPort su 5075.

    Get-CsService -ConferencingServer | ForEach-Object {Set-CsConferenceServer -Identity $_.Identity -ImSipPort 5075}

## Descrizione dettagliata

I server per conferenze (noti anche come A/V Conferencing Server) vengono utilizzati per fornire funzionalità audio e video alle conferenze. A sua volta, il cmdlet **Set-CsConferenceServer** consente di modificare le proprietà di questi server. In particolare, è possibile specificare quali porte utilizzare per il traffico audio, il traffico video e la condivisione di applicazioni. È inoltre possibile utilizzare il cmdlet **Set-CsConferenceServer** per associare un dato server a un particolare server perimetrale o server di archiviazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsConferenceServer** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceServer"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero totale di porte allocate per la condivisione delle applicazioni. Le porte effettive da aprire iniziano dalla porta con il valore configurato per AppSharingPortStart e proseguono per il numero di porte specificato in AppSharingPortCount. Ad esempio, se AppSharingPortStart è impostato su 60000 e AppSharingPortCount è impostato su 100, per la condivisione delle applicazioni saranno utilizzate le porte da 60000 a 60099.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Prima porta nell'intervallo di porte allocate per la condivisione delle applicazioni. Ad esempio: -AppSharingPortStart 60000.</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata per ascoltare le richieste per la condivisione di applicazioni. Le porte effettivamente utilizzate per la condivisione di applicazioni sono configurate utilizzando AppSharingPortStart e AppSharingPortCount.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero totale di porte allocate per l'invio e la ricezione del traffico audio. Le porte effettive da aprire iniziano dalla porta con il valore configurato per AudioPortStart e proseguono per il numero di porte specificato in AudioPortCount. Ad esempio, se AudioPortStart è impostato su 60000 e AudioPortCount è impostato su 100, per il traffico audio saranno utilizzate le porte da 60000 a 60099.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Prima porta nell'intervallo di porte allocate per l'invio e la ricezione del traffico audio. Ad esempio: –AudioPortStart 60000.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioVideoSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta SIP utilizzata per ascoltare le richieste in arrivo per il servizio audio e video. Le porte effettivamente utilizzate per il traffico audio e video sono configurate utilizzando AudioPortCount, AudioPortStart, VideoPortCount e VideoPortStart.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DataPsomPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta dati utilizzata dal protocollo PSOM (Persistent Shared Object Model).</p></td>
</tr>
<tr class="odd">
<td><p><em>EdgeServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso di servizio del server perimetrale da associare al server per conferenze. Ad esempio: -EdgeServer &quot;EdgeServer:atl-edge-001.litwareinc.com&quot;.</p></td>
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
<td><p>Posizione del servizio del componente Conference Server da modificare. Ad esempio: -Identity &quot;ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>È possibile tralasciare il prefisso &quot;ConferencingServer:&quot; quando si specifica un server per conferenze. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ImSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico di messaggistica istantanea.</p></td>
</tr>
<tr class="odd">
<td><p><em>MeetingPsomPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il protocollo PSOM (Persistent Shared Object Model), un protocollo di Microsoft utilizzato per le conferenze.</p></td>
</tr>
<tr class="even">
<td><p><em>PhoneSipPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta utilizzata per il traffico di telefonia.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero totale di porte allocate per l'invio e la ricezione del traffico video. Le porte effettive da aprire iniziano dalla porta con il valore configurato per VideoPortStart e proseguono per il numero di porte specificato in VideoPortCount. Ad esempio, se VideoPortStart è impostato su 60000 e VideoPortCount è impostato su 100, per il traffico video saranno utilizzate le porte da 60000 a 60099.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Prima porta nell'intervallo di porte allocato per l'invio e la ricezione del traffico video. Ad esempio: –VideoPortStart 60000.</p></td>
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

Nessuno. Il cmdlet **Set-CsConferenceServer** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsConferenceServer** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayConferenceServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[Get-CsService](get-csservice.md)

