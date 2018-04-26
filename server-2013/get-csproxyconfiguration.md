---
title: Get-CsProxyConfiguration
TOCTitle: Get-CsProxyConfiguration
ms:assetid: e4836619-026f-4df0-adbd-aa5216e36368
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399011(v=OCS.15)
ms:contentKeyID: 49302266
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsProxyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione dei server proxy attualmente in uso nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsProxyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsProxyConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituita una raccolta di tutte le impostazioni di configurazione del proxy attualmente in uso nell'organizzazione. A tale scopo, il cmdlet **Get-CsProxyConfiguration** viene richiamato senza alcun parametro.

    Get-CsProxyConfiguration

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni sulle impostazioni di configurazione del proxy con valore Identity service:EdgeServer:atl-cs-001.litwareinc.com. Poiché le identità devono essere univoche, il comando non restituirà mai più di una raccolta di impostazioni.

    Get-CsProxyConfiguration -Identity "service:EdgeServer:atl-cs-001.litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 vengono restituite le informazioni relative a tutte le impostazioni del proxy che sono state configurate nell'ambito del servizio. A tale scopo, il comando chiama il cmdlet **Get-CsProxyConfiguration** con il parametro Filter. Il valore di filtro "service:\*" garantisce che vengano restituite solo le impostazioni il cui valore Identity inizia con il valore stringa "service:\*".

    Get-CsProxyConfiguration -Filter "service:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite le informazioni relative alle impostazioni di configurazione del proxy che non consentono l'utilizzo dei certificati dei client come meccanismo di autenticazione. Per eseguire questa attività, viene innanzitutto utilizzato il cmdlet**Get-CsProxyConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione del proxy attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà UseCertificateForClientToProxyAuth è uguale a False.

    Get-CsProxyConfiguration | Where-Object {$_.UseCertificateForClientToProxyAuth -eq $False}

## ESEMPIO 5

Nell'esempio 5 vengono restituite tutte le impostazioni di configurazione del proxy in cui le dimensioni massime del corpo per un messaggio del client sono inferiori a 5.000 KB. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsProxyConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione del proxy attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona le impostazioni in cui la proprietà MaxClientMessageBodySizeKb è minore di 5.000 KB.

    Get-CsProxyConfiguration | Where-Object {$_.MaxClientMessageBodySizeKb -lt 5000}

## Descrizione dettagliata

Lync Server consente di gestire i server proxy in uso tramite le impostazioni di configurazione del server proxy. Tali impostazioni, che possono essere applicate sia nell'ambito globale che nell'ambito del servizio (anche se soltanto per i servizi di registrazione e server perimetrale), consentono di controllare aspetti quali i protocolli di autenticazione utilizzabili dagli endpoint client e se verrà utilizzata o meno la compressione per le connessioni del server proxy in ingresso e in uscita. Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni di configurazione del server proxy. Come fatto notare, è inoltre possibile creare raccolte ulteriori nell'ambito del servizio.

Il cmdlet **Get-CsProxyConfiguration** consente di restituire informazioni relative a qualsiasi impostazione di configurazione del server proxy attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsProxyConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsProxyConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare le impostazioni di configurazione del proxy in questione. Ad esempio, con questa sintassi vengono restituite tutte le impostazioni configurate nell'ambito del servizio: -Filter &quot;service:*&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>l'identificatore univoco per le impostazioni di configurazione del server proxy da restituire. Per restituire le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per restituire le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity. Tuttavia, se si desidera (o è necessario) utilizzare caratteri jolly, utilizzare il parametro Filter.</p>
<p>Se tale parametro non è incluso, il cmdlet <strong>Get-CsProxyConfiguration</strong> restituirà tutte le impostazioni del server proxy attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione del proxy dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsProxyConfiguration** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsProxyConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.ProxySettings.

## Vedere anche

#### Ulteriori risorse

[New-CsProxyConfiguration](new-csproxyconfiguration.md)  
[Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)  
[Set-CsProxyConfiguration](set-csproxyconfiguration.md)

