---
title: Remove-CsPrivacyConfiguration
TOCTitle: Remove-CsPrivacyConfiguration
ms:assetid: 32052c51-953d-4278-9425-306245d297ed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425821(v=OCS.15)
ms:contentKeyID: 49300106
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPrivacyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione della privacy. Le impostazioni di configurazione della privacy consentono di determinare quante informazioni gli utenti rendono disponibili agli altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsPrivacyConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite le informazioni di configurazione della privacy assegnate al sito Redmond. Quando queste impostazioni vengono eliminate, gli utenti nel sito Redmond erediteranno automaticamente le impostazioni di configurazione della privacy globali.

    Remove-CsPrivacyConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le impostazioni di configurazione della privacy assegnate nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPrivacyConfiguration** con il parametro Filter. Il valore di filtro "site:\*" garantisce che vengano restituite solo le impostazioni la cui identità inizia con i caratteri "site". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsPrivacyConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CsPrivacyConfiguration -Filter "site:*" | Remove-CsPrivacyConfiguration

## ESEMPIO 3

Il comando riportato nell'esempio 3 elimina tutte le impostazioni di configurazione della privacy per cui è stata disabilitata la modalità privacy. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPrivacyConfiguration** senza parametri per restituire una raccolta di tutte le impostazioni di configurazione della privacy in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnablePrivacyMode è uguale a True. La raccolta filtrata viene inviata tramite pipe al cmdlet **Remove-CsPrivacyConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Remove-CsPrivacyConfiguration

## Descrizione dettagliata

Lync Server offre agli utenti la possibilità di condividere con altre persone un'elevata quantità di informazioni sulla presenza grazie alla possibilità di pubblicare fotografie personali, di fornire informazioni dettagliate sulla località, di rendere automaticamente disponibili informazioni sulla presenza a chiunque sia presente nell'organizzazione (anziché rendere disponibili tali informazioni solo alle persone presenti nell'elenco Contatti personale).

Alcuni utenti apprezzeranno la possibilità di rendere disponibili queste informazioni ai propri colleghi, mentre altri potrebbero essere più restii a condividere questi dati. Ad esempio, molte persone potrebbero essere riluttanti a includere le proprie foto personali nei dati sulla presenza. In genere, gli utenti hanno il controllo sulle informazioni che intendono (o non intendono) condividere. Ad esempio, gli utenti possono selezionare o deselezionare una casella di controllo per controllare se condividere con altre persone le informazioni sulla posizione. I cmdlet di configurazione della privacy inoltre consentono agli amministratori di gestire le impostazioni di privacy degli utenti. In alcuni casi, gli amministratori possono abilitare o disabilitare le impostazioni. Ad esempio, se la proprietà AutoInitiateContacts è impostata su True, i membri del team vengono automaticamente aggiunti all'elenco Contatti di ogni utente. Se è impostata su False, i membri del team non vengono automaticamente aggiunti all'elenco Contatti di ogni utente.

In altri casi, gli amministratori possono configurare i valori predefiniti in Lync Server consentendo comunque agli utenti di modificare tali valori. Ad esempio, i dati sulla posizione vengono pubblicati per gli utenti per impostazione predefinita, nonostante gli utenti abbiano il diritto di disabilitare la pubblicazione della posizione. Impostando la proprietà PublishLocationDataByDefault su False, gli amministratori possono modificare questo comportamento: in tal caso, i dati sulla posizione non verranno pubblicati per impostazione predefinita, nonostante gli utenti abbiano comunque il diritto di pubblicare questi dati se lo desiderano.

Le impostazioni di configurazione della privacy possono essere applicate nell'ambito globale, nell'ambito del sito e nell'ambito del servizio (ma solo per il servizio Server utenti). Il cmdlet **Remove-CsPrivacyConfiguration** consente di eliminare le impostazioni configurate nell'ambito del sito o del servizio. Ad esempio, se si esegue il cmdlet per le impostazioni configurate nell'ambito del sito, tali impostazioni verranno eliminate e le impostazioni di privacy per gli utenti nel sito saranno gestite dalla raccolta globale. Il cmdlet **Remove-CsPrivacyConfiguration** può essere eseguito anche per la raccolta globale, ma quest'ultima non verrà eliminata. Tutte le proprietà della raccolta verranno invece reimpostate sui rispettivi valori predefiniti. Ad esempio, si supponga di avere precedentemente modificato la proprietà EnablePrivacyMode impostandola su True. Se ora si "elimina" la raccolta globale, EnablePrivacyMode verrà reimpostata sul valore predefinito False.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsPrivacyConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPrivacyConfiguration"}

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
<td><p>Identificatore univoco per le impostazioni di configurazione della privacy da rimuovere. Per rimuovere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity site:Redmond. Per rimuovere le impostazioni a livello del servizio, utilizzare una sintassi simile a quella riportata di seguito: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>Il cmdlet <strong>Remove-CsPrivacyConfiguration</strong> può essere eseguito anche per la raccolta globale di impostazioni. In tal caso, le impostazioni globali però non verranno eliminate. Tutte le proprietà della raccolta verranno invece reimpostate sui rispettivi valori predefiniti.</p></td>
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
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui vengono eliminate le impostazioni di configurazione della privacy. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration. Il cmdlet **Remove-CsPrivacyConfiguration** accetta l'input da pipeline dell'oggetto configurazione della privacy.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPrivacyConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

