---
title: Set-CsConferencingPolicy
TOCTitle: Set-CsConferencingPolicy
ms:assetid: 2ddcf4ea-ae6c-40fa-9499-4e3b1b140e68
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425788(v=OCS.15)
ms:contentKeyID: 49300043
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferencingPolicy

 

_**Ultima modifica dell'argomento:** 2015-04-21_

Modifica un criterio conferenza esistente. I criteri conferenza determinano le funzionalità e le caratteristiche che è possibile utilizzare in una conferenza, ad esempio se includere o meno nella conferenza le funzionalità audio e video IP e il numero massimo di persone che possono partecipare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsConferencingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferencingPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AllowAnnotations <$true | $false>] [-AllowAnonymousParticipantsInMeetings <$true | $false>] [-AllowAnonymousUsersToDialOut <$true | $false>] [-AllowConferenceRecording <$true | $false>] [-AllowExternalUserControl <$true | $false>] [-AllowExternalUsersToRecordMeeting <$true | $false>] [-AllowExternalUsersToSaveContent <$true | $false>] [-AllowIPAudio <$true | $false>] [-AllowIPVideo <$true | $false>] [-AllowLargeMeetings <$true | $false>] [-AllowMultiView <$true | $false>] [-AllowNonEnterpriseVoiceUsersToDialOut <$true | $false>] [-AllowOfficeContent <$true | $false>] [-AllowParticipantControl <$true | $false>] [-AllowPolls <$true | $false>] [-AllowQandA <$true | $false>] [-AllowSharedNotes <$true | $false>] [-AllowUserToScheduleMeetingsWithAppSharing <$true | $false>] [-AppSharingBitRateKb <Int64>] [-AudioBitRateKb <UInt32>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisablePowerPointAnnotations <$true | $false>] [-EnableAppDesktopSharing <None | SingleApplication | Desktop>] [-EnableDataCollaboration <$true | $false>] [-EnableDialInConferencing <$true | $false>] [-EnableFileTransfer <$true | $false>] [-EnableMultiViewJoin <$true | $false>] [-EnableOnlineMeetingPromptForLyncResources <$true | $false>] [-EnableP2PFileTransfer <$true | $false>] [-EnableP2PRecording <$true | $false>] [-EnableP2PVideo <$true | $false>] [-FileTransferBitRateKb <Int64>] [-Force <SwitchParameter>] [-MaxMeetingSize <UInt32>] [-MaxVideoConferenceResolution <CIF | VGA>] [-TotalReceiveVideoBitRateKb <Int64>] [-VideoBitRateKb <Int64>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 modifica il valore di una proprietà del criterio di conferenza SalesConferencingPolicy. In particolare, il comando imposta il valore della proprietà AllowConferenceRecording su False. A tale scopo, viene chiamato il cmdlet **Set-CsConferencingPolicy** con il parametro Identity e il parametro AllowConferenceRecording.

    Set-CsConferencingPolicy -Identity SalesConferencingPolicy -AllowConferenceRecording $False

## ESEMPIO 2

Nell'esempio 2 i valori delle stesse due proprietà, AllowAnonymousParticipantsInMeetings e EnableDialInConferencing, vengono modificati per tutti i criteri di conferenza configurati per l'utilizzo nell'organizzazione. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsConferencingPolicy** per restituire una raccolta di tutti i criteri di conferenza disponibili. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsConferencingPolicy**, che imposta il valore di entrambe le proprietà AllowAnonymousParticipantsInMeetings e EnableDialInConferencing su False per ogni criterio della raccolta.

    Get-CsConferencingPolicy | Set-CsConferencingPolicy -AllowAnonymousParticipantsInMeetings $False -EnableDialInConferencing $False

## ESEMPIO 3

Il comando riportato nell'esempio 3 modifica la proprietà MaxVideoConferenceResolution di tutti i criteri di conferenza configurati nell'ambito del sito. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsConferencingPolicy** e il parametro Filter. Il valore di filtro "site:\*" restituisce solo i dati relativi ai criteri configurati nell'ambito del sito. Questa raccolta filtrata viene inviata tramite pipe al cmdlet **Set-CsConferencingPolicy**, che imposta su "CIF" la proprietà MaxVideoConferenceResolution di ogni criterio della raccolta.

    Get-CsConferencingPolicy -Filter "site:*" | Set-CsConferencingPolicy  -MaxVideoConferenceResolution CIF

## ESEMPIO 4

Nell'esempio 4 vengono recuperati tutti i criteri in cui la dimensione massima della riunione è maggiore di (-gt) 100 e quindi viene impostato su 100 il valore della proprietà associata (MaxMeetingSize). A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsConferencingPolicy** per restituire una raccolta di tutti i criteri di conferenza configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri per cui la proprietà MaxMeetingSize è maggiore di 100. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsConferencingPolicy**, che imposta su 100 la proprietà MaxMeetingSize di ogni criterio della raccolta.

    Get-CsConferencingPolicy | Where-Object {$_.MaxMeetingSize -gt 100} | Set-CsConferencingPolicy -MaxMeetingSize 100 

## Descrizione dettagliata

Le conferenze rappresentano un aspetto importante di Lync Server: le conferenze consentono ai gruppi di utenti di incontrarsi online per visualizzare diapositive e video, condividere applicazioni, scambiare file, comunicare e collaborare in altro modo.

È importante per gli amministratori mantenere il controllo delle conferenze e delle loro impostazioni. In alcuni casi potrebbero verificarsi problemi di protezione: per impostazione predefinita, tutti gli utenti, inclusi quelli non autenticati, possono partecipare alle riunioni e salvare le diapositive o gli stampati distribuiti durante le riunioni stesse. In altri casi potrebbero verificarsi problemi di larghezza di banda: in presenza di molte riunioni simultanee, in ciascuna delle quali sono coinvolti centinaia di partecipanti con trasmissioni video e condivisioni di file, potrebbero verificarsi problemi nella rete. Inoltre, potrebbero verificarsi problemi legali di natura occasionale. Ad esempio, per impostazione predefinita ai partecipanti alla riunione è consentito creare delle annotazioni sul contenuto condiviso, tuttavia queste annotazioni non vengono salvate quando la riunione viene archiviata. Se l'organizzazione è tenuta a conservare un record di tutte le comunicazioni elettroniche, è possibile disabilitare le annotazioni.

Esiste naturalmente una differenza tra la teoria della gestione delle impostazioni delle conferenze e l'effettiva gestione di queste impostazioni. In Lync Server le conferenze vengono gestite con specifici criteri. Nelle precedenti versioni del software questi criteri sono conosciuti come criteri riunione. Come già detto, i criteri conferenza consentono di stabilire le funzionalità e le caratteristiche che è possibile utilizzare in una conferenza, ad esempio se includere o meno nella riunione audio e video IP o il numero massimo di persone che possono partecipare. I criteri conferenza possono essere configurati nell'ambito globale, del sito o per utente. In questo modo gli amministratori possono stabilire quali funzionalità rendere disponibili per ogni utente.

Le proprietà del criterio possono essere configurate nel momento in cui si crea un criterio. Oltre a ciò, è possibile, in qualsiasi momento, usare il cmdlet **Set-CsConferencingPolicy** per modificare le proprietà di un criterio.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsConferencingPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferencingPolicy"}

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
<td><p><em>AllowAnnotations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se ai partecipanti è consentito creare delle annotazioni su schermo nei contenuti condivisi durante la riunione. Questa impostazione determina inoltre se l'uso della lavagna è consentito nella conferenza. Il valore predefinito è True.</p>
<p>Le annotazioni non vengono archiviate insieme agli altri contenuti della riunione.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio includerà annotazioni. L'utente può tuttavia partecipare ad altre conferenze in cui le annotazioni sono consentite.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowAnonymousParticipantsInMeetings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti anonimi è consentito partecipare alla riunione. Se impostato su False, solo agli utenti autenticati (ovvero gli utenti che hanno eseguito l'accesso a Servizi di dominio Active Directory o ad Active Directory di un partner federato) è consentito partecipare alla riunione. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio ammetterà partecipanti anonimi. L'utente può tuttavia partecipare ad altre conferenze in cui i partecipanti anonimi sono ammessi.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowAnonymousUsersToDialOut</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti anonimi (ad esempio, gli utenti non autenticati) sono autorizzati ad accedere a una conferenza utilizzando la funzionalità telefonica per connessione remota. Con la funzionalità telefonica per connessione remota, il server di conferenza chiama l'utente; quando risponde al telefono, l'utente accede automaticamente alla conferenza.</p>
<p>Notare che la conferenza telefonica con accesso esterno è consentita anche quando questa impostazione è False.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se il parametro è impostato su False, in nessuna delle conferenze create da un utente al quale si applica questo criterio verrà permesso ai partecipanti anonimi partecipare alla conferenza tramite chiamata esterna. L'utente può partecipare ad altre conferenze nelle quali ai partecipanti anonimi è consentito partecipare tramite chiamata esterna.</p>
<p>Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>AllowConferenceRecording</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti è consentito registrare la riunione. Il valore predefinito è False.</p>
<p>Questa impostazione riguarda tutti gli utenti che prendono parte alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExternalUserControl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti esterni (anonimi o federati) sono autorizzati a prendere il controllo delle applicazioni o dei desktop condivisi. Il valore predefinito è False.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti sia per le conferenze che per le sessioni di comunicazione peer-to-peer. Di conseguenza, ad alcuni utenti di una sessione può essere consentito di assegnare il controllo di un'applicazione o del desktop condivisi a un utente esterno, mentre ad altri utenti ciò può essere impedito.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowExternalUsersToRecordMeeting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti esterni (ovvero gli utenti anonimi o federati) è consentito registrare la riunione. Il valore predefinito è False.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà agli utenti esterni di registrare le conferenze. L'utente può tuttavia partecipare ad altre conferenze in cui agli utenti esterni è consentito registrare le conferenze.</p>
<p>Questa impostazione è effettiva solo se la proprietà AllowConferenceRecording è impostata su True.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExternalUsersToSaveContent</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti esterni (ovvero gli utenti che attualmente non hanno effettuato l'accesso alla rete) è consentito salvare stampati, diapositive ed altri contenuti della riunione. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà agli utenti esterni di salvare il contenuto. L'utente può tuttavia partecipare ad altre conferenze in cui agli utenti esterni è consentito salvare il contenuto.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowIPAudio</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se nella riunione è consentito l'uso dell'audio del computer. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio ammetterà l'audio IP. L'utente può tuttavia partecipare ad altre conferenze in cui l'audio IP è ammesso.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowIPVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se nella riunione è consentito l'uso del video del computer. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio ammetterà il video IP. L'utente può tuttavia partecipare ad altre conferenze in cui il video IP è ammesso.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowLargeMeetings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True, tutte le riunioni online vengono trattate come &quot;grandi riunioni&quot;. Con una grande riunione, vi sono limitazioni sul numero di notifiche inviate ai partecipanti, nonché sulle dimensioni dell'elenco dei partecipanti trasmesso per impostazione predefinita.</p>
<p>Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowMultiView</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True (valore predefinito) consente agli utenti di pianificare conferenze che consentono multiview, ossia i client possono ricevere più flussi video durante una data conferenza. Questa impostazione si applica all'utente che organizza la conferenza: se è impostato su False, nessuna conferenza creata da un utente interessato da questi criteri può includere multiview. L'utente può, tuttavia, partecipare ad altre conferenze dove è consentito multiview.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowNonEnterpriseVoiceUsersToDialOut</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti che non sono stati abilitati per VoIP aziendale è consentito partecipare a una conferenza tramite chiamata telefonica esterna. Con la chiamata telefonica esterna, il server per conferenze chiama telefonicamente l'utente. Quando l'utente risponde al telefono, viene aggiunto alla conferenza.</p>
<p>Notare che la conferenza telefonica con accesso esterno è consentita anche quando questa impostazione è False.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se è impostato su False, nessuna conferenza creata da un utente interessato da questi criteri consentirà la partecipazione degli utenti non abilitati per VoIP tramite chiamata telefonica esterna. Tuttavia, l'utente può partecipare ad altre conferenze dove gli utenti non abilitati per VoIP aziendale possono partecipare tramite chiamata esterna.</p>
<p>Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowOfficeContent</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su False, impedisce agli utenti di utilizzare contenuti di Office nelle conferenze.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowParticipantControl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i partecipanti alla riunione sono autorizzati a prendere il controllo delle applicazioni o dei desktop condivisi durante la riunione. Il valore predefinito è True.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui sono applicati questi criteri consentirà il controllo da parte dei partecipanti. L'utente può tuttavia partecipare ad altre conferenze in cui il controllo è consentito.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowPolls</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti è consentito gestire polling online durante una riunione. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà il polling. L'utente può tuttavia partecipare ad altre conferenze in cui il polling è consentito.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowQandA</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), l'utente potrà includere la funzionalità di gestione di domande e risposte in qualsiasi conferenza online che organizza. Se impostato su False, all'utente verrà impedito di includere questa funzionalità nelle conferenze.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se impostato su False, nessuna conferenza creata da un utente a cui sono applicati questi criteri consentirà l'utilizzo della funzionalità di gestione di domande e risposte. Tuttavia, l'utente può utilizzare questa funzionalità in altre conferenze in cui sono consentiti i sondaggi.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowSharedNotes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True (valore predefinito) qualsiasi computer notebook OneNote aperto collegato alla conferenza verrà automaticamente aggiornato con informazioni come partecipanti e dettagli sul contenuto condiviso durante la conferenza.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowUserToScheduleMeetingsWithAppSharing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti è consentito organizzare riunioni con condivisione delle applicazioni. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà la condivisione dell'applicazione. L'utente può tuttavia partecipare ad altre conferenze in cui la condivisione dell'applicazione è consentita.</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>La velocità in bit (in kilobit) utilizzata per la condivisione delle applicazioni. Il valore predefinito è 50000.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La velocità in bit (in kilobit) utilizzata per le trasmissioni audio. La velocità in bit dell'audio può corrispondere a qualsiasi numero intero compreso tra 20 e 200. Il valore predefinito è 200.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti sia per le conferenze che per le sessioni di comunicazione peer-to-peer.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo esplicativo sul criterio della conferenza. Ad esempio, nella descrizione potrebbero essere indicati gli utenti ai quali deve essere assegnato il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisablePowerPointAnnotations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True ($True), gli utenti non potranno aggiungere note alle diapositive di PowerPoint utilizzate in una conferenza. Tuttavia, a seconda del valore della proprietà AllowAnnotations, gli utenti avranno comunque accesso ad altre funzionalità di lavagna. Il valore predefinito è False che significa che le note di PowerPoint sono consentite.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableAppDesktopSharing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.EnableAppDesktopSharing</p></td>
<td><p>Indica se i partecipanti sono autorizzati a condividere le applicazioni (o il desktop) nel corso di una riunione. I valori consentiti sono:</p>
<p>Desktop. Agli utenti è consentito condividere il desktop.</p>
<p>SingleApplication. Agli utenti è consentito condividere una singola applicazione.</p>
<p>None. Agli utenti non è consentito condividere le applicazioni o il desktop.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti. Di conseguenza, ad alcuni utenti di una conferenza può essere consentito di condividere il desktop o le applicazioni, mentre ad altri utenti della stessa conferenza ciò può essere impedito.</p>
<p>Il valore predefinito è Desktop.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDataCollaboration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti possono organizzare le riunioni con attività di collaborazione dati, quali lavagna e annotazioni.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà la collaborazione dati. L'utente può tuttavia partecipare ad altre conferenze in cui la collaborazione dati è consentita.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDialInConferencing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti sono in grado di accedere alla riunione eseguendo un accesso esterno con un telefono PSTN (Public Switched Telephone Network). Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà le conferenze telefoniche con accesso esterno. L'utente può tuttavia partecipare ad altre conferenze in cui le conferenze telefoniche con accesso esterno sono consentite.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFileTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se durante la riunione sono consentiti i trasferimenti di file a tutti i partecipanti. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà i trasferimenti di file. L'utente può tuttavia partecipare ad altre conferenze in cui i trasferimenti di file sono consentiti.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMultiViewJoin</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True (valore predefinito) i client tenteranno di partecipare a una conferenza utilizzando multiview (che consente al client di ricevere più flussi video durante la conferenza). Questo parametro verrà ignorato se multiview non è consentito nella conferenza a cui si intende partecipare. Questa impostazione è applicata a livello per utente e sia per le conferenze che per le sessioni di comunicazione peer-to-peer. Pertanto, ad alcuni utenti di una sessione potrebbe essere consentito l'utilizzo di più flussi video mentre ad altri utenti della stessa conferenza no.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineMeetingPromptForLyncResources</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, ogni volta che gli utenti pianificano una riunione in Outlook che include invitati, ad esempio una sala riunioni, vengono avvisati che sarebbe più vantaggioso tenere la riunione online. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableP2PFileTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se nel corso della riunione sono autorizzati i trasferimenti file peer-to-peer (vale a dire, trasferimenti file che non coinvolgono tutti i partecipanti). Il valore predefinito è True ($True).</p>
<p>Questa impostazione è applicata a livello dei singoli utenti. Di conseguenza, ad alcuni utenti di una sessione di comunicazione peer-to-peer può essere consentito di trasferire file, mentre ad altri utenti ciò può essere impedito.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableP2PRecording</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se True, gli utenti saranno in grado di registrare sessioni di conferenze peer-to-peer. Il valore predefinito è False.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti. Di conseguenza, ad alcuni utenti di una sessione di comunicazione peer-to-peer può essere consentito di registrare la sessione, mentre ad altri utenti ciò può essere impedito.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableP2PVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se True, gli utenti saranno in grado di partecipare a sessioni di conferenze peer-to-peer. Il valore predefinito è False.</p>
<p>Questa impostazione viene applicata livello di singolo utente. Ciò significa che a un utente di una sessione di comunicazione peer-to-peer potrebbe essere consentito utilizzare il video mentre a un altro utente potrebbe non essere consentito.</p></td>
</tr>
<tr class="odd">
<td><p><em>FileTransferBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>La velocità in bit (in kilobit) utilizzata per i trasferimenti di file. Il valore predefinito è 50000.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio di conferenza da modificare. È possibile configurare i criteri relativi alle conferenze nell'ambito globale, del sito o per utente. Per modificare il criterio globale, utilizzare la seguente sintassi: -Identity global. Per modificare un criterio di sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per modificare un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity SalesConferencingPolicy.</p>
<p>Si noti che non è consentito utilizzare caratteri jolly per specificare un'identità. Se non si specifica un'identità, il cmdlet <strong>Set-CsConferencingPolicy</strong> modificherà automaticamente il criterio di conferenza globale.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Criterio riunione</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxMeetingSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero massimo di persone che possono partecipare a una riunione. Una volta raggiunto il numero massimo di partecipanti, gli altri utenti che tentano di partecipare alla riunione vengono avvisati che la riunione è completa. Il numero di partecipanti specificato in questo valore può essere qualsiasi numero intero a 32 bit (qualsiasi valore compreso tra 1 e 4.294.967.295), ma è consigliabile scegliere un valore compreso tra 2 e 250. Il valore predefinito è 250.</p>
<div class="alert">

