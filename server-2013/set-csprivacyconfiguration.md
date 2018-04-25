---
title: Set-CsPrivacyConfiguration
TOCTitle: Set-CsPrivacyConfiguration
ms:assetid: 67fbd99a-0708-4e6f-8755-cb1a08d07ff3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398484(v=OCS.15)
ms:contentKeyID: 49300840
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPrivacyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un insieme esistente di impostazioni di configurazione della privacy. Le impostazioni di configurazione della privacy consentono di determinare quante informazioni gli utenti rendono disponibili agli altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsPrivacyConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPrivacyConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di modificare tre valori di proprietà delle impostazioni di configurazione della privacy con Identity site:Redmond. I tre valori di proprietà modificati sono AutoInitiateContacts, PublishLocationDataDefault e DisplayPublishedPhotoDefault.

    Set-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $False -AutoInitiateContacts $True -PublishLocationDataDefault $True -DisplayPublishedPhotoDefault $True

## ESEMPIO 2

Nell'esempio 2 viene abilitata la modalità privacy per tutte le impostazioni di configurazione della privacy attualmente in uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsPrivacyConfiguration** senza alcun parametro aggiuntivo. In questo modo viene restituita la raccolta completa delle impostazioni della privacy. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsPrivacyConfiguration**, che imposta la proprietà EnablePrivacyMode su True per ogni elemento della raccolta.

    Get-CsPrivacyConfiguration | Set-CsPrivacyConfiguration -EnablePrivacyMode $True

## ESEMPIO 3

Nell'esempio 3 vengono apportate modifiche a tutte le impostazioni di configurazione della privacy in cui attualmente non viene usata la modalità privacy. A tale scopo, viene usato prima di tutto il cmdlet **Get-CsPrivacyConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione della privacy. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnablePrivacyMode è uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsPrivacyConfiguration**, che assegna valori alle proprietà AutoInitiateContacts, PublishLocationDataDefault e DisplayPublishedPhotoDefault per ogni elemento nella raccolta.

    Get-CsPrivacyConfiguration | Where-Object {$_.EnablePrivacyMode -eq $False} | Set-CsPrivacyConfiguration -AutoInitiateContacts $True -PublishLocationDataDefault $True -DisplayPublishedPhotoDefault $True

## Descrizione dettagliata

Lync Server consente agli utenti di condividere con altre persone un'elevata quantità di informazioni sulla presenza, grazie alla possibilità di pubblicare foto personali, fornire informazioni dettagliate sulla posizione e rendere automaticamente disponibili le informazioni sulla presenza a chiunque nell'organizzazione e non solo alle persone presenti nell'elenco contatti personale.

Alcuni utenti accoglieranno questa possibilità di condividere le informazioni con i propri colleghi. Altri potrebbero essere invece più riluttanti a condividere questi dati. Ad esempio, molte persone potrebbero non essere entusiaste di avere una propria foto inclusa tra i dati sulla presenza. In generale, spetta agli utenti decidere cosa intendono o non intendono condividere. Ad esempio, gli utenti possono selezionare o deselezionare una casella di controllo per condividere o non condividere con altri le proprie informazioni sulla località. I cmdlet di configurazione della privacy inoltre consentono agli amministratori di gestire le impostazioni della privacy per i propri utenti. In alcuni casi, gli amministratori possono abilitare o disabilitare certe impostazioni. Se ad esempio la proprietà AutoInitiateContacts è impostata su True, i membri del team vengono automaticamente aggiunti all'elenco dei contatti di ogni utente. Se invece la proprietà è impostata su False, i membri del team non vengono automaticamente aggiunti all'elenco dei contatti di ogni utente.

In altri casi, gli amministratori possono configurare i valori predefiniti di Lync lasciando però agli utenti la possibilità di modificarli. Ad esempio, i dati sulla posizione vengono pubblicati per gli utenti per impostazione predefinita, nonostante gli utenti abbiano il diritto di disabilitare la pubblicazione della posizione. Impostando la proprietà PublishLocationDataByDefault su False, gli amministratori possono modificare questo comportamento: in tal caso, i dati sulla posizione non verranno pubblicati per impostazione predefinita, nonostante gli utenti abbiano comunque il diritto di pubblicare questi dati se lo desiderano.

Le impostazioni di configurazione della privacy possono essere applicate nell'ambito globale, nell'ambito del sito e nell'ambito del servizio (sebbene solo per il servizio Server utenti). Il cmdlet **Set-CsPrivacyConfiguration** consente di modificare qualunque impostazione di configurazione della privacy attualmente in uso nell'organizzazione.

Utenti autorizzati a usare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsPrivacyConfiguration** può essere usato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli Controllo degli accessi in base al ruolo a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli Controllo degli accessi in base al ruolo personalizzati), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPrivacyConfiguration"}

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
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, in Lync il manager e i dipendenti diretti vengono aggiunti automaticamente all'elenco contatti. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, la foto dell'utente verrà automaticamente pubblicata in Lync. Se impostato su False, la foto dell'utente non sarà disponibile, a meno che l'utente non selezioni esplicitamente l'opzione Consenti ad altri di vedere la mia foto. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, fornisce all'utente la possibilità di abilitare la modalità privacy avanzata. In modalità privacy avanzata, le informazioni sulla presenza saranno accessibili solo alle persone incluse nel proprio elenco dei contatti. Se impostato su False, le informazioni sulla presenza saranno accessibili a tutti coloro che fanno parte dell'organizzazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero essere generati durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione della privacy da modificare. Per modificare le impostazioni globali, usare la sintassi seguente: -Identity global. Per modificare le impostazioni configurate nell'ambito del sito, usare una sintassi simile alla seguente: -Identity site:Redmond. Per modificare le impostazioni a livello di servizio, usare una sintassi simile alla seguente: -Identity service:Redmond-UserServices-1. Si noti che le impostazioni della privacy possono essere applicate solo al servizio Server utenti. Se si tenta di applicare queste impostazioni a qualunque altro servizio, verrà generato un errore.</p>
<p>Se questo parametro non è specificato, quando si usa il cmdlet <strong>Set-CsPrivacyConfiguration</strong> vengono aggiornate le impostazioni globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto PrivacyConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i dati sulla posizione verranno automaticamente pubblicati in Lync Server. Se impostato su False, i dati sulla posizione non saranno disponibili, a meno che l'utente non selezioni esplicitamente l'opzione Mostra posizione personale a contatti. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per le impostazioni di configurazione della privacy da modificare, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in ambienti ibridi.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration. Il cmdlet **Set-CsPrivacyConfiguration** accetta input tramite pipeline dall'oggetto configurazione privacy.

## Tipi restituiti

Il cmdlet **Set-CsPrivacyConfiguration** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[New-CsPrivacyConfiguration](new-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)

