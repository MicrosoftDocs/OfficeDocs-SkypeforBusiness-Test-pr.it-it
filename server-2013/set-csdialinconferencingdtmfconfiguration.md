---
title: Set-CsDialInConferencingDtmfConfiguration
TOCTitle: Set-CsDialInConferencingDtmfConfiguration
ms:assetid: cc22353e-6c14-49b1-bf23-f952c100bfd8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398860(v=OCS.15)
ms:contentKeyID: 49301988
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDialInConferencingDtmfConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni della segnalazione DTMF (Dual Tone Multi-Frequency) per le conferenze telefoniche con accesso esterno. La tecnologia DTMF consente agli utenti che accedono dall'esterno a una conferenza di controllarne le impostazioni, ad esempio disattivare o riattivare il proprio audio oppure bloccare e sbloccare la conferenza, mediante la tastiera del telefono. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDialInConferencingDtmfConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDialInConferencingDtmfConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdmitAll <String>] [-AudienceMuteCommand <String>] [-CommandCharacter <String>] [-Confirm [<SwitchParameter>]] [-EnableDisableAnnouncementsCommand <String>] [-Force <SwitchParameter>] [-HelpCommand <String>] [-LockUnlockConferenceCommand <String>] [-MuteUnmuteCommand <String>] [-OperatorLineUri <String>] [-PrivateRollCallCommand <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 sostituisce il tasto assegnato al comando per l'abilitazione e la disabilitazione degli annunci, il cui valore predefinito è 9, con il tasto assegnato al comando per la disattivazione e l'attivazione dell'audio di tutti i partecipanti, il cui valore predefinito è 4, per le impostazioni DTMF globali. A tale scopo, vengono utilizzati due parametri diversi: EnableDisableAnnoucementsCommand, a cui viene assegnato il valore 4, e AudienceMuteCommand, a cui viene assegnato il valore 9. Poiché non è specificato il parametro Identity, queste modifiche avranno effetto sulle impostazioni DTMF globali.

    Set-CsDialInConferencingDtmfConfiguration -Identity global -EnableDisableAnnouncementsCommand 4 -AudienceMuteCommand 9

## ESEMPIO 2

Il comando mostrato nell'esempio 2 rappresenta una variazione del comando mostrato nel primo esempio. In questo caso, le modifiche avranno effetto sulle impostazioni DTMF che hanno il valore Identity site:Redmond.

    Set-CsDialInConferencingDtmfConfiguration -Identity site:Redmond -EnableDisableAnnouncementsCommand 4 -AudienceMuteCommand 9

## ESEMPIO 3

Il comando riportato nell'esempio 3 disabilita per il sito Redmond il comando per l'appello, ovvero la capacità di riprodurre un elenco di tutti i partecipanti alla conferenza. Per disabilitare questo comando, viene incluso il parametro PrivateRollCallCommand con valore $Null. Ciò significa che al comando non verrà associato alcun tasto, rendendolo così non disponibile per gli utenti.

    Set-CsDialInConferencingDtmfConfiguration -Identity "site:Redmond" -PrivateRollCallCommand $Null

## ESEMPIO 4

L'esempio 4 rappresenta una variazione dell'esempio 3. In questo esempio il comando per l'appello viene disabilitato per tutte le impostazioni DTMF configurate nell'ambito del sito. A questo scopo, nel comando vengono prima di tutto usati il cmdlet **Get-CsDialInConferencingDtmfConfiguration** e il parametro Filter per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito. Il valore di filtro "site:\*" circoscrive i dati restituiti alle impostazioni con valore Identity che inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsDialInConferencingDtmfConfiguration**, che imposta il valore della proprietà PrivateRollCallCommand su Null ($Null).

    Get-CsDialInConferencingDtmfConfiguration -Filter "site:*" | Set-CsDialInConferencingDtmfConfiguration -PrivateRollCallCommand $Null

## Descrizione dettagliata

Lync Server consente agli utenti di partecipare alle conferenze accedendo dall'esterno tramite il telefono. Gli utenti esterni non possono visualizzare video né scambiare messaggi istantanei con gli altri partecipanti della conferenza, ma possono partecipare completamente alla parte audio della riunione.

Oltre alla possibilità di partecipare a una conferenza, gli utenti possono inoltre gestire parti selezionate della conferenza mediante la tastiera del telefono. La gestione delle specifiche impostazioni della conferenza varia a seconda che l'utente sia o meno un relatore. Ad esempio, per impostazione predefinita, gli utenti possono premere il tasto 6 della tastiera per disattivare o riattivare il proprio audio. I partecipanti possono riprodurre in privato i nomi di tutti gli altri partecipanti alla riunione, mentre i relatori possono ad esempio disattivare e riattivare l'audio di tutti i partecipanti alla riunione e abilitare o disabilitare l'annuncio riprodotto ogni volta che qualcuno accede a una conferenza o la abbandona.

