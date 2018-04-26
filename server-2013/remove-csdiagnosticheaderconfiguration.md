---
title: Remove-CsDiagnosticHeaderConfiguration
TOCTitle: Remove-CsDiagnosticHeaderConfiguration
ms:assetid: d71b79f1-49f2-4a6c-8b3e-ca909e8d5f49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398941(v=OCS.15)
ms:contentKeyID: 49302118
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDiagnosticHeaderConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più raccolte di impostazioni di configurazione delle intestazioni di diagnostica attualmente in uso nell'organizzazione. Tali impostazioni determinano se i messaggi SIP sono corredati da informazioni di intestazione, che possono essere utili per la risoluzione dei problemi e la segnalazione degli errori. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDiagnosticHeaderConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono rimosse le impostazioni di configurazione dell'intestazione diagnostica con il parametro Identity site:Redmond.

    Remove-CsDiagnosticHeaderConfiguration -Identity site:Redmond

## ESEMPIO 2

Il comando mostrato nell'esempio 2 elimina tutte le impostazioni di configurazione dell'intestazione diagnostica applicate in ambito servizio. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDiagnosticHeaderConfiguration** con il parametro Filter. Il valore di filtro "service:\*" limita i dati restituiti alle impostazioni in cui il parametro Identity inizia con i caratteri "service:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsDiagnosticHeaderConfiguration** che elimina ogni elemento presente nella raccolta.

    Get-CsDiagnosticHeaderConfiguration -Filter service:* | Remove-CsDiagnosticHeaderConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione dell'intestazione di diagnostica che consentono l'invio alle reti esterne. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDiagnosticHeaderConfiguration** per restituire una raccolta di tutte le impostazioni delle intestazioni di diagnostica attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che seleziona solo le impostazioni in cui la proprietà SendToExternalNetworks è uguale a True. Queste impostazioni vengono quindi inviate tramite pipe al cmdlet **Remove-CsDiagnosticHeaderConfiguration** che elimina ogni impostazione che consente l'invio alle reti esterne.

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True} | Remove-CsDiagnosticHeaderConfiguration

## Descrizione dettagliata

Gli amministratori hanno la possibilità di allegare un'intestazione ms-diagnostic a ogni messaggio SIP inviato nell'organizzazione. Nel messaggio (non visibile per gli utenti finali) sono contenute informazioni che potrebbero essere utili nella risoluzione dei problemi di connessione o nella segnalazione di errori. Ad esempio, nell'intestazione di diagnostica potrebbero essere contenuti codici di errore che consentono all'applicazione client di eseguire azioni predeterminate nel caso in cui si verifichi una situazione specifica.

Pochi sono i motivi per non includere le intestazioni di diagnostica per i messaggi SIP inviati entro la rete interna: hanno infatti un impatto minimo sulle dimensioni del messaggio e possono essere uno strumento davvero utile per gli amministratori che devono risolvere i problemi di connessione. Le intestazioni di diagnostica tuttavia contengono anche informazioni, quali i nomi di dominio completi (FQDN) dei server SIP, che si potrebbe non voler rendere disponibili per le persone al di fuori della rete interna. Per questo motivo, le impostazioni di configurazione delle intestazioni di diagnostica consentono di decidere se inviare tali intestazioni agli utenti di reti esterne (quali utenti in un dominio federato) e/o a utenti esterni, ovvero utenti che si sono connessi dall'esterno della rete interna e che non sono stati ancora autenticati.

In alternativa, è possibile creare impostazioni personalizzate nell'ambito del sito o nell'ambito del servizio (per il server perimetrale o il servizio di registrazione). In questo modo è possibile scegliere di includere intestazioni di diagnostica nei messaggi inviati da un sito oppure tramite un server perimetrale, non consentendo invece le intestazioni nei messaggi inviati da altri siti o tramite altri server perimetrali.

Le nuove raccolte create nell'ambito del sito o nell'ambito del servizio possono essere successivamente rimosse utilizzando il cmdlet **Remove-CsDiagnosticHeaderConfiguration**. È possibile inoltre eseguire questo cmdlet sulla raccolta globale. In tal caso, però, la raccolta globale non verrà rimossa poiché non è possibile rimuovere la raccolta globale, ma verrà reimpostato il valore predefinito False per le due proprietà contenute nella raccolta globale, ovvero SendToExternalNetworks e SendToOutsideUnauthenticatedUsers.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsDiagnosticHeaderConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDiagnosticHeaderConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco per le impostazioni di configurazione delle intestazioni di diagnostica da rimuovere. Per rimuovere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;site:Redmond&quot;. Per rimuovere le impostazioni configurate in ambito servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:EdgeServer:atl-edge-001.litwareinc.com&quot;.</p>
<p>Il cmdlet <strong>Remove-CsDiagnosticHeaderConfiguration</strong> può anche essere eseguito per le impostazioni di configurazione globali. In questo caso, utilizzare la seguente sintassi: -Identity global. Si noti, tuttavia, che le impostazioni globali non verranno effettivamente rimosse, ma verranno ripristinati tutti i valori predefiniti delle relative proprietà.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings. Il cmdlet **Remove-CsDiagnosticHeaderConfiguration** accetta istanze da pipeline dell'oggetto impostazioni delle intestazioni di diagnostica.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsDiagnosticHeaderConfiguration** elimina piuttosto le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsDiagnosticHeaderConfiguration](get-csdiagnosticheaderconfiguration.md)  
[New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)  
[Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)

