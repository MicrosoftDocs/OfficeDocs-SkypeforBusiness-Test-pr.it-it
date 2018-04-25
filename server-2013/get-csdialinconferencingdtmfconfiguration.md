---
title: Get-CsDialInConferencingDtmfConfiguration
TOCTitle: Get-CsDialInConferencingDtmfConfiguration
ms:assetid: 764741e4-c1cb-4627-8774-95cf08f6cf98
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398578(v=OCS.15)
ms:contentKeyID: 49301016
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingDtmfConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le impostazioni della segnalazione DTMF (Dual Tone Multi-Frequency) per le conferenze telefoniche con accesso esterno. La tecnologia DTMF consente agli utenti che accedono dall'esterno a una conferenza di controllarne le impostazioni, ad esempio disattivare o riattivare il proprio audio oppure bloccare e sbloccare la conferenza, mediante la tastiera del telefono. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDialInConferencingDtmfConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialInConferencingDtmfConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce le impostazioni DTMF per il sito Redmond.

    Get-CsDialInConferencingDtmfConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 viene restituita una raccolta di tutte le impostazioni DTMF, quindi per ogni elemento della raccolta viene visualizzato il valore del tasto da premere al fine di riprodurre in privato una descrizione dei comandi DTMF. A tale scopo, viene chiamato il cmdlet **Get-CsDialInConferencingDtmfConfiguration** affinché restituisca una raccolta di tutti i valori delle proprietà di tutte le impostazioni DTMF attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che seleziona due proprietà (Identity ed HelpCommand) da visualizzare sullo schermo.

    Get-CsDialInConferencingDtmfConfiguration | Select-Object Identity, HelpCommand

## ESEMPIO 3

Il comando mostrato nell'esempio 3 restituisce tutte le impostazioni DTMF configurate nell'ambito del sito. Questa operazione viene eseguita includendo il parametro Filter e il valore del filtro "site:\*". Questo valore filtro limita i dati restituiti alle impostazioni la cui identità inizia con i caratteri "site:". Per definizione, tali impostazioni sono configurate nell'ambito del sito.

    Get-CsDialInConferencingDtmfConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le impostazioni di configurazione DTMF in cui la proprietà AdmitAll è diversa da 8 (valore predefinito). A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsDialInConferencingDtmfConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni DTMF attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà AdmitAll non è uguale a 8.

    Get-CsDialInConferencingDtmfConfiguration | Where-Object {$_.AdmitAll -ne 8}

## Descrizione dettagliata

Lync Server consente agli utenti di partecipare alle conferenze accedendo dall'esterno tramite telefono. Gli utenti con accesso esterno non possono visualizzare video né scambiare messaggi istantanei con gli altri partecipanti alla conferenza, ma possono partecipare completamente alla parte audio della riunione.

Oltre alla possibilità di partecipare a una conferenza, gli utenti possono inoltre gestire parti selezionate della conferenza mediante la tastiera del telefono. La gestione delle specifiche impostazioni della conferenza varia a seconda che l'utente sia o meno un relatore. Ad esempio, per impostazione predefinita, gli utenti possono premere il tasto 6 della tastiera per disattivare o riattivare il proprio audio. I partecipanti possono riprodurre in privato i nomi di tutti gli altri partecipanti alla riunione, mentre i relatori, ad esempio, possono disattivare e riattivare l'audio di tutti i partecipanti alla riunione e abilitare o disabilitare l'annuncio riprodotto ogni volta che qualcuno accede a una conferenza o abbandona la conferenza.

La possibilità di effettuare selezioni mediante la tastiera del telefono è nota come segnalazione DTMF: quando si compone un numero di telefono e la voce registrata chiede di "premere 1 per l'inglese o 2 per l'italiano", questo è un esempio di segnalazione DTMF. Il cmdlet **Get-CsDialInConferencingDtmfConfiguration** consente di recuperare un elenco di tutti i comandi DTMF disponibili, nonché i tasti utilizzati per eseguire tali comandi.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsDialInConferencingDtmfConfiguration** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingDtmfConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare caratteri jolly al fine di restituire una raccolta, o più raccolte, delle impostazioni di configurazione DTMF. Per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi seguente: -Filter site:*. Per restituire una raccolta di tutte le impostazioni che contengono il valore stringa &quot;EMEA&quot; in Identity (l'unica proprietà su cui è possibile applicare il filtro), utilizzare la sintassi riportata di seguito: -Filter *EMEA*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco per l'insieme di impostazioni DTMF da restituire. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity. Tuttavia, se è necessario utilizzare caratteri jolly, utilizzare il parametro Filter.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsDialInConferencingDtmfConfiguration</strong> restituisce una raccolta di tutte le impostazioni di configurazione DTMF in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione DTMF dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDialInConferencingDtmfConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsDialInConferencingDtmfConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingDtmfConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsDialInConferencingDtmfConfiguration](new-csdialinconferencingdtmfconfiguration.md)  
[Remove-CsDialInConferencingDtmfConfiguration](remove-csdialinconferencingdtmfconfiguration.md)  
[Set-CsDialInConferencingDtmfConfiguration](set-csdialinconferencingdtmfconfiguration.md)

