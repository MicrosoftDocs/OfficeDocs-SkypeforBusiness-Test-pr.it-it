---
title: Set-CsDiagnosticHeaderConfiguration
TOCTitle: Set-CsDiagnosticHeaderConfiguration
ms:assetid: e9243b84-63c7-4ee1-8568-6b4417e10b0c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399045(v=OCS.15)
ms:contentKeyID: 49302320
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDiagnosticHeaderConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione delle intestazioni di diagnostica attualmente in uso nell'organizzazione. Tali impostazioni determinano se i messaggi SIP sono corredati da informazioni di intestazione, che possono essere utili per la risoluzione dei problemi e la segnalazione degli errori. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDiagnosticHeaderConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDiagnosticHeaderConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-SendToExternalNetworks <$true | $false>] [-SendToOutsideUnauthenticatedUsers <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono modificate le impostazioni di configurazione delle intestazioni di diagnostica con Identity site:Redmond. In questo esempio il valore della proprietà SendToOutsideUnauthenticatedUsers è impostato su True.

    Set-CsDiagnosticHeaderConfiguration -Identity site:Redmond -SendToOutsideUnauthenticatedUsers $True

## ESEMPIO 2

Il comando mostrato nell'esempio 2 è una variante del comando utilizzato nell'esempio 1. In questo caso, la proprietà SendToOutsideUnauthenticatedUsers viene tuttavia modificata per tutte le impostazioni di configurazione delle intestazioni di diagnostica in uso. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsDiagnosticHeaderConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni delle intestazioni di diagnostica in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsDiagnosticHeaderConfiguration**, che imposta su True la proprietà SendToOutsideUnauthenticatedUsers di ogni elemento nella raccolta.

    Get-CsDiagnosticHeaderConfiguration | Set-CsDiagnosticHeaderConfiguration -SendToOutsideUnauthenticatedUsers $True

## ESEMPIO 3

Nell'esempio 3 la proprietà SendToOutsideUnauthenticatedUsers viene di nuovo modificata, ma in questo caso soltanto per le impostazioni delle intestazioni di diagnostica in cui la proprietà SendToExternalNetworks è True. Per ottenere tale risultato, il comando utilizza innanzitutto il cmdlet **Get-CsDiagnosticHeaderConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione delle intestazioni di diagnostica attualmente in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona soltanto le impostazioni in cui la proprietà SendToExternalNetworks è uguale a True. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsDiagnosticHeaderConfiguration**, che imposta su True il valore della proprietà SendToOutsideUnauthenticatedUsers per ogni elemento nella raccolta.

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True} | Set-CsDiagnosticHeaderConfiguration -SendToOutsideUnauthenticatedUsers $True

## Descrizione dettagliata

Gli amministratori hanno la possibilità di allegare un'intestazione ms-diagnostic a ogni messaggio SIP inviato nell'organizzazione. Nel messaggio (non visibile per gli utenti finali) sono contenute informazioni che potrebbero essere utili nella risoluzione dei problemi di connessione o nella segnalazione di errori. Ad esempio, nell'intestazione di diagnostica potrebbe essere contenuti codici di errore che consentono all'applicazione client, come Lync Server, di eseguire azioni predeterminate nel caso in cui si verifichi una situazione specifica.

Pochi sono i motivi per non includere le intestazioni di diagnostica per i messaggi SIP inviati entro la rete interna: hanno infatti un impatto minimo sulle dimensioni del messaggio e possono essere uno strumento davvero utile per gli amministratori che devono risolvere i problemi di connessione. Le intestazioni di diagnostica tuttavia contengono anche informazioni, quali i nomi di dominio completi (FQDN) dei server SIP, che si potrebbe non voler rendere disponibili per le persone al di fuori della rete interna. Per questo motivo, le impostazioni di configurazione delle intestazioni di diagnostica consentono di decidere se inviare tali intestazioni agli utenti di reti esterne (quali utenti in un dominio federato) e/o a utenti esterni, ovvero utenti che si sono connessi dall'esterno della rete interna e che non sono stati ancora autenticati.

Per impostazione predefinita, le intestazioni non sono incluse in messaggi inviati a rete esterne o a utenti non autenticati. È tuttavia possibile modificare le impostazioni globali delle intestazioni di diagnostica in modo da includere le intestazioni per reti esterne e/o utenti non autenticati. In alternativa, è possibile creare impostazioni personalizzate nell'ambito del sito o nell'ambito del servizio (per il server perimetrale o il servizio di registrazione). In questo modo è possibile scegliere di includere intestazioni di diagnostica nei messaggi inviati da un sito oppure tramite un server perimetrale, non consentendo invece le intestazioni nei messaggi inviati da altri siti o tramite altri server perimetrali.

Il cmdlet **Set-CsDiagnosticHeaderConfiguration** consente di modificare una raccolta esistente di impostazioni di configurazione delle intestazioni di diagnostica. È possibile utilizzare il cmdlet per abilitare o disabilitare la trasmissione delle intestazioni di diagnostica a reti esterne e/o a utenti esterni.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsDiagnosticHeaderConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDiagnosticHeaderConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per le impostazioni di configurazione delle intestazioni di diagnostica da modificare. Per modificare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per modificare le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;. Per modificare le impostazioni globali, utilizzare la sintassi seguente: -Identity global.</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Set-CsDiagnosticHeaderConfiguration</strong> modifica automaticamente le impostazioni globali.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DiagnosticHeaderSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>SendToExternalNetworks</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True, le intestazioni di diagnostica verranno allegate ai messaggi inviati agli utenti su reti esterne, ad esempio agli utenti in un dominio federato. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>SendToOutsideUnauthenticatedUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True, le intestazioni di diagnostica verranno allegate ai messaggi inviati agli utenti esterni, ovvero utenti che si sono connessi dall'esterno della rete interna, ad esempio tramite un server proxy, e che non sono stati ancora autenticati.</p>
<p>Il valore predefinito è False.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings. Il cmdlet **Set-CsDiagnosticHeaderConfiguration** accetta istanze da pipeline dell'oggetto impostazioni delle intestazioni di diagnostica.

## Tipi restituiti

Il cmdlet **Set-CsDiagnosticHeaderConfiguration** non restituisce oggetti o valori. Il cmdlet consente invece di modificare le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsDiagnosticHeaderConfiguration](get-csdiagnosticheaderconfiguration.md)  
[New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)  
[Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)

