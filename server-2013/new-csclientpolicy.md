---
title: New-CsClientPolicy
TOCTitle: New-CsClientPolicy
ms:assetid: 47a92c7d-fe94-4843-b9d5-92b955306666
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425949(v=OCS.15)
ms:contentKeyID: 49300415
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio client. I criteri client consentono di stabilire, tra l'altro, le funzionalità di Lync Server disponibili per gli utenti. È ad esempio possibile decidere di consentire solo ad alcuni utenti di trasferire i file, negando questo diritto ad altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsClientPolicy -Identity <XdsIdentity> [-AddressBookAvailability <WebSearchAndFileDownload | WebSearchOnly | FileDownloadOnly>] [-AttendantSafeTransfer <$true | $false>] [-AutoDiscoveryRetryInterval <TimeSpan>] [-BlockConversationFromFederatedContacts <$true | $false>] [-CalendarStatePublicationInterval <UInt32>] [-ConferenceIMIdleTimeout <TimeSpan>] [-Confirm [<SwitchParameter>]] [-CustomizedHelpUrl <String>] [-CustomLinkInErrorMessages <String>] [-CustomStateUrl <String>] [-Description <String>] [-DGRefreshInterval <TimeSpan>] [-DisableCalendarPresence <$true | $false>] [-DisableContactCardOrganizationTab <$true | $false>] [-DisableEmailComparisonCheck <$true | $false>] [-DisableEmoticons <$true | $false>] [-DisableFederatedPromptDisplayName <$true | $false>] [-DisableFeedsTab <$true | $false>] [-DisableFreeBusyInfo <$true | $false>] [-DisableHandsetOnLockedMachine <$true | $false>] [-DisableHtmlIm <$true | $false>] [-DisableInkIM <$true | $false>] [-DisableMeetingSubjectAndLocation <$true | $false>] [-DisableOneNote12Integration <$true | $false>] [-DisableOnlineContextualSearch <$true | $false>] [-DisablePhonePresence <$true | $false>] [-DisablePICPromptDisplayName <$true | $false>] [-DisablePoorDeviceWarnings <$true | $false>] [-DisablePoorNetworkWarnings <$true | $false>] [-DisablePresenceNote <$true | $false>] [-DisableRTFIM <$true | $false>] [-DisableSavingIM <$true | $false>] [-DisplayPhoto <NoPhoto | PhotosFromADOnly | AllPhotos>] [-EnableAppearOffline <$true | $false>] [-EnableCallLogAutoArchiving <$true | $false>] [-EnableClientMusicOnHold <$true | $false>] [-EnableConversationWindowTabs <$true | $false>] [-EnableEnterpriseCustomizedHelp <$true | $false>] [-EnableEventLogging <$true | $false>] [-EnableExchangeContactSync <$true | $false>] [-EnableExchangeDelegateSync <$true | $false>] [-EnableFullScreenVideo <$true | $false>] [-EnableHighPerformanceConferencingAppSharing <$true | $false>] [-EnableHighPerformanceP2PAppSharing <$true | $false>] [-EnableHotdesking <$true | $false>] [-EnableIMAutoArchiving <$true | $false>] [-EnableMediaRedirection <$true | $false>] [-EnableNotificationForNewSubscribers <$true | $false>] [-EnableSQMData <$true | $false>] [-EnableTracing <$true | $false>] [-EnableUnencryptedFileTransfer <$true | $false>] [-EnableURL <$true | $false>] [-EnableVOIPCallDefault <$true | $false>] [-ExcludedContactFolders <String>] [-Force <SwitchParameter>] [-HelpEnvironment <String>] [-HotdeskingTimeout <TimeSpan>] [-IMWarning <String>] [-InMemory <SwitchParameter>] [-MAPIPollInterval <TimeSpan>] [-MaximumDGsAllowedInContactList <UInt32>] [-MaximumNumberOfContacts <UInt16>] [-MaxPhotoSizeKB <UInt32>] [-MusicOnHoldAudioFile <String>] [-P2PAppSharingEncryption <Supported | Enforced | NotSupported>] [-PlayAbbreviatedDialTone <$true | $false>] [-PolicyEntry <PSListModifier>] [-SearchPrefixFlags <UInt16>] [-ShowManagePrivacyRelationships <$true | $false>] [-ShowRecentContacts <$true | $false>] [-ShowSharepointPhotoEditLink <$true | $false>] [-SPSearchCenterExternalURL <String>] [-SPSearchCenterInternalURL <String>] [-SPSearchExternalURL <String>] [-SPSearchInternalURL <String>] [-TabURL <String>] [-TracingLevel <Off | Light | Full>] [-WebServicePollInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di creare un nuovo criterio client con Identity RedmondClientPolicy. Oltre a specificare l'identità, in questo comando sono inclusi tre parametri facoltativi e i relativi valori: DisableCalendarPresence, DisablePhonePresence, DisplayPhoto.

    New-CsClientPolicy -Identity RedmondClientPolicy -DisableCalendarPresence $True -DisablePhonePresence $True -DisplayPhoto "PhotosFromADOnly"

## ESEMPIO 2

Anche nell'esempio 2 viene creato un nuovo criterio client con identità RedmondClientPolicy. La differenza tra questi comandi e quello utilizzato nell'esempio 1 è rappresentata dal fatto che, nell'esempio 2, il nuovo criterio viene creato solo in memoria e solo in seguito diventa un criterio client effettivo. A tale scopo, viene innanzitutto chiamato il cmdlet **New-CsClientPolicy** con due parametri: Identity (per specificare l'identità del nuovo criterio) e InMemory (per indicare che il nuovo criterio deve essere creato solo in memoria e non utilizzato immediatamente). Dal momento che questo criterio viene creato solo in memoria, è necessario archiviarlo in una variabile. In questo esempio, è una variabile denominata $x.

Dopo la creazione del criterio virtuale, i tre comandi successivi vengono utilizzati per modificare le proprietà di tale criterio. Il comando 2 ad esempio imposta il valore della proprietà DisableCalendarPresence su True ($True). Dopo che sono state apportato tutte le modifiche desiderate, l'ultimo comando utilizza il cmdlet **Set-CsClientPolicy** per trasformare il criterio virtuale in un criterio client effettivo che può essere assegnato agli utenti. Si noti che il comando finale è fondamentale. Se non si chiama il cmdlet **Set-CsClientPolicy**, il criterio RedmondClientPolicy non verrà creato e il criterio virtuale verrà eliminato non appena si termina la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsClientPolicy -Identity RedmondClientPolicy -InMemory
    $x.DisableCalendarPresence = $True 
    $x.DisablePhonePresence = $True 
    $x.DisplayPhoto = "PhotosFromADOnly"
    Set-CsClientPolicy -Instance $x

