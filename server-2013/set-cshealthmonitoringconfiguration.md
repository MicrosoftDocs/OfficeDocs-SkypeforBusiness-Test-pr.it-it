---
title: Set-CsHealthMonitoringConfiguration
TOCTitle: Set-CsHealthMonitoringConfiguration
ms:assetid: 375af06c-70c8-4775-8c7b-3b3f8fd9afcc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425847(v=OCS.15)
ms:contentKeyID: 49300173
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsHealthMonitoringConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione del monitoraggio dello stato. Queste impostazioni consentono agli amministratori di eseguire test di controllo della qualità senza dover fornire nome utente e password per gli account di test necessari. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsHealthMonitoringConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsHealthMonitoringConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-FirstTestSamAccountName <String>] [-FirstTestUserSipUri <String>] [-Force <SwitchParameter>] [-SecondTestSamAccountName <String>] [-SecondTestUserSipUri <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene configurato il primo utente di test assegnato alle impostazioni di configurazione del monitoraggio dell'integrità per il pool atl-cs-001.litwareinc.com. Con questo esempio, l'indirizzo SIP del nuovo utente di test viene impostato su sip:kenmyer@litwareinc.com e il SamAccountName per l'utente di test viene impostato su kenmyer.

    Set-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -FirstTestSamAccountName "litwareinc\kenmyer"

## ESEMPIO 2

L'esempio 2 è una variante del comando riportato nell'esempio 1. In questo caso però lo stesso utente di test viene assegnato a ogni raccolta di impostazioni di configurazione del monitoraggio dello stato in uso nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsHealthMonitoringConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione del monitoraggio dello stato. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsHealthMonitoringConfiguration**, che assegna lo stesso indirizzo SIP e lo stesso valore SamAccountName del primo utente di test a ogni elemento incluso della raccolta.

    Get-CsHealthMonitoringConfiguration | Set-CsHealthMonitoringConfiguration -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -FirstTestSamAccountName "litwareinc\kenmyer"

## ESEMPIO 3

Con l'esempio 3 viene mostrato come eseguire una ricerca e sostituzione del primo utente di test assegnato a una raccolta di impostazioni di configurazione del monitoraggio dell'integrità; in questo esempio, l'utente con indirizzo SIP sip:pilar@litwareinc.com viene sostituito ogni volta che tale utente appare come primo utente di test in una raccolta.

A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsHealthMonitoringConfiguration** senza parametri aggiuntivi per restituire una raccolta di tutte le impostazioni di configurazione del monitoraggio dello stato attualmente in uso nell'organizzazione. Questa raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli elementi in cui la proprietà FirstTestUserSipUri è uguale a (-eq) sip:pilar@litwareinc.com. Tale raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Set-CsHealthMonitoringConfiguration**, che seleziona ogni elemento della raccolta e imposta il valore della proprietà FirstTestUserSipUri su sip:kenmyer@litwareinc.com e il valore della proprietà FirstTestSamAccountName su kenmyer.

    Get-CsHealthMonitoringConfiguration | Where-Object {$_.FirstTestUserSipUri -eq "sip:pilar@litwareinc.com"} | Set-CsHealthMonitoringConfiguration -FirstTestUserSipUri "sip:kenmyer@litwareinc.com" -FirstTestSamAccountName "litwareinc\kenmyer"

## Descrizione dettagliata

Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di completare correttamente normali attività, ad esempio l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono in una rete PSTN (Public Switched Telephone Network). Questi test possono essere eseguiti manualmente da un amministratore oppure automaticamente da un'applicazione, ad esempio Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

È possibile condurre le transazioni in due diversi modi. Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare una account di test per ciascuno dei propri pool di registrazione. Questi account di test sono una coppia di account utente preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test e non di account appartenenti a utenti effettivi. Quando vengono configurati gli account di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su tale pool, senza dover specificare le identità degli account utente (e fornire le relative credenziali) coinvolti nel test. In realtà, la transazione sintetica utilizza automaticamente gli account di test preconfigurati durante l'esecuzione dei controlli.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando account utente effettivi. Ad esempio, se due utenti non riescono a scambiarsi messaggi istantanei, l'amministratore può eseguire una transazione sintetica utilizzando i due account in questione, anziché la coppia di account di test. Se si decide di condurre una transazione sintetica utilizzando gli account utente reali, sarà necessario fornire le credenziali per ogni utente.

Dopo aver configurato le impostazioni di configurazione del monitoraggio dell'integrità è possibile modificare tali impostazioni in qualsiasi momento con il cmdlet **Set-CsHealthMonitoringConfiguration**. Questo cmdlet fornisce un mezzo per modificare uno o entrambi gli account di test configurati per l'uso con un pool.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsHealthMonitoringConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsHealthMonitoringConfiguration"}

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
<td><p><em>FirstTestSamAccountName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>SamAccountName del primo utente di test. È necessario immettere FirstTestSamAccountName utilizzando il formato dominio\nome utente, ad esempio:</p>
<p>-FirstTestSamAccountName litwareinc\kenmyer</p></td>
</tr>
<tr class="odd">
<td><p><em>FirstTestUserSipUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP del primo utente di test da configurare per l'uso da parte di questa raccolta di impostazioni di monitoraggio dell'integrità. L'indirizzo SIP deve includere il prefisso sip:. Ad esempio: -FirstTestUserSipUri &quot;sip:kenmyer@litwareinc.com&quot;.</p></td>
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
<td><p>Nome di dominio completo (FQDN) del pool a cui sono state assegnate le impostazioni di configurazione del monitoraggio dell'integrità da modificare. Ad esempio: -Identity atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto HealthMonitoringSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondTestSamAccountName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>SamAccountName del secondo utente di test. È necessario immettere SecondTestSamAccountName utilizzando il formato dominio\nome utente, ad esempio:</p>
<p>-SecondTestSamAccountName litwareinc\pilar</p></td>
</tr>
<tr class="even">
<td><p><em>SecondTestUserSipUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP del secondo utente di test da configurare per l'uso da parte di questa raccolta di impostazioni di monitoraggio dell'integrità. L'indirizzo SIP deve includere il prefisso sip:. Ad esempio: -FirstTestUserSipUri &quot;sip:pilar@litwareinc.com&quot;.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings. Il cmdlet **Set-CsHealthMonitoringConfiguration** accetta le istanze dell'oggetto di configurazione del monitoraggio dello stato inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsHealthMonitoringConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)  
[Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)

