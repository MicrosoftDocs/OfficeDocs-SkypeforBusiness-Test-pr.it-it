---
title: Get-CsCdrConfiguration
TOCTitle: Get-CsCdrConfiguration
ms:assetid: 4af8ffa2-63d3-4873-8dac-5afede090d4f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398298(v=OCS.15)
ms:contentKeyID: 49300465
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCdrConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni della registrazione dettagli chiamata (CDR). La registrazione dettagli chiamata (CDR) consente di tenere traccia delle sessioni di messaggistica istantanea peer-to-peer, delle chiamate VoIP e delle chiamate ai servizi di conferenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsCdrConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

In questo esempio viene utilizzato il cmdlet **Get-CsCdrConfiguration** per restituire una raccolta di tutte le impostazioni CDR configurate per l'utilizzo nell'organizzazione.

    Get-CsCdrConfiguration

## ESEMPIO 2

Nell'Esempio 2 viene utilizzato il parametro Identity per ottenere un'unica raccolta di impostazioni CDR: le impostazioni con Identity site:Redmond.

    Get-CsCdrConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'Esempio 3 viene utilizzato il parametro Filter per ottenere tutte le impostazioni CDR configurate nell'ambito del sito. Il valore del filtro "site:\*" restituisce tutte le impostazioni CDR la cui identità inizia con la stringa "site:". Per definizione, queste impostazioni sono state configurate nell'ambito del sito.

    Get-CsCdrConfiguration -Filter site:*

## ESEMPIO 4

Nell'esempio 4 viene restituita una raccolta di tutte le impostazioni CDR in cui la proprietà KeepCallDetailForDays è impostata su un valore inferiore a 30 giorni. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsCdrConfiguration** per restituire raccolta di tutte le impostazioni CDR configurate nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà KeepCallDetailForDays è impostata su un valore inferiore a 30 giorni.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30}

## Descrizione dettagliata

La registrazione dettagli chiamata consente di monitorare l'utilizzo di funzionalità di Lync Server come le telefonate VoIP, i messaggi istantanei, i trasferimenti di file, le conferenze audio/video e le sessioni di condivisione delle applicazioni. La registrazione CDR (disponibile solo se è stato distribuito il servizio di monitoraggio) conserva le informazioni sull'utilizzo e registra informazioni quali le parti coinvolte nella conversazione, la relativa durata, se si sono verificati o meno trasferimenti di file e così via. La registrazione dettagli chiamata non registra tuttavia la chiamata.

La registrazione dei dettagli della chiamata tiene traccia anche delle informazioni su eventuali errori verificatesi durante la chiamata: dati di diagnostica dettagliati per le sessioni peer-to-peer e per le chiamate ai servizi di conferenza.

La scelta se utilizzare o meno la funzionalità di registrazione dei dettagli della chiamata nell'organizzazione dipende dall'amministratore. Se è stato distribuito il servizio di monitoraggio, è possibile abilitare o disabilitare la funzionalità CDR. Inoltre, è possibile applicare questa scelta globalmente (nel qual caso, la funzionalità CDR verrà abilitata o disabilitata nell'intera organizzazione) o a livello di singolo sito (ad esempio, si potrebbe voler utilizzare la funzionalità CDR nel sito Redmond, ma non nel sito Paris).

Il cmdlet **Get-CsCdrConfiguration** consente di ottenere informazioni dettagliate sulla modalità di utilizzo della registrazione dei dettagli della chiamata nell'organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsCdrConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsCdrConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per ottenere una raccolta di impostazioni di configurazione CDR. Ad esempio, per ottenere una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la seguente sintassi: -Filter site:*. Per ottenere una raccolta di tutte le impostazioni in cui la stringa &quot;Western&quot; compare nell'identità, utilizzare la seguente sintassi: -Filter *Western*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco della raccolta di impostazioni di configurazione CDR che si desidera ottenere. Per ottenere le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per ottenere una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità. Se si desidera utilizzare i caratteri jolly, è necessario utilizzare il parametro Filter.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsCdrConfiguration</strong> restituirà una raccolta di tutte le impostazioni di configurazione CDR attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione CDR dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsCdrConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsCdrConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

