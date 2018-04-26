---
title: New-CsDialInConferencingDtmfConfiguration
TOCTitle: New-CsDialInConferencingDtmfConfiguration
ms:assetid: 2e373bab-fc4c-4b8b-96e7-fc23ac3bcf47
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425792(v=OCS.15)
ms:contentKeyID: 49300048
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingDtmfConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni della segnalazione DTMF (Dual Tone Multi-Frequency) per le conferenze telefoniche con accesso esterno. La tecnologia DTMF consente agli utenti che accedono dall'esterno a una conferenza di controllare le impostazioni della conferenza, ad esempio disattivare e riattivare il proprio audio o bloccare e sbloccare la conferenza, mediante la tastiera del telefono. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDialInConferencingDtmfConfiguration -Identity <XdsIdentity> [-AdmitAll <String>] [-AudienceMuteCommand <String>] [-CommandCharacter <String>] [-Confirm [<SwitchParameter>]] [-EnableDisableAnnouncementsCommand <String>] [-Force <SwitchParameter>] [-HelpCommand <String>] [-InMemory <SwitchParameter>] [-LockUnlockConferenceCommand <String>] [-MuteUnmuteCommand <String>] [-OperatorLineUri <String>] [-PrivateRollCallCommand <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creato un nuovo set di impostazioni di configurazione DTMF per il sito Redmond. In questo esempio, la proprietà MuteUnmuteCommand è impostata su 4 e la proprietà AudienceMuteCommand è impostata su 6.

    New-CSDialInConferencingDtmfConfiguration -Identity site:Redmond -MuteUnmuteCommand 4 -AudienceMuteCommand 6

## ESEMPIO 2

Nell'esempio 2 viene creato un nuovo insieme di impostazioni di configurazione DTMF per il sito Redmond. In questo esempio viene disabilitata la proprietà AdmitAll utilizzando il parametro AdmitAll e impostando il relativo valore su Null.

    New-CSDialInConferencingDtmfConfiguration -Identity site:Redmond -AdmitAll $Null

## ESEMPIO 3

Nell'esempio 3 viene illustrato come utilizzare il parametro InMemory per creare un'istanza solo in memoria di una raccolta di impostazioni di configurazione DTMF, modificare tali impostazioni e quindi utilizzare il cmdlet **Set-CSDialInConferencingDtmfConfiguration** per creare una raccolta effettiva con l'identità site:Redmond. A tale scopo, il primo comando dell'esempio crea una nuova istanza solo in memoria di una raccolta di impostazioni di configurazione DTMF e archivia tale istanza in una variabile denominata $x. Queste impostazioni saranno presenti solo in memoria. Se si chiude Windows PowerShell o si elimina la variabile $x, le impostazioni verranno eliminate e non verranno mai applicate al sito Redmond.

I tre comandi seguenti modificano le proprietà di questa raccolta di impostazioni DTMF "virtuale". I comandi 2, 3 e 4 assegnano nuovi valori rispettivamente ad AdmitAll, MuteUnmuteCommand e AudienceMuteCommand. Il comando finale utilizza quindi il cmdlet **Set-CSDialInConferencingDtmfConfiguration** e il parametro Instance per trasformare le impostazioni virtuali archiviate in $x in una raccolta effettiva di impostazioni configurate per il sito Redmond.

    $x = New-CSDialInConferencingDtmfConfiguration -Identity site:Redmond -InMemory
    $x.AdmitAll = $Null
    $x.MuteUnmuteCommand = 4 
    $x.AudienceMuteCommand = 6
    Set-CSDialInConferencingDtmfConfiguration -Instance $x

## Descrizione dettagliata

Lync Server consente agli utenti di partecipare alle conferenze accedendo dall'esterno tramite il telefono. Gli utenti esterni non possono visualizzare video né scambiare messaggi istantanei con gli altri partecipanti della conferenza, ma possono partecipare completamente alla parte audio della riunione.

Oltre alla possibilità di partecipare a una conferenza, gli utenti possono inoltre gestire parti selezionate della conferenza mediante la tastiera del telefono. La gestione delle specifiche impostazioni della conferenza varia a seconda che l'utente sia o meno un relatore. Ad esempio, per impostazione predefinita, gli utenti possono premere il tasto 6 della tastiera per disattivare o riattivare il proprio audio. I partecipanti possono riprodurre in privato i nomi di tutti gli altri partecipanti alla riunione, mentre i relatori possono ad esempio disattivare e riattivare l'audio di tutti i partecipanti alla riunione e abilitare o disabilitare l'annuncio riprodotto ogni volta che qualcuno accede a una conferenza o la abbandona.

