---
title: Remove-CsDialInConferencingDtmfConfiguration
TOCTitle: Remove-CsDialInConferencingDtmfConfiguration
ms:assetid: 3cd6313c-fd0a-4fb2-bacd-b1bdf2a59430
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425894(v=OCS.15)
ms:contentKeyID: 49300270
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialInConferencingDtmfConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni della segnalazione DTMF (Dual Tone Multi-Frequency) per le conferenze telefoniche con accesso esterno. La tecnologia DTMF consente agli utenti che accedono dall'esterno a una conferenza di controllarne le impostazioni, ad esempio disattivare o riattivare il proprio audio oppure bloccare e sbloccare la conferenza, mediante la tastiera del telefono. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDialInConferencingDtmfConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene eliminata la raccolta di impostazioni di configurazione DTMF con identità (Identity) site:Redmond.

    Remove-CSDialInConferencingDtmfConfiguration -Identity site:Redmond

## ESEMPIO 2

Il comando riportato nell'esempio 2 elimina tutte le impostazioni DTMF configurate nell'ambito del sito. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CSDialInConferencingDtmfConfiguration** e il parametro Filter per restituire una raccolta di tutte le impostazioni DTMF configurate nell'ambito del sito. Il valore di filtro "site:\*" fa sì che vengano restituite solo le impostazioni in cui l'identità inizia con il valore stringa "site:". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CSDialInConferencingConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CSDialInConferencingDtmfConfiguration -Filter "site:*" | Remove-CSDialInConferencingDtmfConfiguration

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il cmdlet **Remove-CSDialInConferencingDtmfConfiguration** per eliminare tutte le impostazioni DTMF in cui la proprietà PrivateRollCallCommand è uguale a un valore Null. Ciò significa che l'appello presenze privato è stato disabilitato. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CSDialInConferencingDtmfConfiguration** per restituire una raccolta di tutte le impostazioni DTMF attualmente in uso nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà PrivateRollCallCommand è uguale a un valore Null. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CSDialInConferencingDtmfConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CSDialInConferencingDtmfConfiguration | Where-Object {$_.PrivateRollCallCommand -eq $Null} | Remove-CSDialInConferencingDtmfConfiguration

## Descrizione dettagliata

Lync Server consente agli utenti di partecipare alle conferenze accedendo dall'esterno tramite telefono. Gli utenti esterni non possono visualizzare video né scambiare messaggi istantanei con gli altri partecipanti alla conferenza, ma possono partecipare completamente alla parte audio della riunione.

Oltre alla possibilità di partecipare a una conferenza, gli utenti possono inoltre gestire parti selezionate della conferenza mediante la tastiera del telefono. La gestione delle specifiche impostazioni della conferenza varia a seconda che l'utente sia o meno un relatore. Ad esempio, per impostazione predefinita, gli utenti possono premere il tasto 6 della tastiera per disattivare o riattivare il proprio audio. I partecipanti possono riprodurre in privato i nomi di tutti gli altri partecipanti alla riunione, mentre i relatori, ad esempio, possono disattivare e riattivare l'audio di tutti i partecipanti alla riunione e abilitare o disabilitare l'annuncio riprodotto ogni volta che qualcuno accede a una conferenza o abbandona la conferenza.

La possibilità di effettuare tali selezioni mediante la tastiera del telefono è nota come segnalazione DTMF: quando si compone un numero di telefono e la voce registrata chiede di "premere 1 per l'inglese o 2 per l'italiano", questo è un esempio di segnalazione DTMF.

Quando si installa Lync Server, viene automaticamente creata una raccolta globale di impostazioni DTMF. Oltre a queste impostazioni globali, è possibile utilizzare il cmdlet **New-CSDialInConferencingDtmfConfiguration** per creare impostazioni personalizzate per ogni sito. Le impostazioni create nell'ambito del sito potranno essere successivamente rimosse utilizzando il cmdlet **Remove-CSDialInConferencingDtmfConfiguration**. Quando si rimuovono le impostazioni DTMF applicate nell'ambito del sito, agli utenti di tale sito verranno automaticamente applicate le impostazioni di configurazione DTMF globali.

Il cmdlet **Remove-CSDialInConferencingDtmfConfiguration** può anche essere eseguito per le impostazioni globali. In questo caso, le impostazioni globali tuttavia non verranno rimosse perché non è possibile rimuovere le impostazioni DTMF globali. Verranno invece ripristinati i valori predefiniti delle proprietà di tali impostazioni. Ad esempio, si supponga di avere modificato le impostazioni globali in modo da poter utilizzare il tasto 4 per disattivare/riattivare il microfono. Se ora si esegue il cmdlet **Remove-CSDialInConferencingDtmfConfiguration** per le impostazioni globali, il tasto di disattivazione/riattivazione del microfono sarà reimpostato sul valore predefinito 6.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsDialInConferencingDtmfConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialInConferencingDtmfConfiguration"}

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
<td><p>Identificatore univoco della raccolta di impostazioni DTMF da rimuovere. Per &quot;rimuovere&quot; le impostazioni globali, utilizzare la sintassi: -Identity global. Come menzionato in precedenza, in realtà non è possibile rimuovere le impostazioni; è possibile solo ripristinare le proprietà sui valori predefiniti. Per rimuovere una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration. Il cmdlet **Remove-CsDialInConferencingDtmfConfiguration** accetta le istanze dell'oggetto configurazione DTMF delle conferenze telefoniche con accesso esterno inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CSDialInConferencingDtmfConfiguration** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingDtmfConfiguration](get-csdialinconferencingdtmfconfiguration.md)  
[New-CsDialInConferencingDtmfConfiguration](new-csdialinconferencingdtmfconfiguration.md)  
[Set-CsDialInConferencingDtmfConfiguration](set-csdialinconferencingdtmfconfiguration.md)

