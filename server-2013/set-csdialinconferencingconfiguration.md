---
title: Set-CsDialInConferencingConfiguration
TOCTitle: Set-CsDialInConferencingConfiguration
ms:assetid: 3300343f-c075-4b4f-aaa4-091dbf1fcd90
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425825(v=OCS.15)
ms:contentKeyID: 49300115
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialInConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni che determinano la modalità di risposta di Lync Server quando gli utenti abbandonano o accedono a una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDialInConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDialInConferencingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 modifica la proprietà EntryExitAnnoucements per le impostazioni di configurazione per conferenze telefoniche con accesso esterno per il sito Redmond. In questo caso la proprietà EntryExitAnnouncementsType è impostata su ToneOnly.

    Set-CsDialInConferencingConfiguration -Identity site:Redmond -EntryExitAnnouncementsType "ToneOnly"

## ESEMPIO 2

Nell'esempio 2 vengono modificate tutte le impostazioni di configurazione per conferenze telefoniche con accesso esterno in uso nell'organizzazione. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsDialInConferencingConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione per conferenze telefoniche con accesso esterno. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsDialInConferencingConfiguration**, che imposta la proprietà EnableNameRecording di ogni elemento della raccolta su True ($True).

    Get-CsDialInConferencingConfiguration | Set-CsDialInConferencingConfiguration -EnableNameRecording $True

## ESEMPIO 3

Nell'esempio 3 vengono modificate tutte le impostazioni per conferenze telefoniche con accesso esterno configurate nell'ambito del sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsDialInConferencingConfiguration** e il parametro Filter per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito. Il valore di filtro "site:\*" circoscrive i dati restituiti alle impostazioni in cui la proprietà Identity inizia con il valore stringa "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsDialInConferencingConfiguration**, che modifica le proprietà EnableNameRecording ed EntryExitAnnouncementsType di ogni elemento della raccolta. Al termine dell'esecuzione del comando, tutte le impostazioni per conferenze telefoniche con accesso esterno configurate nell'ambito del sito avranno la proprietà EnableNameRecording impostata su True e la proprietà EntryExitAnnoucements impostata su "UseNames".

    Get-CsDialInConferencingConfiguration -Filter "site:*" | Set-CsDialInConferencingConfiguration -EnableNameRecording $True -EntryExitAnnouncementsType "UseNames"

## Descrizione dettagliata

Quando gli utenti accedono o escono da una conferenza telefonica, Lync Server può comportarsi in diversi modi. È possibile ad esempio che ai partecipanti venga richiesto di registrare il proprio nome prima di accedere alla conferenza. Analogamente, gli amministratori possono decidere se impostare un annuncio di Lync Server che segnala l'accesso o l'uscita dei partecipanti dalla conferenza telefonica.

Questi "comportamenti di partecipazione" alla conferenza vengono gestiti tramite le impostazioni di configurazione della conferenza telefonica con accesso esterno; è possibile configurare queste impostazioni nell'ambito globale o del sito. Al momento dell'installazione di Lync Server, le uniche impostazioni di configurazione per le conferenze telefoniche con accesso esterno disponibili sono quelle dell'ambito globale. È tuttavia possibile creare nuove impostazioni nell'ambito del sito tramite il cmdlet **New-CsDialInConferencingConfiguration**. È inoltre possibile modificare una o più impostazioni di configurazione nell'ambito globale o del sito tramite il cmdlet **Set-CsDialInConferencingConfiguration**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsDialInConferencingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialInConferencingConfiguration"}

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
<td><p><em>EnableNameRecording</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se richiedere agli utenti di registrare il proprio nome prima di accedere alla conferenza. Impostare True per abilitare la registrazione del nome o False per disabilitarla. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se viene impostato su True saranno riprodotti degli annunci ogni volta che un partecipante si unisce o abbandona una conferenza. Se è impostato su False (valore predefinito), gli annunci di ingresso e abbandono non vengono riprodotti.</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.EntryExitAnnouncementsType</p></td>
<td><p>Indica l'azione svolta dal sistema ogni volta che un partecipante si unisce a una conferenza o la abbandona. Gli annunci vengono effettuati solo se il parametro EntryExitAnnoucementsEnabledByDefault è impostato su True. I valori validi sono i seguenti:</p>
<p>UseNames. Il nome della persona viene annunciato ogni volta che si unisce a una conferenza o la abbandona, ad esempio &quot;Ken Myer sta abbandonando la conferenza&quot;.</p>
<p>ToneOnly. Ogni volta che un partecipante si unisce o abbandona una conferenza viene riprodotto un segnale acustico.</p>
<p>Il valore predefinito è UseNames.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità delle impostazioni di configurazione della conferenza telefonica con accesso esterno da modificare. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per referenziare le impostazioni del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity site:Redmond. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration. Il cmdlet **Set-CSDialInConferencingConfiguration** accetta le istanze dell'oggetto di configurazione per conferenze telefoniche con accesso esterno inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CSDialInConferencingConfiguration** non restituisce oggetti o valori. Il cmdlet invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[New-CsDialInConferencingConfiguration](new-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)

