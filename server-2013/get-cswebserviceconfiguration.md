---
title: Get-CsWebServiceConfiguration
TOCTitle: Get-CsWebServiceConfiguration
ms:assetid: 28582668-839c-4b04-8211-928c91634672
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425751(v=OCS.15)
ms:contentKeyID: 49299992
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsWebServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su tutte le impostazioni di configurazione dei servizi Web in uso nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsWebServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsWebServiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutte le impostazioni di configurazione dei servizi Web attualmente in uso nell'organizzazione.

    Get-CsWebServiceConfiguration

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce informazioni sulle impostazioni di configurazione dei servizi Web con valore Identity site:Redmond.

    Get-CsWebServiceConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 vengono restituite tutte le impostazioni di configurazione dei servizi Web assegnate nell'ambito del sito. A tale scopo, quando si chiama il cmdlet **Get-CsWebServiceConfiguration**, viene incluso il parametro Filter. Il valore di filtro "site:\*" assicura che vengano restituite solo le impostazioni la cui identità inizia con il valore stringa "site:".

    Get-CsWebServiceConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 il comando restituisce tutte le impostazioni di configurazione dei servizi Web che non consentono l'autenticazione tramite PIN (Personal Identification Number). A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsWebServiceConfiguration** per restituire tutte le impostazioni di configurazione dei servizi Web attualmente in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente le impostazioni con proprietà UsePinAuth uguale a False.

    Get-CsWebServiceConfiguration | Where-Object {$_.UsePinAuth -eq $False}

## ESEMPIO 5

Nell'esempio 5 vengono restituite tutte le impostazioni di configurazione dei servizi Web in cui la dimensione massima di espansione gruppo è maggiore di 100. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsWebServiceConfiguration** per restituire tutte le impostazioni di configurazione dei servizi Web attualmente in uso. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che seleziona unicamente le impostazioni con proprietà MaxGroupSizeToExpand maggiore di 100.

    Get-CsWebServiceConfiguration | Where-Object {$_.MaxGroupSizeToExpand -gt 100}

## Descrizione dettagliata

Molti componenti di Lync Server sono basati su Web: questi componenti utilizzano i servizi Web o le pagine Web per eseguire le attività. Gli utenti utilizzano ad esempio un servizio Web quando cercano nuovi contatti nella Rubrica o quando utilizzano l'espansione gruppo per visualizzare i singoli membri di un gruppo di distribuzione. Analogamente, componenti come le conferenze telefoniche con accesso esterno e il Pannello di controllo di Lync Server utilizzano le pagine Web come interfaccia tra Lync Server e gli utenti.

I cmdlet **CsWebServiceConfiguration** consentono agli amministratori di gestire le impostazioni di configurazione dei servizi Web nell'organizzazione, ad esempio la gestione dell'espansione dei gruppi, delle impostazioni dei certificati e dei metodi di autenticazione consentiti. Poiché nell'ambito globale, del sito e del servizio è possibile configurare impostazioni diverse, anche se solo per il servizio Servizi Web, le funzionalità dei servizi Web possono essere personalizzate per utenti e postazioni differenti.

Il cmdlet **Get-CsWebServiceConfiguration** consente di restituire informazioni dettagliate sulle impostazioni di configurazione dei servizi Web attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsWebServiceConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsWebServiceConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare la raccolta o le raccolte di impostazioni di configurazione dei servizi Web da restituire. Ad esempio, la sintassi che segue restituisce tutte le informazioni configurate nell'ambito del sito: -Filter &quot;site:*&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione dei servizi Web da restituire. Per restituire le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per restituire le impostazioni configurate nell'ambito del sito, utilizzare la sintassi: -Identity &quot;site:Redmond.&quot; ﻿Per recuperare le impostazioni dell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando. Se non si specifica né l'uno né l'altro parametro, il cmdlet <strong>Get-CsWebServiceConfiguration</strong> restituirà tutte le raccolte delle impostazioni dei servizi Web attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione dei servizi Web dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsWebServiceConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsWebServiceConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Web.WebServiceSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

