---
title: Remove-CsHealthMonitoringConfiguration
TOCTitle: Remove-CsHealthMonitoringConfiguration
ms:assetid: 2e401908-2366-4e67-ba5b-68ba7ece166e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425794(v=OCS.15)
ms:contentKeyID: 49300059
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsHealthMonitoringConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione del monitoraggio dello stato. Queste impostazioni consentono agli amministratori di eseguire test di controllo della qualità senza dover fornire nome utente e password per gli account di test necessari. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsHealthMonitoringConfiguration -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eliminare una raccolta di impostazioni di configurazione per il monitoraggio dello stato con l'identità atl-cs-001.litwareinc.com. Poiché le identità devono essere univoche, il comando eliminerà al massimo una raccolta di impostazioni.

    Remove-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le impostazioni di configurazione del monitoraggio dello stato attualmente in uso. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsHealthMonitoringConfiguration** senza alcun parametro. Viene così restituita una raccolta di tutte le impostazioni di configurazione del monitoraggio dello stato definite nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsHealthMonitoringConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsHealthMonitoringConfiguration | Remove-CsHealthMonitoringConfiguration 

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione del monitoraggio dello stato create per il dominio litwareinc.com. A tale scopo, viene chiamato il cmdlet **Get-CsHealthMonitoringConfiguration** con il parametro Filter. Il valore di filtro "\*.litwareinc.com" assicura che vengano restituite solo le impostazioni la cui identità termina con il valore stringa ".litwareinc.com". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsHealthMonitoringConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsHealthMonitoringConfiguration -Filter *.litwareinc.com  | Remove-CsHealthMonitoringConfiguration 

## ESEMPIO 4

Il comando riportato nell'esempio 4 elimina tutte le impostazioni di configurazione del monitoraggio dello stato che includono l'utente con indirizzo SIP sip:kenmyer@litwareinc.com come uno degli utenti di test. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsHealthMonitoringConfiguration** senza alcun parametro. Viene così restituita una raccolta di tutte le impostazioni di configurazione del monitoraggio dello stato attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà FirstTestUserSipUri è uguale a "sip:kenmyer@litwareinc.com" o la proprietà SecondTestUserSipUri è uguale a "sip:kenmyer@litwareinc.com". A loro volta queste impostazioni vengono inviate tramite pipe al cmdlet **Remove-CsHealthMonitoringConfiguration**, che le rimuove.

    (Get-CsHealthMonitoringConfiguration | Where-Object {$_.FirstTestUserSipUri -eq "sip:kenmyer@litwareinc.com" -or $_.SecondTestUserSipUri -eq " sip:kenmyer@litwareinc.com"}) | Remove-CsHealthMonitoringConfiguration

## Descrizione dettagliata

Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di completare correttamente normali attività, ad esempio l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono in una rete PSTN (Public Switched Telephone Network). Questi test possono essere eseguiti manualmente da un amministratore oppure automaticamente da un'applicazione, ad esempio Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Per eseguire le transazioni sintetiche è possibile procedere in due modi. Alcuni amministratori utilizzano i cmdlet **CsHealthMonitoringConfiguration** per configurare account di test per ciascun pool di registrazione. Si tratta di una coppia di account utente appositamente preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test che non appartengono a utenti reali. Dopo aver configurato gli account di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su quel pool senza dover specificare le identità o fornire le credenziali degli account utente coinvolti nel test. Infatti, al momento di eseguire i controlli, la transazione sintetica utilizzerà automaticamente gli account di test predefiniti.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando degli account utente reali. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (piuttosto che degli account utente di test). Se si decide di eseguire una transazione sintetica utilizzando degli account utente reali, sarà necessario fornire le credenziali di tutti gli utenti coinvolti.

Il cmdlet **Remove-CsHealthMonitoringConfiguration** consente di rimuovere qualsiasi impostazione di configurazione per il monitoraggio dello stato di integrità configurata per l'utilizzo nell'organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsHealthMonitoringConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsHealthMonitoringConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome completo di dominio (FQDN) del pool che ospita le impostazioni di configurazione per il monitoraggio dello stato di integrità da eliminare. Ad esempio: -Identity atl-cs-001.litwareinc.com.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings. Il cmdlet **Remove-CsHealthMonitoringConfiguration** accetta le istanze dell'oggetto configurazione del monitoraggio dello stato inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsHealthMonitoringConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)

