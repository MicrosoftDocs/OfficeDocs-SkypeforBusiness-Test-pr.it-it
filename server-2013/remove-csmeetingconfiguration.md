---
title: Remove-CsMeetingConfiguration
TOCTitle: Remove-CsMeetingConfiguration
ms:assetid: a5d4c758-25f6-4cdb-a5b7-dbb0fb1d8488
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412775(v=OCS.15)
ms:contentKeyID: 49301569
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMeetingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Remove-CsMeetingConfiguration** consente di eliminare una raccolta esistente di impostazioni di configurazione di riunione. Tali impostazioni consentono di stabilire il tipo di riunioni (definite anche "conferenze") che gli utenti possono creare, nonché di controllare il modo in cui gli utenti anonimi e gli utenti di conferenze telefoniche con accesso esterno possono eventualmente partecipare a tali riunioni. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsMeetingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono rimosse le impostazioni di configurazione riunione con Identity site:Redmond. Una volta rimosse queste impostazioni dal sito Redmond, gli utenti del sito erediteranno automaticamente le impostazioni di configurazione riunione globali.

    Remove-CsMeetingConfiguration -Identity site:Redmond

## ESEMPIO 2

Il comando mostrato nell'esempio 2 rimuove tutte le impostazioni di riunione configurate nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsMeetingConfiguration** con il parametro Filter. I valore di filtro "site:\*" assicura che vengano selezionate solo le impostazioni con valore Identity che inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsMeetingConfiguration**, che elimina tutti gli elementi della raccolta.

    Get-CsMeetingConfiguration -Filter "site:*" | Remove-CsMeetingConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le raccolte di impostazioni di configurazione di riunione in cui la proprietà AdmitAnonymousUsersbyDefault è impostata su True. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsMeetingConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione di riunione attualmente in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente le impostazioni in cui la proprietà AdmitAnonymousUsersByDefault è uguale a True. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsMeetingConfiguration**, che procede alla rimozione di ogni elemento della raccolta.

    Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $True} | Remove-CsMeetingConfiguration

## Descrizione dettagliata

Le riunioni online, note anche come conferenze, sono parte integrante di Lync Server. I cmdlet **CsMeetingConfiguration** consentono agli amministratori di controllare il tipo di riunioni che gli utenti possono creare, nonché di determinare come devono essere gestiti nelle riunioni gli utenti anonimi e gli utenti di conferenze telefoniche con accesso esterno. È ad esempio possibile configurare le riunioni in modo che venga ammesso automaticamente chiunque accede mediante connessione telefonica esterna tramite rete PSTN (Public Switched Telephone Network). In alternativa, è possibile configurare le riunioni in modo che gli utenti con accesso esterno non vengano ammessi automaticamente, bensì vengano instradati alla sala d'attesa. Questi utenti rimarranno in attesa finché un relatore non li ammetterà alla riunione.

Le impostazioni di configurazione di riunione possono essere assegnate nell'ambito globale, del sito o del servizio. Se si creano nuove impostazioni nell'ambito del sito o del servizio, sarà possibile rimuoverle in un secondo momento tramite il cmdlet **Remove-CsMeetingConfiguration**. È inoltre possibile eseguire il cmdlet **Remove-CsMeetingConfiguration** per le impostazioni di riunione globali. In questo caso, le impostazioni globali non vengono rimosse, poiché non è possibile rimuoverle. Tuttavia, per tutte le proprietà della raccolta globale vengono ripristinate i valori predefiniti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsMeetingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsMeetingConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione riunione da rimuovere. Per &quot;rimuovere&quot; le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Come evidenziato in precedenza, non è possibile rimuovere del tutto le impostazioni globali, bensì è consentito ripristinarne le proprietà in base ai rispettivi valori predefiniti. Per rimuovere le impostazioni dall'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. È possibile rimuovere le impostazioni del servizio, utilizzando la sintassi: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity.</p></td>
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
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per le impostazioni di configurazione di riunione da eliminare, ad esempio:</p>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration. Il cmdlet **Remove-CsMeetingConfiguration** accetta istanze dell'oggetto configurazione riunione inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsMeetingConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)  
[New-CsMeetingConfiguration](new-csmeetingconfiguration.md)  
[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

