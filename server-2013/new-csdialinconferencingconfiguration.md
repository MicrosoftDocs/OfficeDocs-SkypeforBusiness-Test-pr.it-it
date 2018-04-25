---
title: New-CsDialInConferencingConfiguration
TOCTitle: New-CsDialInConferencingConfiguration
ms:assetid: ac0b6e22-3883-4884-aa94-18f4029c7f1e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412816(v=OCS.15)
ms:contentKeyID: 49301645
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDialInConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione per le conferenze telefoniche con accesso esterno. Tali impostazioni determinano il modo in cui Lync Server risponde quando gli utenti accedono o abbandonano una conferenza telefonica con accesso esterno. In particolare, le informazioni restituite specificano se i partecipanti devono registrare o meno il proprio nome quando partecipano a una conferenza e in che modo il sistema annuncia eventualmente che qualcuno si è unito alla chiamata o l'ha abbandonata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDialInConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableNameRecording <$true | $false>] [-EntryExitAnnouncementsEnabledByDefault <$true | $false>] [-EntryExitAnnouncementsType <UseNames | ToneOnly>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione per le conferenze telefoniche con accesso esterno applicate al sito Redmond. Viene incluso inoltre il parametro facoltativo EnableNameRecording per impostare la proprietà EnableNameRecording su False.

    New-CSDialInConferencingConfiguration -Identity site:Redmond -EnableNameRecording $False

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il parametro InMemory per creare una nuova raccolta di impostazioni di configurazione per le conferenze telefoniche con accesso esterno inizialmente esistente solo in memoria. A tale scopo, nell'esempio viene chiamato innanzitutto il cmdlet **New-CSDialInConferencingConfiguration** con il parametro InMemory per creare una raccolta virtuale di impostazioni archiviata nella variabile $x. Alla raccolta viene assegnato come valore Identity site:Redmond. Dopo la creazione della raccolta virtuale, nella riga 2 viene modificato il valore della proprietà EnableNameRecording. Nella riga 3 dell'esempio infine viene chiamato il cmdlet **Set-CSDialInConferencingConfiguration** per trasformare le impostazioni di configurazione virtuali archiviate in $x in una raccolta effettiva di impostazioni applicate al sito Redmond.

    $x = New-CSDialInConferencingConfiguration -Identity site:Redmond -InMemory
    $x.EnableNameRecording = $False
    Set-CSDialInConferencingConfiguration -Instance $x

## Descrizione dettagliata

Quando gli utenti partecipano a una conferenza telefonica con accesso esterno o escono da essa, Lync Server può rispondere in diversi modi. È ad esempio possibile che ai partecipanti venga richiesto di registrare il proprio nome prima di accedere alla conferenza. Allo stesso modo, gli amministratori possono decidere se impostare un annuncio di Lync Server che segnala l'accesso o l'uscita dei partecipanti alla conferenza telefonica.

Questi comportamenti di accesso a una conferenza vengono gestiti utilizzando le impostazioni di configurazione per le conferenze telefoniche con accesso esterno. Queste impostazioni possono essere configurate nell'ambito globale o del sito. Le impostazioni configurate nell'ambito del sito hanno la precedenza su quelle configurate nell'ambito globale. Al momento dell'installazione di Lync Server, le uniche impostazioni di configurazione per le conferenze telefoniche con accesso esterno disponibili sono quelle dell'ambito globale. È tuttavia possibile creare nuove impostazioni nell'ambito del sito tramite il cmdlet **New-CSDialInConferencingConfiguration**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsDialInConferencingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDialInConferencingConfiguration"}

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
<td><p>XdsIdentity</p></td>
<td><p>Indica l'identità delle impostazioni di configurazione per le conferenze telefoniche con accesso esterno da creare. Dal momento che queste impostazioni possono essere create solo nell'ambito del sito, utilizzare una sintassi simile a quella riportata di seguito, con il prefisso &quot;site:&quot; seguito dal nome del sito: -Identity site:Redmond.</p>
<p>È possibile disporre di un solo insieme di impostazioni di configurazione per le conferenze telefoniche con accesso esterno per sito. Il comando di esempio avrà esito negativo se esiste già una raccolta di impostazioni con valore Identity site:Redmond.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableNameRecording</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Determina se richiedere agli utenti di registrare il proprio nome prima di accedere alla conferenza. Impostare True ($True) per richiedere la registrazione del nome oppure False ($False) per disabilitarla. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>EntryExitAnnouncementsEnabledByDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se il parametro viene impostato su True, verranno riprodotti annunci ogni volta che un partecipante si unisce a una conferenza o l'abbandona. Se invece viene impostato su False (valore predefinito), non verranno riprodotti annunci di ingresso e abbandono.</p></td>
</tr>
<tr class="odd">
<td><p><em>EntryExitAnnouncementsType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>EntryExitAnnouncementsType</p></td>
<td><p>Indica l'azione svolta dal sistema ogni volta che un partecipante si unisce a una conferenza o l'abbandona. I valori validi sono:</p>
<p>UseNames. Il nome della persona viene annunciato ogni volta che si unisce a una conferenza o l'abbandona, ad esempio &quot;Davide Garghentini sta abbandonando la conferenza&quot;.</p>
<p>ToneOnly. Ogni volta che un partecipante si unisce a una conferenza o l'abbandona, viene riprodotto un segnale acustico.</p>
<p>Il valore predefinito è UseNames. Gli annunci verranno riprodotti solo se la proprietà EntryExitAnnouncementsEnabledByDefault è impostata su True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsDialInConferencingConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingConfiguration](get-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