## Descrizione dettagliata

In Lync Server i criteri client sostituiscono le impostazioni di Criteri di gruppo in uso nelle versioni precedenti del prodotto. In Microsoft Office Communicator 2007 e Microsoft Office Communicator 2007 R2 la funzionalità Criteri di gruppo viene utilizzata per definire le azioni consentite agli utenti in Communicator e in altri client. Alcune impostazioni di Criteri di gruppo ad esempio stabiliscono se gli utenti possono o meno salvare una trascrizione delle rispettive sessioni di messaggistica istantanea, se possono o meno inserire emoticon o testo formattato nei messaggi istantanei e se nelle informazioni sulla presenza vengono incorporate le informazioni di Microsoft Outlook.

Per quanto utile, la tecnologia di Criteri di gruppo tuttavia presenta limitazioni se applicata a Lync Server. Da un lato, Criteri di gruppo è stato concepito per essere applicato per singolo dominio o per singola unità organizzativa e pertanto risulta difficile applicare i criteri a un gruppo di utenti specifici, ad esempio tutti gli utenti che lavorano in un determinato reparto o tutti gli utenti con una determinata qualifica. Dall'altro, Criteri di gruppo viene applicato solo agli utenti che accedono al dominio tramite un computer e non agli utenti che accedono a Lync Server da Internet o che accedono al sistema utilizzando un telefono cellulare. Ciò significa che lo stesso utente può avere un'esperienza diversa in base al dispositivo e al luogo da cui esegue l'accesso.

Per ovviare a questi problemi, in Lync Server vengono utilizzati criteri client anziché Criteri di gruppo. I criteri client vengono applicati ogni volta che un utente accede al sistema, indipendentemente dal dispositivo e dal luogo da cui viene eseguito l'accesso. I criteri client, analogamente ad altri criteri di Lync Server, possono inoltre essere applicati a gruppi di utenti selezionati. È anche possibile creare un criterio personalizzato che viene assegnato a un singolo utente.

Il cmdlet **New-CsClientPolicy** consente di creare nuovi criteri client nell'ambito del sito o nell'ambito per utente. Si noti che ciascun sito può avere al massimo un unico criterio client; se si cerca di creare un criterio per il sito Redmond e nel sito è già presente un criterio client, il comando avrà esito negativo. Allo stesso modo, il comando avrà esito negativo se si cerca di creare un nuovo criterio client nell'ambito globale, dal momento che l'ambito globale contiene già un criterio client. Se è necessario apportare modifiche al criterio globale, utilizzare il cmdlet **Set-CsClientPolicy**.