> [!NOTE]
> 250 è il valore massimo per distribuzioni con pool condivisi, in base ai test Microsoft. Per informazioni sul supporto di riunioni con più di 250 partecipanti, vedere "Supporto di Microsoft Lync Server 2010 per riunioni estese" all'indirizzo <A href="http://go.microsoft.com/fwlink/?linkid=242073">http://go.microsoft.com/fwlink/?linkID=242073</A>.


</div>
<p>Questa impostazione si applica all'utente che organizza la conferenza. Nessuna conferenza creata da un utente a cui è applicato questo criterio ammetterà un numero di partecipanti superiore al valore specificato. L'utente può tuttavia partecipare ad altre conferenze in cui sono ammessi più partecipanti.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxVideoConferenceResolution</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MaxVideoConferenceResolution</p></td>
<td><p>Indica la risoluzione massima per il video della riunione. I valori consentiti sono:</p>
<p>CIF. CIF (Common Intermediate Format) ha una risoluzione di 352 pixel per 288 pixel.</p>
<p>VGA. VGA ha una risoluzione di 640 pixel per 480 pixel.</p>
<p>Il valore predefinito è VGA.</p></td>
</tr>
<tr class="odd">
<td><p><em>TotalReceiveVideoBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Indica la massima velocità in bit (in kilobit al secondo) consentita per tutti i video utilizzati in una conferenza, ovvero il totale combinato di tutti i flussi video. Il valore predefinito è 50000 kilobit al secondo.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Velocità in bit (in kilobit) utilizzata per le trasmissioni video. Il valore predefinito è 50000.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti sia per le conferenze che per le sessioni di comunicazione peer-to-peer.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy. Il cmdlet **Set-CsConferencingPolicy** accetta istanze dell'oggetto criterio riunione inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsConferencingPolicy** non restituisce oggetti o valori. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Remove-CsConferencingPolicy](remove-csconferencingpolicy.md)

