---
title: New-CsPrivacyConfiguration
TOCTitle: New-CsPrivacyConfiguration
ms:assetid: 9b7f02d7-93a5-4fa5-a74c-3fe4baf8bbfc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398807(v=OCS.15)
ms:contentKeyID: 49301462
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPrivacyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione della privacy. Tali impostazioni consentono di determinare quante informazioni gli utenti rendono disponibili per altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsPrivacyConfiguration -Identity <XdsIdentity> [-AutoInitiateContacts <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayPublishedPhotoDefault <$true | $false>] [-EnablePrivacyMode <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PublishLocationDataDefault <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare una nuova raccolta di impostazioni di configurazione della privacy e di applicarle al sito Redmond (-Identity site:Redmond). Le nuove impostazioni abilitano la modalità privacy, questo risultato è viene ottenuto aggiungendo il parametro EnablePrivacyMode ed impostando il valore del parametro su True. Si noti che questo comando avrà esito negativo se il sito Redmond possiede già una raccolta di impostazioni della privacy.

    New-CsPrivacyConfiguration -Identity site:Redmond -EnablePrivacyMode $True

## ESEMPIO 2

Nell'esempio 2 viene illustrato come utilizzare il parametro InMemory per creare una nuova raccolta di impostazioni di configurazione della privacy che inizialmente esistono solo in memoria. A tale scopo, viene chiamato il cmdlet **New-CsPrivacyConfiguration** con i parametri Identity e InMemory. L'oggetto risultante viene archiviato in una variabile denominata $x. A questo punto le impostazioni della privacy esistono solo in memoria. Se si esegue il cmdlet **Get-CsPrivacyConfiguration**, non sarà possibile visualizzare un elenco per site:Redmond.

Nel secondo comando il valore della proprietà EnablePrivacyMode è impostato su True. Infine, il terzo comando utilizza il cmdlet **Set-CsPrivacyConfiguration** per trasformare questa raccolta virtuale di impostazioni della privacy in una raccolta di impostazioni effettive applicate al sito Redmond. La chiamata al cmdlet **Set-CsPrivacyConfiguration** è fondamentale: se questo cmdlet non viene chiamato, le nuove impostazioni della privacy non verranno applicate al sito Redmond e scompariranno completamente quando si chiude la sessione di Windows PowerShell o quando si elimina la variabile $x.

    $x = New-CsPrivacyConfiguration -Identity site:Redmond -InMemory
    $x.EnablePrivacyMode = $True
    Set-CsPrivacyConfiguration -Instance $x

## Descrizione dettagliata

Lync Server offre agli utenti la possibilità di condividere con altre persone un'elevata quantità di informazioni sulla presenza. Possono infatti pubblicare una propria foto, fornire informazioni dettagliate sulla posizione in cui si trovano, rendere le informazioni sulla presenza automaticamente accessibili a tutti all'interno dell'organizzazione, invece che solo alle persone inserite nel proprio elenco contatti.

Alcuni utenti accoglieranno questa possibilità di condividere le informazioni con i propri colleghi. Altri potrebbero essere invece più riluttanti a condividere questi dati. Ad esempio, molte persone potrebbero non essere entusiaste di avere una propria foto inclusa tra i dati sulla presenza. In generale, spetta agli utenti decidere cosa intendono o non intendono condividere. Ad esempio, gli utenti possono selezionare o deselezionare una casella di controllo per condividere o non condividere con altri le proprie informazioni sulla località. I cmdlet di configurazione della privacy inoltre consentono agli amministratori di gestire le impostazioni della privacy per i propri utenti. In alcuni casi, gli amministratori possono abilitare o disabilitare certe impostazioni. Se ad esempio la proprietà AutoInitiateContacts è impostata su True, i membri del team vengono automaticamente aggiunti all'elenco dei contatti di ogni utente. Se invece la proprietà è impostata su False, i membri del team non vengono automaticamente aggiunti all'elenco dei contatti di ogni utente.

In altri casi, gli amministratori possono configurare i valori predefiniti in Lync concedendo però sempre agli utenti il diritto di modificare questi valori. Ad esempio, per impostazione predefinita, le informazioni sulla posizione degli utenti vengono pubblicate, anche se gli utenti mantengono comunque il diritto di bloccare la pubblicazione di queste informazioni. Impostando la proprietà PublishLocationDataByDefault su False, gli amministratori possono modificare questo comportamento. In tal caso, i dati sulla posizione non verranno pubblicati per impostazione predefinita, anche se gli utenti mantengono il diritto di pubblicarli, se lo desiderano.

Le impostazioni di configurazione della privacy possono essere applicate nell'ambito globale, nell'ambito del sito e nell'ambito del servizio (sebbene solo per il servizio User Server). Il cmdlet **New-CsPrivacyConfiguration** consente di creare nuove impostazioni di configurazione della privacy da applicare a un sito o a un servizio. Le nuove raccolte non possono essere create in ambito globale. Si noti che ogni sito o servizio può avere al massimo un'unica raccolta di impostazioni di configurazione della privacy. Se si tenta di creare una nuova raccolta per il sito Redmond e questo sito ospita già una raccolta di impostazioni di configurazione della privacy, il comando avrà esito negativo.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsPrivacyConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPrivacyConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione della privacy da creare. Per creare nuove raccolte di impostazioni nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per creare nuove impostazioni nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity service:UserServer:atl-cs-001.litwareinc.com. Le impostazioni della privacy possono essere create solo per il servizio User Server. Se si tenta di applicare queste impostazioni a qualunque altro servizio, verrà generato un errore.</p>
<p>Si noti che il comando avrà esito negativo se le impostazioni di configurazione della privacy esistono già per il sito o servizio specificato. Similmente, il comando avrà esito negativo se si tenta di creare una nuova raccolta di impostazioni globali.</p></td>
</tr>
<tr class="even">
<td><p><em>AutoInitiateContacts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, in Lync il proprio responsabile e i propri subalterni vengono aggiunti automaticamente all'elenco contatti. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayPublishedPhotoDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, la foto dell'utente verrà automaticamente pubblicata in Lync. Se impostato su False, la foto dell'utente non sarà disponibile, a meno che l'utente non selezioni esplicitamente l'opzione Consenti ad altri di vedere la mia foto. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePrivacyMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, fornisce all'utente la possibilità di abilitare la modalità privacy avanzata. In modalità privacy avanzata, le informazioni sulla presenza saranno accessibili solo alle persone incluse nel proprio elenco dei contatti. Se impostato su False, le informazioni sulla presenza saranno accessibili a tutti coloro che fanno parte dell'organizzazione. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>PublishLocationDataDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i dati sulla posizione verranno automaticamente pubblicati in Lync. Se impostato su False, i dati sulla posizione non saranno disponibili, a meno che l'utente non selezioni esplicitamente l'opzione Mostra posizione personale a contatti. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per cui vengono create nuove impostazioni di configurazione della privacy, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID tenant per ciascun tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Nessuno. Il cmdlet **New-CsPrivacyConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsPrivacyConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.PrivacyConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)  
[Remove-CsPrivacyConfiguration](remove-csprivacyconfiguration.md)  
[Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

