---
title: New-CsConferencingPolicy
TOCTitle: New-CsConferencingPolicy
ms:assetid: f343bfcc-f296-4935-aa4c-94658dacace7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413019(v=OCS.15)
ms:contentKeyID: 49302460
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferencingPolicy

 

_**Ultima modifica dell'argomento:** 2015-04-06_

Crea un nuovo criterio conferenza per l'utilizzo nell'organizzazione. I criteri conferenza determinano le funzionalità e le caratteristiche che è possibile utilizzare in una conferenza, ad esempio se includere o meno nella conferenza le funzionalità audio e video IP e il numero massimo di persone che possono partecipare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsConferencingPolicy -Identity <XdsIdentity> [-AllowAnnotations <$true | $false>] [-AllowAnonymousParticipantsInMeetings <$true | $false>] [-AllowAnonymousUsersToDialOut <$true | $false>] [-AllowConferenceRecording <$true | $false>] [-AllowExternalUserControl <$true | $false>] [-AllowExternalUsersToRecordMeeting <$true | $false>] [-AllowExternalUsersToSaveContent <$true | $false>] [-AllowIPAudio <$true | $false>] [-AllowIPVideo <$true | $false>] [-AllowLargeMeetings <$true | $false>] [-AllowMultiView <$true | $false>] [-AllowNonEnterpriseVoiceUsersToDialOut <$true | $false>] [-AllowOfficeContent <$true | $false>] [-AllowParticipantControl <$true | $false>] [-AllowPolls <$true | $false>] [-AllowQandA <$true | $false>] [-AllowSharedNotes <$true | $false>] [-AllowUserToScheduleMeetingsWithAppSharing <$true | $false>] [-AppSharingBitRateKb <Int64>] [-AudioBitRateKb <UInt32>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisablePowerPointAnnotations <$true | $false>] [-EnableAppDesktopSharing <None | SingleApplication | Desktop>] [-EnableDataCollaboration <$true | $false>] [-EnableDialInConferencing <$true | $false>] [-EnableFileTransfer <$true | $false>] [-EnableMultiViewJoin <$true | $false>] [-EnableOnlineMeetingPromptForLyncResources <$true | $false>] [-EnableP2PFileTransfer <$true | $false>] [-EnableP2PRecording <$true | $false>] [-EnableP2PVideo <$true | $false>] [-FileTransferBitRateKb <Int64>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxMeetingSize <UInt32>] [-MaxVideoConferenceResolution <CIF | VGA>] [-TotalReceiveVideoBitRateKb <Int64>] [-VideoBitRateKb <Int64>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 utilizza il cmdlet **New-CsConferencingPolicy** per creare nuovi criteri di conferenza con il parametro Identity SalesConferencingPolicy. Tali criteri utilizzeranno i valori predefiniti per i criteri di conferenza ad eccezione di MaxMeetingSize. In questo esempio il valore massimo per una riunione sarà impostato su 50 anziché sul valore predefinito di 250.

    New-CsConferencingPolicy -Identity SalesConferencingPolicy -MaxMeetingSize 50

## ESEMPIO 2

Nell'esempio 2, il cmdlet **New-CsConferencingPolicy** viene utilizzato per creare un criterio relativo alle conferenze con il parametro Identity site:Redmond. Nell'esempio vengono configurati due diversi valori di proprietà: MaxMeetingSize è impostato su 100 e AllowParticipantControl è impostato su False. Per tutte le altre proprietà del criterio verranno utilizzati i valori predefiniti.

    New-CsConferencingPolicy -Identity site:Redmond -MaxMeetingSize 100 -AllowParticipantControl $False

## Descrizione dettagliata

Le conferenze rappresentano un aspetto importante di Lync Server: le conferenze consentono ai gruppi di utenti di incontrarsi online per visualizzare diapositive e video, condividere applicazioni, scambiare file, comunicare e collaborare in altro modo.

È importante per gli amministratori mantenere il controllo delle conferenze e delle loro impostazioni. In alcuni casi potrebbero verificarsi problemi di protezione: per impostazione predefinita, tutti gli utenti, inclusi quelli non autenticati, possono partecipare alle riunioni e salvare le diapositive o gli stampati distribuiti durante le riunioni stesse. In altri casi potrebbero verificarsi problemi di larghezza di banda: in presenza di molte riunioni simultanee, in ciascuna delle quali sono coinvolti centinaia di partecipanti con trasmissioni video e condivisioni di file, potrebbero verificarsi problemi nella rete. Inoltre, potrebbero verificarsi problemi legali di natura occasionale. Ad esempio, per impostazione predefinita ai partecipanti alla riunione è consentito creare delle annotazioni sul contenuto condiviso, tuttavia queste annotazioni non vengono salvate quando la riunione viene archiviata. Se l'organizzazione è tenuta a conservare un record di tutte le comunicazioni elettroniche, è possibile disabilitare le annotazioni.

L'esigenza di gestire le impostazioni dei servizi di conferenza è diversa dall'effettiva gestione di queste impostazioni. In Lync Server le conferenze vengono gestite utilizzando i criteri relativi alle conferenze. (Nelle versioni precedenti del software, questi criteri erano definiti criteri riunione). Come osservato, i criteri relativi alle conferenze determinano le caratteristiche e le funzionalità che possono essere utilizzate in una conferenza, a partire dal fatto che la conferenza possa o non possa includere l'audio e il video IP fino al numero massimo di persone che possono partecipare a una riunione. I criteri relativi alle conferenze possono essere configurati nell'ambito globale, nell'ambito del sito o per utente. In tal modo gli amministratori dispongono di un'elevata flessibilità per la determinazione delle funzionalità da rendere disponibili ai singoli utenti.

Il cmdlet **New-CsConferencingPolicy** consente di creare nuovi criteri relativi alle conferenze in ambito sito o per utente. Non è possibile creare un nuovo criterio globale, in quanto tale criterio è già esistente. Tuttavia, è possibile modificare i valori di proprietà del criterio globale utilizzando il cmdlet **Set-CsConferencingPolicy**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsConferencingPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferencingPolicy"}

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
<td><p>L'identificatore univoco per il criterio relativo alle conferenze da creare. I criteri relativi alle conferenze possono essere creati in ambito sito o per utente. Per creare un criterio di sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per creare un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity SalesConferencingPolicy.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowAnnotations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se ai partecipanti è consentito creare delle annotazioni su schermo nei contenuti condivisi durante la riunione. Questa impostazione determina inoltre se l'uso della lavagna è consentito nella conferenza. Il valore predefinito è True.</p>
<p>Le annotazioni non vengono archiviate insieme agli altri contenuti della riunione.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio includerà annotazioni. L'utente può tuttavia partecipare ad altre conferenze in cui le annotazioni sono consentite.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowAnonymousParticipantsInMeetings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti anonimi è consentito partecipare alla riunione. Se impostato su False, solo agli utenti autenticati (ovvero gli utenti che hanno eseguito l'accesso a Servizi di dominio Active Directory o ad Active Directory di un partner federato) è consentito partecipare alla riunione. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio ammetterà partecipanti anonimi. L'utente può tuttavia partecipare ad altre conferenze in cui i partecipanti anonimi sono ammessi.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowAnonymousUsersToDialOut</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti anonimi (utenti non autenticati) è consentito partecipare a una conferenza utilizzando chiamate in uscita. Con le chiamate in uscita il server per conferenze telefona all'utente, il quale accederà alla conferenza rispondendo al telefono.</p>
<p>Le conferenze telefoniche con accesso esterno sono consentite anche se questa impostazione è False.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se il parametro è impostato su False, in nessuna delle conferenze create da un utente al quale si applica questo criterio verrà permesso ai partecipanti anonimi partecipare alla conferenza tramite chiamata esterna. L'utente può partecipare ad altre conferenze nelle quali ai partecipanti anonimi è consentito partecipare tramite chiamata esterna.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowConferenceRecording</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti è consentito registrare la riunione. Il valore predefinito è False.</p>
<p>Questa impostazione riguarda tutti gli utenti che prendono parte alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowExternalUserControl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti esterni (ovvero gli utenti anonimi o federati) è consentito assumere il controllo delle applicazioni o dei desktop condivisi. Il valore predefinito è False.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti sia per le conferenze che per le sessioni di comunicazione peer-to-peer. Di conseguenza, ad alcuni utenti di una sessione può essere consentito di assegnare il controllo di un'applicazione o del desktop condivisi a un utente esterno, mentre ad altri utenti ciò può essere impedito.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>AllowExternalUsersToRecordMeeting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti esterni (ovvero gli utenti anonimi o federati) è consentito registrare la riunione. Il valore predefinito è False.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà agli utenti esterni di registrare le conferenze. L'utente può tuttavia partecipare ad altre conferenze in cui agli utenti esterni è consentito registrare le conferenze.</p>
<p>Questa impostazione è effettiva solo se la proprietà AllowConferenceRecording è impostata su True.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowExternalUsersToSaveContent</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti esterni (ovvero gli utenti che attualmente non hanno effettuato l'accesso alla rete) è consentito salvare stampati, diapositive ed altri contenuti della riunione. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà agli utenti esterni di salvare il contenuto. L'utente può tuttavia partecipare ad altre conferenze in cui agli utenti esterni è consentito salvare il contenuto.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>AllowIPAudio</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se nella riunione è consentito l'uso dell'audio del computer. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio ammetterà l'audio IP. L'utente può tuttavia partecipare ad altre conferenze in cui l'audio IP è ammesso.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowIPVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se nella riunione è consentito l'uso del video del computer. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio ammetterà il video IP. L'utente può tuttavia partecipare ad altre conferenze in cui il video IP è ammesso.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>AllowLargeMeetings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True, tutte le riunioni online vengono trattate come &quot;grandi riunioni&quot;. Con una grande riunione, vi sono limitazioni sul numero di notifiche inviate ai partecipanti, nonché sulle dimensioni dell'elenco dei partecipanti trasmesso per impostazione predefinita.</p>
<p>Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>AllowMultiView</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True (valore predefinito) consente agli utenti di pianificare conferenze che consentono multiview, ossia i client possono ricevere più flussi video durante una data conferenza. Questa impostazione si applica all'utente che organizza la conferenza: se è impostato su False, nessuna conferenza creata da un utente interessato da questi criteri può includere multiview. L'utente può, tuttavia, partecipare ad altre conferenze dove è consentito multiview.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowNonEnterpriseVoiceUsersToDialOut</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti che non sono stati abilitati per VoIP aziendale è consentito partecipare a una conferenza tramite chiamata telefonica esterna. Con la chiamata telefonica esterna, il server per conferenze chiama telefonicamente l'utente. Quando l'utente risponde al telefono, viene aggiunto alla conferenza.</p>
<p>Notare che la conferenza telefonica con accesso esterno è consentita anche quando questa impostazione è False.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se è impostato su False, nessuna conferenza creata da un utente interessato da questi criteri consentirà la partecipazione degli utenti non abilitati per VoIP tramite chiamata telefonica esterna. Tuttavia, l'utente può partecipare ad altre conferenze dove gli utenti non abilitati per VoIP aziendale possono partecipare tramite chiamata esterna.</p>
<p>Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>AllowOfficeContent</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su False, impedisce agli utenti di utilizzare contenuti di Office nelle conferenze.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowParticipantControl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i partecipanti alla riunione sono autorizzati a prendere il controllo delle applicazioni o dei desktop condivisi durante la riunione. Il valore predefinito è True.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui sono applicati questi criteri consentirà il controllo da parte dei partecipanti. L'utente può tuttavia partecipare ad altre conferenze in cui il controllo è consentito.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>AllowPolls</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti è consentito gestire polling online durante una riunione. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà il polling. L'utente può tuttavia partecipare ad altre conferenze in cui il polling è consentito.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowQandA</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), l'utente potrà includere la funzionalità di gestione di domande e risposte in qualsiasi conferenza online che organizza. Se impostato su False, all'utente verrà impedito di includere questa funzionalità nelle conferenze.</p>
<p>Questa impostazione si applica all'utente che organizza la conferenza: se impostato su False, nessuna conferenza creata da un utente a cui sono applicati questi criteri consentirà l'utilizzo della funzionalità di gestione di domande e risposte. Tuttavia, l'utente può utilizzare questa funzionalità in altre conferenze in cui sono consentiti i sondaggi.</p></td>
</tr>
<tr class="even">
<td><p><em>AllowSharedNotes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True (valore predefinito) qualsiasi computer notebook OneNote aperto collegato alla conferenza verrà automaticamente aggiornato con informazioni come partecipanti e dettagli sul contenuto condiviso durante la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowUserToScheduleMeetingsWithAppSharing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se agli utenti è consentito organizzare riunioni con condivisione delle applicazioni. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà la condivisione dell'applicazione. L'utente può tuttavia partecipare ad altre conferenze in cui la condivisione dell'applicazione è consentita.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>La velocità in bit (in kilobit) utilizzata per la condivisione delle applicazioni. Il valore predefinito è 50000.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La velocità in bit (in kilobit) utilizzata per le trasmissioni audio. La velocità in bit dell'audio può corrispondere a qualsiasi numero intero compreso tra 20 e 200. Il valore predefinito è 200.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti sia per le conferenze che per le sessioni di comunicazione peer-to-peer.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo descrittivo sul criterio relativo alle conferenze. Ad esempio, il parametro Description potrebbe indicare gli utenti ai quali deve essere assegnato il criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>DisablePowerPointAnnotations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True ($True), gli utenti non potranno aggiungere note alle diapositive di PowerPoint utilizzate in una conferenza. Tuttavia, a seconda del valore della proprietà AllowAnnotations, gli utenti avranno comunque accesso ad altre funzionalità di lavagna. Il valore predefinito è False che significa che le note di PowerPoint sono consentite.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableAppDesktopSharing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.EnableAppDesktopSharing</p></td>
<td><p>Indica se ai partecipanti è consentito condividere le applicazioni (o i rispettivi desktop) durante il corso di una riunione. I valori consentiti sono:</p>
<p>Desktop. Agli utenti è consentito condividere il desktop.</p>
<p>SingleApplication. Agli utenti è consentito condividere una singola applicazione.</p>
<p>None. Agli utenti non è consentito condividere le applicazioni o il desktop.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti. Di conseguenza, ad alcuni utenti di una conferenza può essere consentito di condividere il desktop o le applicazioni, mentre ad altri utenti della stessa conferenza ciò può essere impedito.</p>
<p>Il valore predefinito è Desktop.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDataCollaboration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti possono organizzare le riunioni con attività di collaborazione dati, quali lavagna e annotazioni.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà la collaborazione dati. L'utente può tuttavia partecipare ad altre conferenze in cui la collaborazione dati è consentita.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDialInConferencing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti sono in grado di accedere alla riunione eseguendo un accesso esterno con un telefono PSTN (Public Switched Telephone Network). Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà le conferenze telefoniche con accesso esterno. L'utente può tuttavia partecipare ad altre conferenze in cui le conferenze telefoniche con accesso esterno sono consentite.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFileTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se durante la riunione sono consentiti i trasferimenti di file a tutti i partecipanti. Il valore predefinito è True.</p>
<p>Questa impostazione riguarda l'utente che organizza la conferenza: se è impostata su False, nessuna conferenza creata da un utente a cui è applicato questo criterio consentirà i trasferimenti di file. L'utente può tuttavia partecipare ad altre conferenze in cui i trasferimenti di file sono consentiti.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMultiViewJoin</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True (valore predefinito) i client tenteranno di partecipare a una conferenza utilizzando multiview (che consente al client di ricevere più flussi video durante la conferenza). Questo parametro verrà ignorato se multiview non è consentito nella conferenza a cui si intende partecipare. Questa impostazione è applicata a livello per utente e sia per le conferenze che per le sessioni di comunicazione peer-to-peer. Pertanto, ad alcuni utenti di una sessione potrebbe essere consentito l'utilizzo di più flussi video mentre ad altri utenti della stessa conferenza no.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableOnlineMeetingPromptForLyncResources</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, ogni volta che gli utenti pianificano una riunione in Outlook che include invitati, ad esempio una sala riunioni, vengono avvisati che sarebbe più vantaggioso tenere la riunione online. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableP2PFileTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se durante la riunione sono consentiti i trasferimenti di file peer-to-peer (ovvero i trasferimenti di file che non coinvolgono tutti i partecipanti). Il valore predefinito è True.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti. Di conseguenza, ad alcuni utenti di una sessione di comunicazione peer-to-peer può essere consentito di trasferire file, mentre ad altri utenti ciò può essere impedito.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableP2PRecording</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se True, gli utenti saranno in grado di registrare sessioni di conferenze peer-to-peer. Il valore predefinito è False.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti. Di conseguenza, ad alcuni utenti di una sessione di comunicazione peer-to-peer può essere consentito di registrare la sessione, mentre ad altri utenti ciò può essere impedito.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableP2PVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se True, gli utenti saranno in grado di partecipare a sessioni di conferenze peer-to-peer. Il valore predefinito è False.</p>
<p>Questa impostazione è applicata a livello dei singoli utenti. Di conseguenza, ad alcuni utenti di una sessione di comunicazione peer-to-peer può essere consentito di utilizzare video nella sessione, mentre ad altri utenti ciò può essere impedito.</p></td>
</tr>
<tr class="even">
<td><p><em>FileTransferBitRateKb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>La velocità in bit (in kilobit) utilizzata per i trasferimenti di file. Il valore predefinito è 50000.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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
<td><p>Indica la velocità in bit massima consentita (in kilobyte al secondo) per tutto il video utilizzato in una conferenza, ossia il totale combinato per tutti i flussi video. Il valore predefinito è 50000 kilobyte al secondo.</p></td>
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

Nessuno. Il cmdlet **New-CsConferencingPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsConferencingPolicy** crea una nuova istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)  
[Remove-CsConferencingPolicy](remove-csconferencingpolicy.md)  
[Set-CsConferencingPolicy](set-csconferencingpolicy.md)

