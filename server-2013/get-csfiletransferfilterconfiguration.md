---
title: Get-CsFileTransferFilterConfiguration
TOCTitle: Get-CsFileTransferFilterConfiguration
ms:assetid: 6f43c203-acd6-4dbf-a071-752bf0c1727c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398527(v=OCS.15)
ms:contentKeyID: 49300927
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsFileTransferFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le configurazioni di filtro per il trasferimento di file dell'organizzazione. Queste configurazioni sono utilizzate per impedire a un utente di trasferire determinati tipi di file (ad esempio i file con estensione vbs o ps1) utilizzando un client Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsFileTransferFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsFileTransferFilterConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 restituisce una raccolta di tutte le configurazioni di filtro per il trasferimento dei file configurate per l'utilizzo nella propria organizzazione. Questo è il comportamento predefinito ogni volta che si chiama il cmdlet **Get-CsFileTransferFilterConfiguration** senza parametri aggiuntivi.

    Get-CsFileTransferFilterConfiguration

## ESEMPIO 2

Nell'esempio 2 viene restituita una singola raccolta di configurazioni di filtro per il trasferimento dei file: la configurazione con identità (Identity) site:Redmond. Poiché le identità devono essere univoche, il comando non restituirà mai più di una configurazione.

    Get-CsFileTransferFilterConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per ottenere una raccolta di tutte le configurazioni del filtro per il trasferimento dei file a livello di sito. Il valore di filtro "site:\*" indica al cmdlet **Get-CsFileTransferFilterConfiguration** di restituire solo le configurazioni in cui l'identità (Identity) inizia con la stringa "site:".

    Get-CsFileTransferFilterConfiguration -Filter site:*

## ESEMPIO 4

Il comando riportato nell'esempio 4 restituisce solo le configurazioni di filtro per il trasferimento dei file che includono .xls nell'elenco delle estensioni proibite. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsFileTransferFilterConfiguration** per ottenere una raccolta di tutte le configurazioni in uso nell'organizzazione. Quella raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro per restituire solo i dati relativi alle configurazioni nelle quali la proprietà Extensions include (-contains) il valore di stringa ".xls".

    Get-CsFileTransferFilterConfiguration | Where-Object {$_.Extensions -contains ".xls"}

## ESEMPIO 5

Nell'esempio 5 vengono restituite tutte le configurazioni di filtro per il trasferimento di file attualmente disabilitate. A tale scopo, viene utilizzato il cmdlet **Get-CsFileTransferFilterConfiguration** per restituire una raccolta di tutte le configurazioni in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente le configurazioni in cui la proprietà Enabled equivale a (-eq) False ($False).

    Get-CsFileTransferFilterConfiguration | Where-Object {$_.Enabled -eq $False}

## ESEMPIO 6

L'Esempio 6 mostra un elenco completo delle estensioni dei file proibite dalle configurazioni di filtro per il trasferimento dei file globali. Il comando utilizza il cmdlet **Get-CsFileTransferFilterConfiguration** specificando le raccolte di impostazioni Global. Questi dati vengono quindi inviati tramite pipe al cmdlet **Select-Object** che utilizza il parametro ExpandProperty per "espandere" il valore della proprietà Extensions. Viene così prodotto un elenco completo delle estensioni dei file visualizzato sullo schermo, una riga per estensione.

    Get-CsFileTransferFilterConfiguration -Identity Global | Select-Object -ExpandProperty Extensions

## Descrizione dettagliata

Quando inviano messaggi istantanei, gli utenti possono allegare e inviare file ad altri partecipanti alla conversazione. È possibile configurare Lync Server in modo che non sia consentito l'invio di file con determinate estensioni (generalmente quelle associati a tipi di file potenzialmente dannosi) utilizzando un client Lync.

Il cmdlet **Get-CsFileTransferFilterConfiguration** consente di recuperare le impostazioni per una particolare raccolta di impostazioni (queste impostazioni possono essere configurate nell'ambito globale o del sito). Le configurazioni di filtro per il trasferimento dei file includono l'elenco delle estensioni dei file per i quali è bloccato il trasferimento, a quale grado di filtro è abilitato (sono bloccati tutti i trasferimenti di file o solo quei file con le estensioni specificate) e se il filtro per il trasferimento dei file è attivo.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsFileTransferFilterConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsFileTransferFilterConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare le configurazioni di filtro per il trasferimento dei file da ottenere. Ad esempio, per restituire tutte le configurazioni di filtro per il trasferimento dei file nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per impostazione predefinita, le configurazioni di trasferimento dei file con una identità (la sola proprietà che si possa filtrare) che inizia con il valore di stringa &quot;site:&quot; sono impostazioni configurate nell'ambito del sito.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la configurazione per il trasferimento dei file che si vuole recuperare. Per ottenere le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per ottenere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità. Se si desidera utilizzare i caratteri jolly, utilizzare invece il parametro Filter.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare le configurazioni di filtro per il trasferimento dei file dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsFileTransferFilterConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsFileTransferFilterConfiguration](new-csfiletransferfilterconfiguration.md)  
[Remove-CsFileTransferFilterConfiguration](remove-csfiletransferfilterconfiguration.md)  
[Set-CsFileTransferFilterConfiguration](set-csfiletransferfilterconfiguration.md)

