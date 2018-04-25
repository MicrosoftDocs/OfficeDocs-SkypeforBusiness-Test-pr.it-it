---
title: Remove-CsArchivingConfiguration
TOCTitle: Remove-CsArchivingConfiguration
ms:assetid: d83b8935-079e-47d0-ba48-c95dd07965c0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398951(v=OCS.15)
ms:contentKeyID: 49302131
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsArchivingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta di impostazioni di archiviazione specificata. Le impostazioni di archiviazione vengono utilizzate per abilitare o disabilitare il salvataggio automatico delle sessioni di messaggistica istantanea e per bloccare facoltativamente i messaggi istantanei che non possono essere archiviati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsArchivingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsArchivingConfiguration** per eliminare le impostazioni di configurazione dell'archiviazione con il parametro Identity site:Redmond.

    Remove-CsArchivingConfiguration -Identity site:Redmond

## ESEMPIO 2

Il comando mostrato nell'esempio 2 rimuove tutte le impostazioni di configurazione dell'archiviazione configurate nell'ambito del sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsArchivingConfiguration** con il parametro Filter per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito. A tale scopo, viene utilizzato il valore di filtro "site:\*", che limita i dati restituiti alle impostazioni in cui il parametro Identity inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsArchivingConfiguration** che elimina ogni elemento presente nella raccolta.

    Get-CsArchivingConfiguration -Filter "site:*" | Remove-CsArchivingConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione dell'archiviazione in cui la proprietà EnableArchiving è stata impostata su "None". Per eseguire questa attività, viene chiamato il cmdlet **Get-CsArchivingConfiguration** senza alcun parametro, in modo da restituire una raccolta di tutte le impostazioni di archiviazione configurate per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableArchiving è uguale a "None". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsArchivingConfiguration** che elimina ogni elemento presente nella raccolta.

    Get-CsArchivingConfiguration | Where-Object {$_.EnableArchiving -eq "None"} | Remove-CsArchivingConfiguration

## Descrizione dettagliata

Molte organizzazioni trovano utile trascrivere tutte le sessioni di messaggistica istantanea e le conferenze a cui partecipano i propri utenti. In altri casi tali trascrizioni sono obbligatorie, ad esempio numerose organizzazioni operanti nel settore finanziario sono tenute per legge a conservare copie di tutte le comunicazioni elettroniche.

Lync Server offre grande flessibilità nell'archiviazione di sessioni di messaggistica istantanea e conferenze Web. Se è stato distribuito server di archiviazione, sarà possibile utilizzare i diversi cmdlet **CsArchivingConfiguration** per abilitare e disabilitare l'archiviazione delle sessioni di messaggistica istantanea e per gestire il database di archiviazione. Se l'archiviazione non dovesse riuscire, è inoltre possibile sospendere la messaggistica istantanea. Questo consente di conservare un record di tutte le comunicazioni elettroniche.

Quando si installa Lync Server, viene creata automaticamente una raccolta di impostazioni di archiviazione globali. Per impostazione predefinita, tali impostazioni verranno applicate all'intera organizzazione. In alternativa, è possibile utilizzare il cmdlet **New-CsArchivingConfiguration** per creare impostazioni di configurazione personalizzate per i singoli siti. Tutte le impostazioni specifiche del sito create con il cmdlet **New-CsArchivingConfiguration** possono essere successivamente rimosse con il cmdlet **Remove-CsArchivingConfiguration**. Quando si rimuovono le impostazioni per un sito, al sito interessato verranno applicate le impostazioni globali.

Si noti che il cmdlet **Remove-CsArchivingConfiguration** può anche essere eseguito sulle impostazioni di archiviazione globali. In tal caso, però, le impostazioni non verranno rimosse, poiché non è possibile eliminare le impostazioni globali. Verranno invece ripristinati i valori predefiniti di tutte le proprietà globali. Si supponga, ad esempio, di aver abilitato l'archiviazione delle sessioni di messaggistica istantanea in ambito globale e di eseguire successivamente questo comando:

Remove-CsArchivingConfiguration -Identity global

L'esecuzione del comando reimposterà i valori delle proprietà per le impostazioni globali, ovvero verrà ripristinato il valore predefinito None di EnableArchiving, disabilitando a sua volta l'archiviazione nell'ambito globale.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsArchivingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsArchivingConfiguration"}

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
<td><p>Identificatore univoco per la raccolta delle impostazioni di configurazione dell'archiviazione da rimuovere. Per rimuovere la raccolta globale, utilizzare la seguente sintassi: -Identity global. Si noti che non è possibile rimuovere effettivamente le impostazioni globali ma è possibile solo reimpostare i valori predefiniti delle proprietà. Per rimuovere la raccolta di un sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per rimuovere le impostazioni configurate per un singolo pool di registrazione, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p>
<p>Si noti che le impostazioni a livello di pool sono disponibili solo in Lync Server 2013.</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica un valore Identity criterio.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings. Il cmdlet **Remove-CsArchivingConfiguration** accetta input inviato tramite pipe degli oggetti di configurazione dell'archiviazione.

## Tipi restituiti

Il cmdlet **Remove-CsArchivingConfiguration** non restituisce un valore o un oggetto. Questo cmdlet rimuove piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)  
[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)

