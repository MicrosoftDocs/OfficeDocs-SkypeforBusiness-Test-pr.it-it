---
title: Get-CsAVEdgeConfiguration
TOCTitle: Get-CsAVEdgeConfiguration
ms:assetid: f1a0db80-158c-47bd-8a8e-30e3f095fb2a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413008(v=OCS.15)
ms:contentKeyID: 49302429
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAVEdgeConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni di configurazione per i computer in cui è in esecuzione il servizio A/V Edge nell'organizzazione. Le impostazioni di configurazione disponibili in tali computer, noti anche come A/V Edge Server, consentono agli utenti interni di condividere dati audio e video con utenti esterni (ovvero con utenti che non hanno effettuato l'accesso alla rete interna), nonché di scambiare file e partecipare a sessioni di condivisione desktop. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAVEdgeConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAVEdgeConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce una raccolta di tutte le impostazioni di configurazione di A/V Edge configurate per l'utilizzo nell'organizzazione. La chiamata al cmdlet **Get-CsAVEdgeConfiguration** senza ulteriori parametri restituisce sempre una raccolta completa di impostazioni di configurazione A/V Edge.

    Get-CsAVEdgeConfiguration

## ESEMPIO 2

Nell'esempio 2 viene restituita una singola raccolta di impostazioni di configurazione di A/V Edge: la raccolta con Identity site:Redmond.

    Get-CsAVEdgeConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene restituita una raccolta di tutte le impostazioni di configurazione di A/V Edge configurate nell'ambito del sito. A tale scopo, viene chiamato il cmdlet **Get-CsAVEdgeConfiguration** con il parametro Filter. Il valore di filtro "site:\*" limita i dati restituiti alle impostazioni con valore Identity che inizia con i caratteri "site:". Per definizione, i dati restituiti vengono così limitati alle impostazioni configurate nell'ambito del sito.

    Get-CsAVEdgeConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 le uniche impostazioni di configurazione A/V Edge restituite sono quelle in cui la proprietà MaxBandwidthPerUserKB è maggiore di 10.000 kilobit al secondo. Per eseguire questa attività, nel comando viene innanzitutto chiamato il cmdlet **Get-CsAVEdgeConfiguration** senza alcun parametro. In questo modo, viene restituita una raccolta di tutte le impostazioni di configurazione A/V Edge attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà MaxBandwidthPerUserKB è maggiore di 10000 kilobit al secondo.

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxBandwidthPerUserKB -gt 10000}

## ESEMPIO 5

L'esempio 5 è analogo al comando mostrato nell'esempio 4. Nell'esempio 5 tuttavia le uniche impostazioni A/V Edge restituite sono quelle in cui la proprietà MaxBandwidthPerUserKB è esattamente uguale a 10000 kilobit al secondo.

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxBandwidthPerUserKB -eq 10000}

## ESEMPIO 6

Il comando mostrato nell'esempio 6 restituisce solo le impostazioni di configurazione A/V Edge in cui la proprietà MaxTokenLifetime è minore di 8 ore (08 ore : 00 minuti : 00 secondi). A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsAVEdgeConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione A/V Edge utilizzate nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui MaxTokenLifetime è minore di 8 ore (08:00:00).

    Get-CsAVEdgeConfiguration | Where-Object {$_.MaxTokenLifetime -lt "08:00:00"}

## Descrizione dettagliata

Un computer A/V Edge Server consente di scambiare traffico audio e video attraverso il firewall aziendale. In questo modo gli utenti possono, tra l'altro, utilizzare Lync Server su Internet e quindi scambiare dati audio e video con utenti che hanno effettuato l'accesso al sistema all'interno del firewall. Le impostazioni di configurazione di server perimetrale possono essere assegnate nell'ambito globale, del sito e del servizio. Le impostazioni di configurazione A/V Edge consentono agli amministratori di effettuare operazioni quali gestire la durata del periodo di validità dell'autenticazione utente prima del rinnovo e limitare la larghezza di banda utilizzabile da un singolo utente o da una singola porta.

Il cmdlet **Get-CsAVEdgeConfiguration** consente di recuperare informazioni sulle impostazioni di configurazione A/V Edge attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsAVEdgeConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAVEdgeConfiguration"}

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
<td><p>Consente l'utilizzo di caratteri jolly quando si specificano le impostazioni di configurazione A/V Edge da restituire. Ad esempio, per restituire tutte le impostazioni configurate nell'ambito del sito, utilizzare la seguente sintassi: -Filter site:*. Per restituire una raccolta di tutte le impostazioni configurate nell'ambito del servizio, utilizzare la seguente sintassi: -Filter &quot;service:*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la raccolta delle impostazioni di configurazione di A/V Edge da recuperare. Per recuperare la raccolta globale, la sintassi utilizzata è la seguente: -Identity global. Per recuperare una raccolta di siti, utilizzare una sintassi analoga alla seguente: -Identity site:Redmond. Le impostazioni configurate nell'ambito del servizio possono essere referenziate con una sintassi simile alla seguente: -Identity service:EdgeServer:atl-cs-001.litwareinc.com. Non è possibile utilizzare i caratteri jolly per specificare l'identità di un criterio.</p>
<p>Se il parametro non è incluso, il cmdlet <strong>Get-CsAVEdgeConfiguration</strong> restituirà una raccolta di tutte le impostazioni di configurazione Edge attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione A/V Edge dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsAVEdgeConfiguration** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsAVEdgeConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.MediaRelaySettings.

## Vedere anche

#### Ulteriori risorse

[New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)  
[Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)  
[Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

