---
title: Remove-CsDialInConferencingConfiguration
TOCTitle: Remove-CsDialInConferencingConfiguration
ms:assetid: 0c7f2a69-eeed-41bf-8ba7-5cc36dfdfa3c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398174(v=OCS.15)
ms:contentKeyID: 49299658
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialInConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più raccolte di impostazioni di configurazione delle conferenze telefoniche con accesso esterno. Queste impostazioni determinano la modalità di risposta di Lync Server quando gli utenti partecipano o abbandonano una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono eliminate le impostazioni di configurazione delle conferenze telefoniche con accesso esterno per il sito Redmond.

    Remove-CSDialInConferencingConfiguration -Identity "site:Redmond"

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le impostazioni di conferenze telefoniche con accesso esterno configurate nell'ambito del sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CSDialInConferencingConfiguration** e il parametro Filter per restituire una raccolta di tutte le impostazioni di conferenze telefoniche con accesso esterno configurate nell'ambito del sito. Il valore di filtro "site:\*" garantisce che vengano restituite solo le impostazioni la cui identità inizia con il valore stringa "site:". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CSDialInConferencingConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CSDialInConferencingConfiguration -Filter "site:*" | Remove-CSDialInConferencingConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione delle conferenze telefoniche con accesso esterno che non utilizzano la registrazione del nome. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CSDialInConferencingConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione delle conferenze telefoniche con accesso esterno attualmente in uso nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableNameRecording è uguale a False. Questa raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CSDialInConferencingConfiguration**, che elimina ogni elemento della raccolta.

    Get-CSDialInConferencingConfiguration | Where-Object {$_.EnableNameRecording -eq $False} | Remove-CSDialInConferencingConfiguration

## Descrizione dettagliata

Quando gli utenti accedono o escono da una conferenza telefonica, Lync Server può comportarsi in diversi modi. È possibile ad esempio che ai partecipanti venga richiesto di registrare il proprio nome prima di accedere alla conferenza. Analogamente, gli amministratori possono decidere se impostare un annuncio di Lync Server che segnala l'accesso o l'uscita dei partecipanti dalla conferenza telefonica.

Questi "comportamenti" relativi alla conferenza vengono gestiti utilizzando le impostazioni di configurazione della conferenza telefonica; queste impostazioni possono essere configurate nell'ambito globale o nell'ambito del sito. Le impostazioni configurate nell'ambito del sito hanno la precedenza su quelle configurate nell'ambito globale. Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni di configurazione delle conferenze telefoniche con accesso esterno. Se si desidera applicare diverse impostazioni a un sito (o a un gruppo di siti), è possibile creare queste raccolte utilizzando il cmdlet **New-CSDialInConferencingConfiguration**.

Il cmdlet **Remove-CSDialInConferencingConfiguration** consente di eliminare tutte le impostazioni delle conferenze telefoniche con accesso esterno configurate nell'ambito del sito. Quando queste impostazioni specifiche del sito vengono eliminate, agli utenti che fanno parte di questi siti verranno applicate le impostazioni globali.

Il cmdlet **Remove-CSDialInConferencingConfiguration** può anche essere eseguito per le impostazioni globali delle conferenze telefoniche con accesso remoto. In questo caso, le impostazioni globali non verranno rimosse perché non è possibile rimuovere le impostazioni di questo tipo, ma verranno ripristinati i valori predefiniti di tutte le proprietà della raccolta di impostazioni.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsDialInConferencingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialInConferencingConfiguration"}

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
<td><p>Indica l'identità delle impostazioni di configurazione delle conferenze telefoniche da rimuovere. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per far riferimento alle impostazioni del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity.</p></td>
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
<td><p>Consente di ignorare la visualizzazione di messaggi di errore non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration. Il cmdlet **Remove-CSDialInConferencingConfiguration** accetta le istanze da pipeline dell'oggetto di configurazione delle conferenze telefoniche con accesso esterno.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CSDialInConferencingConfiguration** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[New-CsDialInConferencingConfiguration](new-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