La possibilità di eseguire queste operazioni tramite la tastiera del telefono è definita "segnale DTMF (Dual Tone Multi-Frequency)": chiunque abbia mai digitato un numero telefonico e ascoltato messaggi tipo "Premere 1 per attivare questa opzione o premere 2 per parlare con un operatore" ha utilizzato un segnale DTMF.

Quando si installa Lync Server, viene automaticamente creata una raccolta globale di impostazioni DTMF. Oltre a queste impostazioni globali, è possibile utilizzare il cmdlet **New-CSDialInConferencingDtmfConfiguration** per creare impostazioni personalizzate sito per sito. È ad esempio possibile creare una nuova raccolta di impostazioni per il sito Redmond (e solo per il sito Redmond) che utilizzi il tasto 4 anziché il tasto 6 per attivare o disattivare l'audio del microfono. Si noti che qualsiasi impostazione che si configura con ambito del sito ha la priorità sulle impostazioni configurate con ambito globale. Come risultato, gli utenti del sito Redmond utilizzeranno il tasto 4 per attivare o disattivare l'audio del microfono anche se le impostazioni globali prevedono l'utilizzo del tasto 6 per tale scopo.

È possibile disporre di una sola raccolta di impostazioni DTMF e di una raccolta globale per sito. Si supponga, ad esempio, di disporre già di una raccolta con identità site:Redmond e di tentare di eseguire il comando seguente:

New- CSDialInConferencingDtmfConfiguration –Identity site:Redmond

Questo comando non riuscirà poiché la raccolta site:Redmond esiste già. Se si desidera modificare le impostazioni del sito Redmond, utilizzare il cmdlet **Set-CSDialInConferencingDtmfConfiguration** o rimuovere la raccolta esistente e quindi creare una nuova raccolta che utilizza l'identità site:Redmond.

Quando si configurano valori per i comandi DTMF, tenere presenti due aspetti. Innanzitutto, è esclusivamente possibile utilizzare i tasti numerici da 0 a 9 e l'asterisco (\*); non consentito alcun altro tasto presente sul tastierino (quale il tasto \#). Con una eccezione: il parametro CommandCharacter accetta solo il tasto asterisco (\*) o cancelletto (\#). In secondo luogo, ai comandi devono essere assegnati tasti univoci. Il tasto 4, ad esempio, non può essere utilizzato sia per disattivare e riattivare il proprio audio che per bloccare e sbloccare una conferenza. Ciò significa che, quando si modificano i tasti assegnati a un comando, potrebbe essere necessario sostituire i tasti utilizzati da due comandi diversi. Se ad esempio si desidera assegnare il tasto 4 al comando EnableDisableAnnouncementsCommand, il cui valore predefinito è 9, sarà necessario contestualmente assegnare il tasto 9 al comando AudienceMuteCommand.

Per disabilitare un comando, impostarne il valore su Null ($Null).

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsDialInConferencingDtmfConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingDtmfConfiguration"}

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
<td><p>Identificatore univoco da assegnare alla nuova raccolta di impostazioni di configurazione DTMF. Poiché è possibile creare nuove raccolte solo nell'ambito del sito, l'identità avrà sempre il prefisso &quot;site:&quot; seguito dal nome del sito; ad esempio &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>AdmitAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per consentire a tutti gli utenti che si trovano in sala di attesa di accedere immediatamente alla conferenza. Il valore predefinito è 8.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudienceMuteCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto che un relatore può premere per attivare o disattivare l'audio di tutti gli altri partecipanti alla conferenza (verrà attivato o disattivato l'audio di tutti i partecipanti tranne il relatore). Il tasto predefinito è 4.</p></td>
</tr>
<tr class="even">
<td><p><em>CommandCharacter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere all'inizio di un comando. Il tasto predefinito è asterisco (*). Il solo valore consentito è #.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDisableAnnouncementsCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per abilitare o disabilitare gli annunci ogni volta che qualcuno accede a una conferenza o abbandona la conferenza. Il tasto predefinito è 9.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>HelpCommand</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tasto da premere per riprodurre in privato una descrizione di tutti i comandi DTMF. Il tasto predefinito è 1.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. Il cmdlet **New-CsDialInConferencingDtmfConfiguration** non accetta l'input da pipeline.

## Tipi restituiti

Consente di creare nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingDtmfConfiguration](get-csdialinconferencingdtmfconfiguration.md)  
[Remove-CsDialInConferencingDtmfConfiguration](remove-csdialinconferencingdtmfconfiguration.md)  
[Set-CsDialInConferencingDtmfConfiguration](set-csdialinconferencingdtmfconfiguration.md)

