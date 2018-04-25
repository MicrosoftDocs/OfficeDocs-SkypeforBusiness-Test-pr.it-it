---
title: New-CsMeetingConfiguration
TOCTitle: New-CsMeetingConfiguration
ms:assetid: 0043c9e7-83c6-4f07-88d2-7018c65c1654
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398065(v=OCS.15)
ms:contentKeyID: 49299477
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMeetingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione delle riunioni nell'ambito del sito o del servizio. Le impostazioni di configurazione delle riunioni consentono di stabilire il tipo di riunioni (denominate anche "conferenze") che gli utenti possono creare e di controllare come (o anche se) utenti anonimi e utenti che utilizzano conferenze telefoniche con accesso esterno possono partecipare a queste riunioni. Si noti che queste impostazioni hanno effetto solo sulle riunioni pianificate e non sulle riunioni ad hoc create facendo clic sull'opzione Riunione immediata in Lync. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsMeetingConfiguration -Identity <XdsIdentity> [-AdmitAnonymousUsersByDefault <$true | $false>] [-AssignedConferenceTypeByDefault <$true | $false>] [-Confirm [<SwitchParameter>]] [-CustomFooterText <String>] [-DesignateAsPresenter <None | Company | Everyone>] [-EnableAssignedConferenceType <$true | $false>] [-Force <SwitchParameter>] [-HelpURL <String>] [-InMemory <SwitchParameter>] [-LegalURL <String>] [-LogoURL <String>] [-PstnCallersBypassLobby <$true | $false>] [-RequireRoomSystemsAuthorization <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione delle riunioni per il sito Redmond (-Identity site:Redmond). Oltre a specificare l'identità (Identity), in questo comando sono inclusi tre parametri facoltativi: EnableAssignedConferenceType, AssignedConferenceTypeByDefault e AdmitAnonymousUsersByDefault. In tutti e tre i casi i parametri sono impostati su False. Ciò significa che saranno disabilitati i tipi di riunione pubblica, che il tipo di riunione predefinito non sarà impostato sulla riunione pubblica e che per impostazione predefinita non sarà consentito agli utenti anonimi di partecipare alle riunioni.

Si noti che questo comando avrà esito negativo se esiste già una raccolta di impostazioni di configurazione delle riunioni con Identity site:Redmond. Infatti, a un determinato sito può essere assegnata una sola raccolta di impostazioni di configurazione delle riunioni.

    New-CsMeetingConfiguration -Identity site:Redmond -EnableAssignedConferenceType $False -AssignedConferenceTypeByDefault $False -AdmitAnonymousUsersByDefault $False

## ESEMPIO 2

Nell'esempio 2 viene illustrato un metodo alternativo per creare una nuova raccolta di impostazioni di configurazione delle riunioni per il sito Redmond. In questo caso, le impostazioni vengono inizialmente create in memoria e solo in seguito applicate al sito. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsMeetingConfiguration** per creare le nuove impostazioni delle riunioni per il sito Redmond. Il parametro InMemory viene aggiunto alla fine del comando per fare in modo che queste nuove impostazioni vengano create solo in memoria e non vengano immediatamente applicate al sito Redmond. Dal momento che queste impostazioni esistono solo in memoria, devono essere archiviate in una variabile. In questo esempio, vengono archiviate in una variabile denominata $x.

Dopo la creazione di queste impostazioni virtuali delle riunioni, vengono utilizzati i comandi 2, 3 e 4 per modificare diverse proprietà di tali impostazioni (EnableAssignedConferenceType, AssignedConferenceTypeByDefault e AdmitAnonymousUsersByDefault). Nell'ultimo comando viene utilizzato il cmdlet **Set-CsMeetingConfiguration** insieme al parametro Instance per applicare effettivamente le impostazioni virtuali al sito Redmond. Si noti che questo passaggio finale è fondamentale. Se non si chiama il cmdlet **Set-CsMeetingConfiguration**, le nuove impostazioni di configurazione delle riunioni non verranno mai applicate al sito Redmond. Le impostazioni virtuali verranno invece eliminate non appena si termina la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsMeetingConfiguration -Identity site:Redmond -InMemory
    $x.EnableAssignedConferenceType = $False 
    $x.AssignedConferenceTypeByDefault = $False 
    $x.AdmitAnonymousUsersByDefault = $False
    Set-CsMeetingConfiguration -Instance $x

## Descrizione dettagliata

Le riunioni (denominate anche "conferenze") sono parte integrante di Lync Server. I cmdlet **CsMeetingConfiguration** consentono agli amministratori di controllare il tipo di riunioni che gli utenti possono creare e di stabilire la modalità di partecipazione alle riunioni da parte di utenti anonimi e utenti che utilizzano conferenze telefoniche con accesso esterno. È ad esempio possibile configurare le riunioni in modo che chiunque acceda tramite PSTN (Public Switched Telephone Network) venga automaticamente ammesso alla riunione. In alternativa, è possibile configurare le riunioni in modo che gli utenti che utilizzano conferenze telefoniche con accesso esterno non siano automaticamente ammessi alla riunione, ma vengano instradati alla sala d'attesa. Questi utenti restano in attesa finché un relatore non concede loro l'accesso alla riunione.

Come specificato in precedenza, queste impostazioni hanno effetto solo sulle riunioni pianificate e non sulle riunioni ad hoc create facendo clic sull'opzione Riunione immediata in Microsoft Lync. Quando si crea una riunione facendo clic su Riunione immediata, l'accesso come partecipante viene automaticamente consentito a tutti e gli utenti anonimi possono partecipare alla riunione senza dover attendere nella sala di attesa. Questo si verifica indipendentemente dalla configurazione delle impostazioni della riunione tramite i cmdlet CsMeetingConfiguration.

Il cmdlet **New-CsMeetingConfiguration** consente di creare nuove raccolte di impostazioni di configurazione delle riunioni nell'ambito del sito o del servizio (sebbene solo per il modulo Servizi utente). Le impostazioni delle riunioni non possono essere create nell'ambito globale perché esiste già una raccolta globale di impostazioni.

Si noti che ogni sito o servizio può avere al massimo una raccolta di impostazioni di configurazione delle riunioni. Se si tenta di creare nuove impostazioni per il sito Redmond e nel sito Redmond è già presente una raccolta di impostazioni di configurazione delle riunioni, il comando avrà esito negativo.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsMeetingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsMeetingConfiguration"}

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
<td><p>Identificatore univoco per la nuova raccolta di impostazioni di configurazione delle riunioni. Tali impostazioni possono essere create solo nell'ambito del sito o del servizio. Per creare nuove impostazioni nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per creare nuove impostazioni nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:UserServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Si noti che la chiamata al cmdlet <strong>New-CsMeetingConfiguration</strong> avrà esito negativo se il servizio o il sito specificato dispone già di una raccolta di impostazioni di configurazione delle riunioni.</p></td>
</tr>
<tr class="even">
<td><p><em>AdmitAnonymousUsersByDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di stabilire se verrà consentito, per impostazione predefinita, agli utenti anonimi (cioè, utenti non autenticati) di partecipare alle riunioni. Impostare questo valore su True se si desidera consentire, per impostazione predefinita, agli utenti anonimi di partecipare alle nuove riunioni. Impostare questo valore su False se invece si desidera non consentire, per impostazione predefinita, agli utenti anonimi di partecipare alle nuove riunioni. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>AssignedConferenceTypeByDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se le nuove riunioni saranno configurate, per impostazione predefinita, come riunioni pubbliche. Impostare questo valore su True per utilizzare le riunioni pubbliche come impostazione predefinita; impostare questo valore su False per utilizzare le riunioni private come impostazione predefinita. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomFooterText</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Testo da utilizzare negli inviti alle riunioni personalizzati.</p></td>
</tr>
<tr class="even">
<td><p><em>DesignateAsPresenter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.DesignateAsPresenter</p></td>
<td><p>Indica a quali utenti (oltre all'organizzazione della riunione) deve essere automaticamente assegnato il ruolo di relatore quando partecipano a una riunione. Le alternative valide sono: None, Company e Everyone. Per impostazione predefinita, il parametro DesignateAsPresenter è impostato su Company e ciò significa che chiunque nell'organizzazione dispone dei diritti di relatore a partire dal momento in cui accede alla riunione.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableAssignedConferenceType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti possono pianificare riunioni pubbliche. In una riunione pubblica, l'ID conferenza e il collegamento della riunione restano gli stessi ogni volta che si organizza la riunione. In una riunione privata, l'ID conferenza e il collegamento della riunione cambiano ogni volta.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL di un sito Web in cui gli utenti possono ottenere assistenza per partecipare alla riunione.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>LegalURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL di un sito Web contenente informazioni legati e dichiarazioni di non responsabilità per le riunioni.</p></td>
</tr>
<tr class="even">
<td><p><em>LogoURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL dell'immagine da utilizzare negli inviti alle riunioni personalizzati.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnCallersBypassLobby</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti connessi a una rete PSTN (Public Switched Telephone Network) devono essere ammessi automaticamente ad una riunione. Se impostato su True, i chiamanti che utilizzano la rete PSTN saranno ammessi automaticamente alla riunione. Se impostato su False, i chiamanti che utilizzano la rete PSTN verranno inizialmente reinstradati alla sala d'attesa della conferenza. Quindi, verranno messi in attesa finché un relatore della conferenza non concede loro l'accesso alla riunione. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireRoomSystemsAuthorization</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True ($True), tutti gli utenti dovranno essere autenticati prima di poter partecipare a una riunione utilizzando il sistema delle sale di Lync. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per cui vengono create le nuove impostazioni di configurazione delle riunioni. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
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

Nessuno. Il cmdlet **New-CsMeetingConfiguration** non accetta dati da pipeline.

## Tipi restituiti

Il cmdlet **New-CsMeetingConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)  
[Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md)  
[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