La possibilità di effettuare tali selezioni mediante la tastiera del telefono è nota come segnalazione DTMF (Dual-Tone Multifrequency, multifrequenza a doppio tono). Quando si compone un numero di telefono e una voce registrata indica ad esempio di "premere 1 per l'inglese o 2 per l'italiano", si sta usando la segnalazione DTMF.

Il cmdlet **Set-CsDialInConferencingDtmfConfiguration** consente di cambiare i tasti utilizzati per attivare i comandi supportati in una conferenza telefonica con accesso esterno di Lync Server.

Quando si modificano i comandi DTMF, tenere presenti due aspetti. In primo luogo, è possibile utilizzare solo i tasti numerici da 0 a 9. Tutti gli altri tasti che potrebbero essere presenti sulla tastiera, ad esempio il tasto \#, non sono consentiti. Esiste un'eccezione a questa regola: il parametro CommandCharacter consente di utilizzare solo il tasto asterisco (\*) o il tasto cancelletto (\#). Non è possibile assegnare un valore numerico al parametro CommandCharacter. Tutti gli altri parametri dei comandi accetteranno invece solo valori numerici.

In secondo luogo, ai comandi devono essere assegnati tasti univoci. Il tasto 4, ad esempio, non può essere utilizzato sia per disattivare e riattivare il proprio audio che per bloccare e sbloccare una conferenza. Ciò significa che, quando si modificano i tasti assegnati a un comando, potrebbe essere necessario sostituire i tasti utilizzati da due comandi diversi. Se ad esempio si desidera assegnare il tasto 4 a EnableDisableAnnouncementsCommand, il cui valore predefinito è 9, sarà necessario contestualmente assegnare il tasto 9 ad AudienceMuteCommand.

Per disabilitare un comando, impostarne il valore su Null ($Null).

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsDialInConferencingDtmfConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDialInConferencingDtmfConfiguration"}

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
<td><p><em>AdmitAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per consentire a tutti gli utenti che si trovano in sala di attesa di accedere immediatamente alla conferenza. Il valore predefinito è 8.</p></td>
</tr>
<tr class="even">
<td><p><em>AudienceMuteCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto che può essere premuto da un relatore per disattivare l'audio di tutti i partecipanti alla conferenza, ovvero verrà disattivato l'audio di tutti i partecipanti tranne quello del relatore. Il tasto predefinito è 4.</p></td>
</tr>
<tr class="odd">
<td><p><em>CommandCharacter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere all'inizio di un comando. Il tasto predefinito è l'asterisco (*). L'unico altro valore consentito è il tasto cancelletto (#).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDisableAnnouncementsCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per abilitare o disabilitare gli annunci ogni volta che qualcuno accede a una conferenza o abbandona la conferenza. Il tasto predefinito è 9.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per riprodurre in privato una descrizione di tutti i comandi DTMF. Il tasto predefinito è 1.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco per la raccolta di impostazioni DTMF da modificare. Per fare riferimento alle impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Set-CsDialInConferencingDtmfConfiguration</strong> modificherà le impostazioni DTMF globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DialInConferencingDtmfConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>LockUnlockConferenceCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per bloccare o sbloccare una conferenza. Se una conferenza è bloccata, non sarà consentito l'accesso a nuovi partecipanti, almeno finché la conferenza non viene sbloccata. Il tasto predefinito è 7.</p></td>
</tr>
<tr class="odd">
<td><p><em>MuteUnmuteCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per disattivare o riattivare il proprio audio. Viene utilizzato lo stesso tasto per passare dalla disattivazione all'attivazione audio e viceversa. Il tasto predefinito è 6.</p></td>
</tr>
<tr class="even">
<td><p><em>OperatorLineUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono a cui verrà connesso un utente PSTN dall'operatore automatico per le conferenze telefoniche con accesso esterno ogni volta che l'utente preme *0 sulla tastiera del telefono. La pressione di *0 è progettata per connettere gli utenti di conferenze telefoniche con accesso esterno all'operatore per l'assistenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateRollCallCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per riprodurre in privato il nome di ogni partecipante alla conferenza. Il tasto predefinito è 3.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration. Il cmdlet **Set-CsDialInConferencingDtmfConfiguration** accetta le istanze da pipeline dell'oggetto configurazione DTMF di conferenza telefonica con accesso esterno.

## Tipi restituiti

Il cmdlet **Set-CsDialInConferencingDtmfConfiguration** non restituisce un oggetto o un valore. Il cmdlet configura piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingDtmfConfiguration](get-csdialinconferencingdtmfconfiguration.md)  
[New-CsDialInConferencingDtmfConfiguration](new-csdialinconferencingdtmfconfiguration.md)  
[Remove-CsDialInConferencingDtmfConfiguration](remove-csdialinconferencingdtmfconfiguration.md)