Tenere presente che i criteri client sono diversi da molti altri criteri in quanto per la maggior parte delle impostazioni non sono disponibili valori predefiniti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsClientPolicy** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientPolicy"}

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
<td><p>Identità univoca da assegnare al nuovo criterio. I nuovi criteri client possono essere creati nell'ambito del sito e per utente. Per creare un nuovo criterio del sito, utilizzare il prefisso &quot;site:&quot; e il nome del sito come identità. Ad esempio, utilizzare la sintassi seguente per creare un nuovo criterio per il sito Redmond: -Identity site:Redmond. Per creare un nuovo criterio per utente, usare un'identità simile alla seguente: -Identity SalesClientPolicy.</p></td>
</tr>
<tr class="even">
<td><p><em>AddressBookAvailability</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.AddressBookAvailability</p></td>
<td><p>Indica il modo in cui gli utenti possono accedere alle informazioni utilizzando servizio query Web della Rubrica e/o scaricando una copia della Rubrica sul computer locale. Il parametro AddressBookAvailability deve essere impostato su uno dei seguenti valori:</p>
<p>WebSearchAndFileDownload</p>
<p>WebSearchOnly</p>
<p>FileDownloadOnly</p></td>
</tr>
<tr class="odd">
<td><p><em>AttendantSafeTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, Attendant funziona in modalità &quot;trasferimento sicuro&quot;; ciò significa che le chiamate trasferite che non raggiungono il destinatario verranno di nuovo visualizzate nell'area conversazioni in arrivo con una notifica di &quot;trasferimento non riuscito&quot;. Se impostato su False, le chiamate trasferite che non raggiungono il destinatario non verranno di nuovo visualizzate nell'area conversazioni in arrivo.</p></td>
</tr>
<tr class="even">
<td><p><em>AutoDiscoveryRetryInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Dopo un tentativo di connessione non riuscito, specifica il tempo di attesa di Lync prima di un nuovo tentativo di connessione a Lync Server. Il parametro AutoDiscoveryRetryInterval può essere impostato su un valore compreso tra 1 secondo e 60 minuti (1 ora), estremi inclusi.</p>
<p>Quando si specifica il parametro AutoDiscoveryRetryInterval, è necessario utilizzare il formato ore:minuti:secondi. Per impostare, ad esempio, l'intervallo su 25 minuti, utilizzare la sintassi seguente:</p>
<p>- AutoDiscoveryRetryInterval 00:25:00</p>
<p>Questa impostazione equivale all'impostazione &quot;Intervallo di tempo tra tentativi di individuazione automatica&quot; di Criteri di gruppo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>BlockConversationFromFederatedContacts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i contatti esterni all'organizzazione non saranno autorizzati ad avviare conversazioni istantanee con qualunque utente al quale sia applicato questo criterio. Tuttavia, gli utenti esterni potranno partecipare alle conversazioni avviate da un utente interno. Se impostato su False, i contatti esterni saranno autorizzati a inviare messaggi istantanei indesiderati agli utenti interni all'organizzazione.</p>
<p>Questa impostazione equivale all'impostazione &quot;Blocca conversazione da gruppo di contatti associati esterni&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>CalendarStatePublicationInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Specifica il tempo di attesa, espresso in secondi, prima che Lync recuperi le informazioni del calendario da Microsoft Outlook e le aggiunga alle informazioni sulla presenza.</p>
<p>Per impostare, ad esempio, CalendarStatePublicationInterval su 10 minuti (600 secondi), utilizzare la sintassi seguente:</p>
<p>- CalendarStatePublicationInterval 600</p>
<p>Questa impostazione equivale all'impostazione &quot;Intervallo di tempo di pubblicazione dati calendario nella presenza&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>ConferenceIMIdleTimeout</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica il tempo in minuti per il quale un utente può rimanere in una sessione di messaggistica istantanea senza inviare né ricevere alcun messaggio istantaneo.</p>
<p>Il parametro ConferenceIMIdleTimeout deve essere minore o uguale a un'ora e deve essere specificato utilizzando il formato ore:minuti:secondi. Per impostare il valore di timeout su 45 minuti, utilizzare ad esempio la sintassi seguente:</p>
<p>-ConferenceIMIdleTimeout 00:45:00</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomizedHelpUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL della guida personalizzata di Lync Server preparata da un'organizzazione. Questa guida personalizzata verrà visualizzata al posto della guida predefinita del prodotto quando un utente fa clic sul menu ? di Lync.</p>
<p>Tuttavia, perché la guida personalizzata sia disponibile, occorre che anche il parametro EnableEnterpriseCustomizedHelp sia impostato su True.</p>
<p>Questa impostazione equivale all'impostazione &quot;Menu ?&quot; di Criteri di gruppo in Communications Server 2007 R2. L'uso di questo parametro è deprecato con Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomLinkInErrorMessages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del sito Web che è possibile aggiungere ai messaggi di errore visualizzati in Lync Server. Se viene specificato un URL, questo verrà visualizzato alla fine di ogni messaggio di errore visualizzato in Lync Server. Gli utenti possono fare clic sul collegamento e accedere a un sito Web personalizzato contenente informazioni aggiuntive, ad esempio suggerimenti per la risoluzione dei problemi.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomStateUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Specifica il percorso del file XML utilizzato per aggiungere a Lync Server i diversi stati di presenza personalizzati. Lync Server supporta fino a quattro stati di presenza personalizzati oltre a quelli predefiniti (Disponibile, Occupato e Non disturbare). Il percorso del file XML deve essere specificato utilizzando il protocollo HTTPS.</p>
<p>Questa impostazione equivale all'impostazione &quot;URL stati presenza personalizzati&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire informazioni aggiuntive su un criterio. Ad esempio, nella descrizione potrebbero essere indicati gli utenti ai quali deve essere assegnato il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>DGRefreshInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica il tempo di attesa di Lync Server prima di un nuovo aggiornamento automatico dell'elenco dei membri di un gruppo di distribuzione &quot;espanso&quot; nell'elenco contatti. Espandere un gruppo di distribuzione significa semplicemente visualizzare tutti i membri di tale gruppo. Il parametro DGRefreshInterval può essere impostato su un numero intero compreso tra 30 e 28.000 secondi (8 ore), estremi inclusi. Il valore predefinito è 28.800 secondi.</p>
<p>Questa impostazione equivale all'impostazione &quot;Intervallo di tempo per aggiornamento appartenenza di ogni gruppo di distribuzione&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableCalendarPresence</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le informazioni del calendario prese da Microsoft Outlook non vengono incluse nelle informazioni sulla presenza. Se impostato su False, le informazioni del calendario vengono incluse nelle informazioni sulla presenza. Ad esempio, le informazioni sulla disponibilità vengono riportate nella scheda del contatto. Allo stesso modo, lo stato viene automaticamente impostato su Occupato tutte le volte che in Outlook risulta che l'utente è impegnato in riunione.</p>
<p>Questa impostazione equivale all'impostazione &quot;Disattiva presenza calendario&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableContactCardOrganizationTab</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, la scheda Organizzazione della scheda contatto non sarà visibile nell'interfaccia utente di Lync. Se invece si imposta il parametro su False, la scheda Organizzazione della scheda contatto sarà disponibile in Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailComparisonCheck</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, Lync non tenterà di verificare che ogni singola istanza di Microsoft Outlook attualmente in esecuzione appartenga allo stesso utente che esegue Lync Server. Ad esempio, il software non verificherà che Outlook e Lync siano entrambi in esecuzione nell'ambito dell'account utente di Ken Myer. Il programma presupporrà che le due applicazioni siano in esecuzione nell'ambito dello stesso account utente e, di conseguenza, includerà i dati relativi a contatto e calendario di Outlook in Lync.</p>
<p>Se impostato su False, Lync utilizzerà gli indirizzi SMTP per verificare che Outlook e Lync siano in esecuzione nell'ambito dello stesso account. Se gli indirizzi SMTP non corrispondono, i dati relativi a contatto e calendario di Outlook non verranno incorporati in Lync.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>DisableEmoticons</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, gli utenti non saranno in grado di inviare o ricevere emoticon nei loro messaggi istantanei; vedranno, invece, il testo equivalente a quegli emoticon. Ad esempio, invece di vedere l'immagine grafica di uno smile, gli utenti vedranno solo il suo corrispondente testuale:</p>
<p>: )</p>
<p>Se impostato su False, gli utenti potranno includere gli emoticon nei loro messaggi istantanei e visualizzarli correttamente nei messaggi istantanei che riceveranno.</p>
<p>Questa impostazione equivale all'impostazione &quot;Disabilita emoticon nei messaggi istantanei&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableFederatedPromptDisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, tutte le finestre di notifica create quando un utente viene aggiunto all'elenco contatti di un altro utente federato utilizzeranno l'indirizzo SIP dell'utente federato, ad esempio sip:kenmyer@fabrikam.com. Se impostato su False, la finestra di notifica utilizzerà invece il nome visualizzato dell'utente federato, ad esempio Ken Myer.</p>
<p>Questa impostazione equivale all'impostazione &quot;Impedisci visualizzazione nome visualizzato di gruppi di contatti non PIC nella finestra di dialogo di notifica&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableFeedsTab</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, la scheda dei feed attività non verrà visualizzata in Lync. Se invece si imposta il parametro su False, la scheda dei feed attività sarà disponibile in Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableFreeBusyInfo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le informazioni sulla disponibilità recuperate da Microsoft Outlook non vengono visualizzate nella scheda del contatto. Se impostato su False, le informazioni sulla disponibilità vengono visualizzate nella scheda del contatto Ad esempio, la scheda del contatto potrebbe includere una nota simile alla seguente:</p>
<p>Calendario: Libero fino alle 14:00</p>
<p>Questa impostazione equivale all'impostazione &quot;Disabilita pubblicazione informazioni su disponibilità&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableHandsetOnLockedMachine</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, gli utenti non saranno in grado di utilizzare il ricevitore Polycom se il computer a cui è connesso il ricevitore è bloccato. Per utilizzare il ricevitore, gli utenti dovranno prima sbloccare il computer.</p>
<p>Se invece si imposta il parametro su False, gli utenti potranno utilizzare un ricevitore Polycom anche quando il computer a cui è connesso il ricevitore è bloccato.</p>
<p>Questa impostazione equivale all'impostazione &quot;Configura uso del ricevitore in caso di computer bloccato&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableHtmlIm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, qualunque testo HTML copiato da una pagina Web verrà convertito in testo normale quando viene incollato in un messaggio istantaneo. Se impostato su False, la formattazione HTML (ad esempio, dimensioni e colore del carattere, elenchi a discesa, pulsanti) verrà mantenuta quando il testo viene incollato in un messaggio istantaneo.</p>
<p>Si noti che, anche quando il parametro è impostato su False, gli script e altri elementi potenzialmente pericolosi (come i tag che riproducono un suono) non verranno comunque copiati nel messaggio istantaneo. È possibile copiare e incollare i pulsanti e altri controlli nel messaggio, ma gli script allegati a quei controllo verranno automaticamente rimossi.</p>
<p>Questa impostazione equivale all'impostazione &quot;Impedisci formato HTML in messaggi istantanei&quot; di Criteri di gruppo in Communicator 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableInkIM</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, agli utenti non sarà consentito ricevere messaggi istantanei contenenti dati immessi in un Tablet PC utilizzando l'inchiostro digitale. Si tratta di una tecnologia di scrittura che consente di inserire note scritte a mano in un documento. Se impostato su False, agli utenti sarà consentito ricevere messaggi contenenti dati immessi in un Tablet PC utilizzando l'inchiostro digitale.</p>
<p>Questa impostazione equivale all'impostazione &quot;Impedisci input penna nei messaggi istantanei&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableMeetingSubjectAndLocation</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su False, le informazioni dettagliate su una riunione, ad esempio l'oggetto della riunione e il luogo in cui si svolge, verranno visualizzate come suggerimento quando si visualizzano le informazioni sulla disponibilità in una scheda contatto. Se invece si imposta il parametro su True, queste informazioni dettagliate non verranno visualizzate. Per impedire completamente la visualizzazione di informazioni sulla riunione, impostare anche DisableCalendarPresence su True.</p>
<p>Questa impostazione equivale all'impostazione &quot;Disabilita pubblicazione informazioni su oggetto riunione e sede&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableOneNote12Integration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà disabilitata la possibilità di avviare Microsoft OneNote da Lync e di collegare automaticamente le sessioni di messaggistica istantanea alle note di OneNote. Se invece si imposta il parametro su False, l'opzione Scrivi note con OneNote verrà abilitata in Lync. Se inoltre si individua la trascrizione di un messaggio istantaneo nella Cronologia conversazioni di Microsoft Outlook, sarà possibile recuperare le eventuali note di OneNote associate a tale conversazione semplicemente facendo clic sul pulsante per la modifica delle note sulla conversazione.</p>
<p>Questa impostazione equivale all'impostazione &quot;Disabilita integrazione con OneNote 12&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableOnlineContextualSearch</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, consente di disabilitare l'opzione Trova conversazioni precedenti che viene visualizzata quando si fa clic con il pulsante destro del mouse su un utente nell'elenco dei contatti. Questa opzione consente di effettuare ricerche nella cartella Cronologia conversazioni di Microsoft Outlook per trovare precedenti sessioni di messaggistica istantanea che coinvolgono l'utente in questione. Se impostato su False, l'opzione Trova conversazioni precedenti è abilitata quando si fa clic con il pulsante destro del mouse su un utente nell'elenco dei contatti.</p>
<p>Si noti che questa impostazione si applica solo agli utenti che non eseguono Microsoft Outlook in modalità cache. Questo perché le ricerche effettuate da quegli utenti devono necessariamente avvenire su Microsoft Exchange Server e spesso gli amministratori preferiscono limitare il traffico di rete causato da questo tipo di ricerche. Se Outlook viene eseguito in modalità cache, le ricerche vengono effettuate su una copia della posta in arrivo dell'utente memorizzata nella cache locale. Le ricerche nella cache non sono influenzati da questa impostazione.</p>
<p>Questa impostazione equivale all'impostazione &quot;Disabilita ricerca contestuale online&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisablePhonePresence</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, Lync non considererà le chiamate telefoniche per stabilire lo stato corrente dell'utente. Se invece si imposta il parametro su False, le chiamate telefoniche verranno considerate nella determinazione dello stato corrente dell'utente. Ad esempio, ogni volta che l'utente è al telefono, il relativo stato viene automaticamente impostato su Occupato.</p>
<p>Questa impostazione equivale all'impostazione &quot;Disabilita presenza chiamata&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisablePICPromptDisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, tutte le finestre di notifica generate quando un utente viene aggiunto all'elenco dei contatti di un utente con un account su un servizio di messaggistica istantanea pubblica (ad esempio, MSN) utilizzeranno l'indirizzo SIP del secondo utente (ad esempio, sip:kenmyer@litwareinc.com). Se impostato su False, la finestra di notifica utilizzerà invece il nome visualizzato del secondo utente (ad esempio, Ken Myer).</p>
<p>Questa impostazione equivale all'impostazione &quot;Impedisci visualizzazione nome visualizzato dei contatti PIC nella finestra di dialogo di notifica&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisablePoorDeviceWarnings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, Lync non invierà avvisi (ad esempio all'avvio, nella regolazione guidata, nella finestra di conversazione) qualora un dispositivo audio o video non funzioni correttamente. Se invece si imposta il parametro su False, gli avvisi verranno inviati.</p></td>
</tr>
<tr class="even">
<td><p><em>DisablePoorNetworkWarnings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True, in Lync non vengono visualizzati avvisi relativi alla scarsa qualità della rete.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisablePresenceNote</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il messaggio Fuori sede configurato in Microsoft Outlook non verrà visualizzati come parte delle informazioni sulla presenza. Se impostato su False, il messaggio Fuori sede di un utente verrà visualizzato tutte le volte che un altro utente posiziona il puntatore del mouse sul nome del primo utente nel proprio elenco contatti.</p>
<p>Questa impostazione equivale all'impostazione &quot;Disabilita nota presenza&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableRTFIM</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questa impostazione e l'impostazione DisableHtmlIm sono impostate su True, si impedisce agli utenti di utilizzare la formattazione RTF (ad esempio, con tipi, dimensioni e colori dei caratteri diversi) nei messaggi istantanei; nei messaggi inviati e ricevuti il formato RTF viene convertito in testo normale. Se impostato su False, la formattazione RTF verrà mantenuta nei messaggi istantanei.</p>
<p>Questa impostazione equivale all'impostazione &quot;Impedisci formato RTF in messaggi istantanei&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisableSavingIM</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, le opzioni per il salvataggio di una sessione di messaggistica istantanea verranno rimosse dalla barra dei menu nella finestra di conversazione di Lync. Se invece si imposta il parametro su False, queste opzioni saranno disponibili nella finestra di conversazione.</p>
<p>Si noti che, impostando questo valore su True, vengono rimosse le opzioni che semplificano il salvataggio delle trascrizioni dei messaggi istantanei. Tuttavia, ciò non impedisce agli utenti di copiare tutto il testo di una trascrizione negli Appunti, incollarlo in un'altra applicazione e quindi salvarlo comunque come trascrizione.</p>
<p>Questa impostazione equivale all'impostazione &quot;Impedisci salvataggio di messaggi istantanei&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayPhoto</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.DisplayPhoto</p></td>
<td><p>Stabilisce se le foto dell'utente e dei relativi contatti verranno visualizzate o meno in Lync. Le impostazioni valide sono:</p>
<p>NoPhoto - Le foto non vengono visualizzate in Lync.</p>
<p>PhotosFromADOnly - Vengono visualizzate solo le foto che sono state pubblicate in Active Directory.</p>
<p>AllPhotos - Vengono visualizzate sia le foto di Active Directory sia quelle personalizzate.</p>
<p>Il valore predefinito è AllPhotos.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableAppearOffline</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, in Lync sarà disponibile un altro stato presenza, Invisibile. In questo stato l'utente risulta essere offline, ma in realtà è online e può rispondere alle chiamate e ai messaggi istantanei. Se si imposta il parametro su False, lo stato di presenza Invisibile non sarà disponibile in Lync.</p>
<p>Questa impostazione equivale all'impostazione &quot;Abilita stato Invisibile&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCallLogAutoArchiving</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le informazioni sulle chiamate telefoniche in arrivo e in uscita vengono automaticamente salvate nella cartella Cronologia conversazioni di Microsoft Outlook. In effetti, la chiamata in quanto tale non viene registrata. Ciò che viene registrato è chi ha preso parte alla chiamata, la durata della chiamata e se si tratta di una chiamata in arrivo o in uscita. Se impostato su False, queste informazioni non vengono salvate in Outlook.</p>
<p>Questa impostazione equivale all'impostazione &quot;Abilita/disabilita archiviazione automatica dei registri chiamate nella cassetta postale di Outlook&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableClientMusicOnHold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, la musica verrà riprodotta ogni volta che un chiamante verrà messo in attesa. Se impostato su False, la musica non verrà riprodotta ogni volta che un chiamante verrà messo in attesa. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableConversationWindowTabs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le informazioni supplementari relative a una sessione di messaggistica istantanea verranno visualizzate in una finestra separata del browser. Questo tipo di informazioni è disponibile solo per le applicazioni personalizzate che utilizzano le API per le comunicazioni unificate di Microsoft. Ad esempio, il personale del servizio clienti o del supporto tecnico può accedere automaticamente alle informazioni mentre è in chat con qualcuno.</p>
<p>Se impostato su False, le informazioni supplementari non verranno visualizzate in una finestra separata del browser. Sebbene l'utente possa ancora prendere parte a una sessione di messaggistica istantanea, tuttavia non avrà accesso alle informazioni supplementari associate alla sessione.</p>
<p>Questa impostazione equivale all'impostazione &quot;Abilita le schede nella finestra conversazione&quot; di Criteri di gruppo in Communications Server 2007 R2. L'utilizzo di questo parametro è deprecato con Lync Server 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableEnterpriseCustomizedHelp</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, gli utenti che fanno clic sul menu ? di Lync visualizzeranno la guida personalizzata preparata dall'organizzazione. Se invece si imposta il parametro su False, gli utenti che fanno clic sul menu ? visualizzeranno la guida predefinita di Lync.</p>
<p>Se si abilita la Guida personalizzata, è necessario anche specificare un URL valido per il sito Web della Guida personalizzata. A tale scopo, utilizzare il parametro CustomizedHelpUrl. Se questo parametro non è specificato oppure l'URL non è valido, è probabile che si verifichino errori quando gli utenti tentano di pianificare riunioni o di parteciparvi.</p>
<p>L'utilizzo di questo parametro è deprecato con Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableEventLogging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, nel registro eventi applicazioni verranno registrate le informazioni dettagliate su Lync. Se invece si imposta il parametro su False, nel registro eventi verranno registrati solo gli eventi principali, ad esempio la mancata connessione a Lync Server.</p>
<p>Questa impostazione equivale all'impostazione &quot;Attiva registrazione eventi per Communicator&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableExchangeContactSync</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True (valore predefinito), Lync creerà un contatto personale corrispondente in Microsoft Outlook per ogni persona inclusa nell'elenco contatti di un utente in Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableExchangeDelegateSync</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, ai delegati configurati da un utente in Microsoft Exchange verrà consentito di programmare le riunioni online di quell'utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFullScreenVideo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando l'impostazione è True, questo parametro consente due operazioni: 1) abilitazione del video in modalità schermo intero, con le proporzioni corrette, per le chiamate di Lync e 2) disabilitazione dell'anteprima video per le chiamate di Lync. Quando l'impostazione è False, in Lync non è disponibile la modalità video schermo intero, ma è disponibile l'anteprima video.</p>
<p>Questa impostazione equivale all'impostazione &quot;Abilita video a schermo intero e disabilita anteprima video per tutte le videochiamate di OC&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableHighPerformanceConferencingAppSharing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, consente migliori prestazioni per le applicazioni (come le applicazioni CAD/CAM) che hanno un'elevata frequenza di aggiornamento dello schermo. Tuttavia, questo miglioramento delle prestazioni ridurrà le risorse di sistema e la larghezza di banda disponibili per le altre applicazioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableHighPerformanceP2PAppSharing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, consente a una sessione di condivisione applicazioni peer-to-peer di superare la frequenza dei fotogrammi massima di 2,5 fotogrammi al secondo. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableHotdesking</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato su True, questo parametro consente agli utenti di accedere a un telefono con Lync Phone Edition in un'area di lavoro condivisa tramite il relativo account Lync Server. Tra l'altro, in questo modo l'utente può accedere anche ai propri contatti. Se invece il parametro è impostato su False, gli utenti non potranno accedere a un telefono utilizzando le proprie credenziali.</p>
<p>Si noti che questa impostazione si applica solo ai telefoni nelle aree comuni e non agli utenti. Se impostato su True e applicato a un telefono in un'area comune, qualsiasi utente potrà accedere a quel telefono usando le proprie credenziali. Se impostato su False, nessun utente potrà accedere a un telefono in un'area comune a cui è stato applicato questo criterio.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>EnableIMAutoArchiving</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, nella cartella Cronologia conversazioni di Microsoft Outlook verrà salvata una trascrizione di ciascuna sessione di messaggistica istantanea a cui l'utente partecipa. Se impostato su False, queste trascrizioni non verranno salvate automaticamente. Tuttavia, gli utenti hanno l'opzione di salvare manualmente le trascrizioni dei messaggi istantanei.</p>
<p>Questa impostazione equivale all'impostazione &quot;Abilita/disabilita archiviazione automatica delle conversazioni istantanee nella cassetta postale di Outlook&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMediaRedirection</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True ($True), questo parametro consente di separare i flussi audio e video da altro traffico di rete. In questo modo i dispositivi client possono eseguire la codifica e la decodifica di audio e video localmente. Il reindirizzamento degli elementi multimediali in genere comporta un utilizzo inferiore della larghezza di banda, una maggiore scalabilità del server e un'esperienza utente superiore rispetto a tecniche simili, ad esempio le comunicazioni remote dei dispositivi o la compressione codec.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableNotificationForNewSubscribers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, ogni volta che un utente viene aggiunto all'elenco contatti di un altro utente riceverà la notifica di questa operazione. Nella finestra di dialogo di notifica sono inoltre disponibili opzioni che consentono all'utente di aggiungere l'altro utente al proprio elenco contatti oppure di bloccare la visualizzazione delle proprie informazioni sulla presenza. Se impostato su False, l'utente non riceverà alcuna notifica quando un altro utente lo aggiunge al proprio elenco contatti.</p>
<p>Questa impostazione equivale all'impostazione di Criteri di gruppo di Office Communications Server 2007 R2 relativa alla visualizzazione di notifiche per nuovi sottoscrittori presenza.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSQMData</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Nota: questa impostazione è deprecata per Lync Server 2013.</p>
<p>Il programma Analisi utilizzo software è progettato per consentire a Microsoft di raccogliere dati relativi all'utilizzo reale di Lync. Quando un utente viene registrato nel programma Analisi utilizzo software, tutte le volte che esegue Lync, le informazioni relative alle operazioni eseguite e alla relativa frequenza vengono inviate a Microsoft, archiviate in un database e quindi analizzate per individuare le tendenze di utilizzo.</p>
<p>Quando EnableSQMData è impostato su True, l'utente non viene automaticamente registrato nel programma Analisi utilizzo software. Lync tuttavia fornisce all'utente la possibilità di partecipare al programma.</p>
<p>Se si imposta questo parametro su False, l'utente non verrà registrato nel programma Analisi utilizzo software. Inoltre, Lync non offrirà agli utenti la possibilità di partecipare al programma. L'unico modo per consentire a un utente di partecipare al programma Analisi utilizzo software consiste nell'impostare il parametro EnableSQMData su True e nell'accettare esplicitamente di partecipare.</p>
<p>Si noti che non verrà inviata alcuna informazione personale al programma Analisi utilizzo software. Il programma Analisi utilizzo software non tiene traccia di informazioni come ad esempio i destinatari dei messaggi istantanei. Vengono registrate invece informazioni quali la frequenza con cui gli utenti utilizzano Lync per trasferire i file o il numero medio di contatti contenuti negli elenchi contatti.</p>
<p>Questa impostazione equivale all'impostazione &quot;Specifica strumentazione&quot; di Criteri di gruppo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableTracing</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà abilitata la funzionalità di traccia del software in Lync. Se invece si imposta il parametro su False, la funzionalità di traccia del software verrà disabilitata. La funzionalità di traccia del software comporta una registrazione dettagliata di tutte le attività di un programma, inclusa la traccia della chiamate API. Questo tipo di traccia è utile soprattutto per gli sviluppatori e il personale di supporto per le applicazioni.</p>
<p>Questa impostazione equivale all'impostazione &quot;Attiva traccia per Communicator&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableUnencryptedFileTransfer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, agli utenti sarà consentito scambiare file con utenti esterni il cui software di messaggistica istantanea non supporta il trasferimento di file crittografati. Se impostato su False, agli utenti sarà consentito scambiare file solo con utenti esterni il cui software di messaggistica istantanea supporta il trasferimento di file crittografati.</p>
<p>Questa impostazione equivale all'impostazione &quot;Consenti il trasferimento di file non crittografati&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, i collegamenti ipertestuali incorporati in un messaggio istantaneo vengono attivati; ciò significa che, se gli utenti fanno clic su di essi, il browser accede ai siti corrispondenti. Se impostato su False, i collegamenti ipertestuali risultano disattivati, cioè vengono visualizzati come semplice testo nei messaggi istantanei. In questo caso, per accedere al sito corrispondente, gli utenti dovranno copiare e incollare il testo del collegamento nel browser.</p>
<p>Questa impostazione equivale all'impostazione &quot;Consenti collegamenti ipertestuali nei messaggi istantanei&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableVOIPCallDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà effettuata una chiamata Lync ogni volta che un utente utilizza la funzionalità di chiamata con un clic.</p>
<p>L'impostazione di questo criterio influisce solo sullo stato iniziale della caratteristica di chiamata con un clic. Se l'utente modifica il valore dell'impostazione di chiamata con un clic, il valore selezionato dall'utente avrà la precedenza sull'impostazione di questo criterio. Dopo che un utente ha modificato l'impostazione di chiamata con un clic, tale impostazione rimane in uso e il criterio EnableVOIPCallDefault non ha effetto su di essa.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludedContactFolders</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica le eventuali cartelle contatti di Microsoft Outlook in cui non devono essere effettuate le ricerche di nuovi contatti avviate in Lync. È possibile specificare più cartelle separandone i nomi con un punto e virgola, ad esempio: -ExcludedContactFolders &quot;SenderPhotoContacts;OtherContacts&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HelpEnvironment</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se si imposta questo parametro su &quot;Office 365&quot;, gli utenti visualizzeranno la Guida client di Skype for Business online per Lync 2013 anziché la Guida locale visualizzata per impostazione predefinita. È possibile impostare HelpEnvironment su &quot;Office 365&quot; o su un valore Null ($Null). Se si utilizza un valore Null (valore predefinito), gli utenti visualizzeranno la Guida locale.</p></td>
</tr>
<tr class="even">
<td><p><em>HotdeskingTimeout</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Intervallo di timeout di un utente collegato a un telefono di tipo Hot Desk, ovvero un telefono di Lync Phone Edition che si trova in un'area di lavoro condivisa e al quale gli utenti possono accedere utilizzando i propri account di Lync Server. Il parametro HotdeskingTimeout specifica il numero di minuti che possono trascorrere prima che un utente venga automaticamente scollegato da un telefono di tipo Hot Desk. Quando si specifica questo timeout, è necessario utilizzare il formato ore:minuti:secondi. Per specificare un intervallo di timeout di hotdesking di 45 minuti, utilizzare ad esempio la sintassi seguente:</p>
<p>-HotdeskingTimeout 00:45:00</p>
<p>Si noti che questa impostazione si applica solo ai telefoni di area comune e non agli utenti. Il valore predefinito è 5 minuti (00:05:00) e il valore minimo è 30 secondi (00:00:30).</p></td>
</tr>
<tr class="odd">
<td><p><em>IMWarning</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se configurato, il messaggio specificato viene visualizzato nella finestra di conversazione ogni volta che un utente partecipa a una sessione di messaggistica istantanea. Se ad esempio per IMWarning è specificato il messaggio &quot;Tutte le informazioni sono di proprietà di Litwareinc&quot;, questo messaggio verrà visualizzato nella finestra di conversazione ogni volta che un utente partecipa a una sessione di messaggistica istantanea.</p>
<p>Se impostato su un valore Null ($Null), nella finestra Conversazione non verrà visualizzato alcun messaggio.</p>
<p>Il messaggio di avviso deve essere composto da un massimo di 256 caratteri e può contenere solo testo normale. Non è possibile utilizzare alcun tipo di formattazione (ad esempio grassetto o corsivo) e non è possibile inserire URL su cui fare clic all'interno del testo.</p>
<p>Questa impostazione equivale all'impostazione &quot;Testo di avviso&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MAPIPollInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Importante: l'utilizzo di questo parametro è deprecato con Lync Server 2013.</p>
<p>Per gli utenti di Microsoft Exchange Server 2003, il parametro MAPIPollInterval specifica la frequenza con cui Lync recupera i dati di calendario dalle cartelle pubbliche di Exchange. Il parametro MAPIPollInterval può essere impostato su un valore compreso tra 1 secondo e 1 ora, estremi inclusi. Per configurare l'intervallo di polling MAPI, utilizzare il formato ore:minuti:secondi. Il comando seguente imposta ad esempio l'intervallo di polling MAPI su 45 minuti:</p>
<p>-MapiPollInterval 00:45:00</p>
<p>Si noti che questa impostazione non si applica agli utenti il cui account di posta elettronica si trova in Microsoft Exchange Server 2010 o Microsoft Exchange Server 2007. Per questi utenti, il recupero dei dati del calendario viene gestito tramite il parametro WebServicePollInterval.</p>
<p>Questa impostazione equivale all'impostazione &quot;Intervallo di tempo per il caricamento dei dati del calendario dal provider MAPI&quot; di Criteri di gruppo in Office Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>MaximumDGsAllowedInContactList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indicate il numero massimo di gruppi di distribuzione che un utente può configurare come contatto. Il parametro MaximumDGsAllowedInContactList può essere impostato su qualsiasi numero intero compreso tra 0 e 64, inclusi. Il valore predefinito è 10.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaximumNumberOfContacts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Indica il numero massimo di contatti che un utente può avere. Il numero massimo di contatti può essere impostato su qualsiasi numero intero compreso tra 0 e 1000, inclusi. Se impostato su 0, l'utente non può avere alcun contatto.</p>
<p>Questa impostazione equivale all'impostazione &quot;Numero massimo di contatti consentiti&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxPhotoSizeKB</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica la dimensione massima (in kilobyte) delle foto visualizzate in Lync.</p>
<p>Il valore predefinito è 30 kilobyte.</p></td>
</tr>
<tr class="odd">
<td><p><em>MusicOnHoldAudioFile</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il percorso del file audio da riprodurre quando un chiamante viene messo in attesa. Se per questa proprietà è configurato un valore, la musica di attesa verrà abilitata e nessun utente potrà disabilitarla. Se per questa proprietà non è configurato alcun valore, gli utenti possono specificare un proprio file audio per la musica di attesa, a condizione che il parametro EnableClientMusicOnHold sia impostato su True.</p></td>
</tr>
<tr class="even">
<td><p><em>P2PAppSharingEncryption</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.P2PAppSharingEncryption</p></td>
<td><p>Indica se i dati di condivisione delle applicazioni e del desktop scambiati durante una conversazione peer-to-peer devono essere crittografati o meno. I valori consentiti sono:</p>
<p>Supported. I dati di condivisione delle applicazioni e del desktop verranno crittografati, se possibile.</p>
<p>Enforced. I dati di condivisione delle applicazioni e del desktop devono essere crittografati. Qualora i dati non possano essere crittografati, la condivisione delle applicazioni e del desktop non sarà abilitata per la conversazione.</p>
<p>NotSupported. I dati di condivisione delle applicazioni e del desktop non verranno crittografati.</p></td>
</tr>
<tr class="odd">
<td><p><em>PlayAbbreviatedDialTone</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà visualizzato un segnale di linea di 3 secondi ogni volta che viene sganciato un ricevitore compatibile con Lync. Un ricevitore Lync è come un normale telefono che deve però essere collegato a una porta USB di un computer e utilizzato per le chiamate Lync e non per le &quot;normali&quot; telefonate. Se si imposta questo parametro su False, verrà visualizzato un segnale di linea di 30 secondi ogni volta che viene sganciato un ricevitore compatibile con Lync.</p>
<p>Questa impostazione è equivalente all'impostazione &quot;Riproduci segnale di linea abbreviato&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyEntry</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Consente di aggiungere impostazioni non previste dai parametri predefiniti. Ad esempio, per testare le versioni non definitive di Microsoft Lync Server 2010 era possibile aggiungere a Microsoft Lync 2010 l'opzione Commenti e suggerimenti. Era possibile eseguire l'operazione utilizzando un codice simile al seguente:</p>
<p>$x = New-CsClientPolicyEntry -Name &quot;OnlineFeedbackURL&quot; -Value &quot;http://www.litwareinc.com/feedback&quot;Set-CsClientPolicy -Identity global -PolicyEntry @{Add=$x}</p>
<p>Per ulteriori dettagli ed esempi, vedere l'argomento relativo al cmdlet <a href="new-csclientpolicyentry.md">New-CsClientPolicyEntry</a> nella Guida.</p></td>
</tr>
<tr class="odd">
<td><p><em>SearchPrefixFlags</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Consente di specificare quali attributi della Rubrica devono essere considerati quando si cerca un nuovo contatto. I valori del parametro SearchPrefixFlags vengono costruiti come numeri binari simili (ad esempio, 11101111) nei quali 1 e 0 indicano, rispettivamente, che quell'attributo va considerato per ricerca e non va considerato per la ricerca. Nel valore binario, gli attributi (da destra a sinistra) sono i seguenti:</p>
<p>Indirizzo di posta elettronica principale</p>
<p>Alias di posta elettronica</p>
<p>Tutti gli indirizzi di posta elettronica</p>
<p>Società</p>
<p>Nome visualizzato</p>
<p>Nome</p>
<p>Cognome</p>
<p>Il valore binario 1110111 sta ad indicare che per la ricerca vanno considerati tutti gli attributi meno l'attributo 4: Società. Per cercare solo il cognome, il nome e il nome visualizzato, il valore sarebbe:</p>
<p>1110000</p>
<p>Una volta costruito, il valore binario deve essere convertito in valore decimale per poter essere assegnato al parametro SearchPrefixFlags. Per convertire un numero binario in numero decimale, è possibile utilizzare un comando di Windows PowerShell simile al seguente:</p>
<p>[Convert]::ToInt32(&quot;1110111&quot;, 2)</p></td>
</tr>
<tr class="even">
<td><p><em>ShowManagePrivacyRelationships</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, verrà visualizzata l'opzione Relazioni nell'elenco contatti in Lync. Se invece si imposta il parametro su False, l'opzione Relazioni verrà nascosta.</p>
<p>Si noti che questa impostazione si applica solo a Lync 2010. In Lync 2013 queste relazioni non vengono visualizzate anche se ShowManagePrivacyRelationships è impostato su True.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowRecentContacts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Questo parametro non ha effetto sul client.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>ShowSharepointPhotoEditLink</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se si imposta questo parametro su True, Lync includerà un collegamento che consente agli utenti di modificare la foto personale archiviata nel proprio sito personale di Microsoft SharePoint. Il valore predefinito è False, con cui Lync non include un collegamento al sito personale di SharePoint.</p></td>
</tr>
<tr class="odd">
<td><p><em>SPSearchCenterExternalURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL esterno del sito di Microsoft SharePoint utilizzato per la ricerca tramite parole chiave, nota anche come ricerca avanzata. Questo URL verrà visualizzato nella parte inferiore di tutte le finestre dei risultati di ricerca tramite parole chiave in Lync. Se l'utente fa clic su questo URL, nel Web browser verrà visualizzato il sito di SharePoint in cui sarà possibile eseguire le ricerche sfruttando le funzionalità di ricerca di SharePoint. In SharePoint infatti sono disponibili più opzioni di ricerca rispetto a Lync.</p>
<p>SPSearchCenterExternalURL indica l'URL per gli utenti esterni, vale a dire per gli utenti che accedono al sistema dall'esterno del firewall dell'organizzazione Il parametro SPSearchCenterInternalURL è riservato agli utenti che accedono al sistema dall'esterno del firewall.</p></td>
</tr>
<tr class="even">
<td><p><em>SPSearchCenterInternalURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL interno del sito di Microsoft SharePoint utilizzato per la ricerca tramite parole chiave, nota anche come ricerca avanzata. Questo URL verrà visualizzato nella parte inferiore di tutte le finestre dei risultati di ricerca tramite parole chiave in Lync. Se l'utente fa clic su questo URL, nel Web browser verrà visualizzato il sito di SharePoint in cui sarà possibile eseguire le ricerche sfruttando le funzionalità di ricerca di SharePoint. In SharePoint infatti sono disponibili più opzioni di ricerca rispetto a Lync.</p>
<p>SPSearchCenterInternalURL indica l'URL per gli utenti interni, vale a dire per gli utenti che accedono al sistema dall'esterno del firewall dell'organizzazione. Il parametro SPSearchCenterExternalURL è riservato agli utenti che accedono al sistema dall'esterno del firewall.</p></td>
</tr>
<tr class="odd">
<td><p><em>SPSearchExternalURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL esterno del sito di Microsoft SharePoint utilizzato per la ricerca tramite parole chiave, nota anche come ricerca avanzata. In Lync viene utilizzato il sito di SharePoint indicato da questo URL ogni volta che un utente esterno, ovvero un utente che ha effettuato l'accesso al sistema dall'esterno del firewall dell'organizzazione, esegue una ricerca tramite parole chiave.</p></td>
</tr>
<tr class="even">
<td><p><em>SPSearchInternalURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL interno del sito di Microsoft SharePoint utilizzato per la ricerca tramite parole chiave, nota anche come ricerca avanzata. In Lync viene utilizzato il sito di SharePoint indicato da questo URL ogni volta che un utente interno, ovvero un utente che ha effettuato l'accesso al sistema dall'interno del firewall dell'organizzazione, esegue una ricerca tramite parole chiave.</p></td>
</tr>
<tr class="odd">
<td><p><em>TabURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Specifica il percorso del file XML utilizzato per creare le schede personalizzate posizionate nella parte inferiore della finestra dell'elenco contatti di Lync. Le schede personalizzate consentono di accedere alle pagine Web, ad esempio le pagine Web del team di supporto, da Lync. L'uso di questo parametro è deprecato con Lync Server 2013.</p>
<p>Questa impostazione equivale all'impostazione &quot;URL scheda Web&quot; di Criteri di gruppo in Communications Server 2007 R2.</p></td>
</tr>
<tr class="even">
<td><p><em>TracingLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Client.TracingLevel</p></td>
<td><p>Consente agli amministratori di gestire la traccia e la registrazione degli eventi in Lync 2013. I valori consentiti sono:</p>
<p>* Off: la traccia è disabilita e l'utente non può modificare questa impostazione.</p>
<p>* Light: vengono eseguite attività di traccia minime e l'utente non può modificare questa impostazione.</p>
<p>* Full: vengono eseguite attività di traccia dettagliate e l'utente non può modificare questa impostazione.</p>
<p>Per impostazione predefinita, il valore di TracingLevel è Light.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebServicePollInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Per gli utenti di Microsoft Exchange Server 2007 e versioni successive, il parametro WebServicePollInterval specifica la frequenza con cui Lync recupera i dati di calendario dai servizi Web di Microsoft Exchange Server. È possibile impostare WebServicePollInterval su un valore compreso tra 1 secondo e 1 ora, estremi inclusi. Per configurare l'intervallo di polling dei servizi Web, utilizzare il formato ore:minuti:secondi. Il comando seguente imposta ad esempio l'intervallo di polling dei servizi Web su 45 minuti:</p>
<p>-WebServicePollInterval 00:45:00</p>
<p>Si noti che questa impostazione non si applica agli utenti il cui account di posta elettronica si trova in Exchange 2003. Per questi utenti, il recupero dei dati del calendario è gestito tramite il parametro MAPIPollInterval.</p>
<p>Questa impostazione equivale all'impostazione &quot;Intervallo di tempo per il caricamento dei dati del calendario dal provider di servizi Web&quot; di Criteri di gruppo di Communications Server 2007 R2.</p></td>
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

Nessuno. Il cmdlet **New-CsClientPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsClientPolicy** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Client.ClientPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientPolicy](get-csclientpolicy.md)  
[Grant-CsClientPolicy](grant-csclientpolicy.md)  
[New-CsClientPolicyEntry](new-csclientpolicyentry.md)  
[Remove-CsClientPolicy](remove-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

