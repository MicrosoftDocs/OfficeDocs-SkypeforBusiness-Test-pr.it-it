---
title: Test-CsAudioConferencingProvider
TOCTitle: Test-CsAudioConferencingProvider
ms:assetid: 9e00081e-5825-4ee9-a838-3c91ad054589
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205117(v=OCS.15)
ms:contentKeyID: 49301474
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAudioConferencingProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se un utente può connettersi al proprio provider di servizi di audioconferenza. Un provider di servizi di audioconferenza è una società terza che fornisce servizi di conferenza alle organizzazioni. Tra l'altro, i provider di servizi di audioconferenza consentono agli utenti in trasferta, che non sono connessi alla rete aziendale o a Internet, di accedere ai contenuti audio di una conferenza o di una riunione. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsAudioConferencingProvider -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAudioConferencingProvider -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAudioConferencingProvider [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-DialoutUserCredential <PSCredential>] [-DialoutUserSipAddress <String>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Esempi

## Esempio 1

Nell'esempio 1 viene verificato se un utente di test definito per il pool atl-cs-001.litwareinc.com può connettersi al relativo provider di servizi di audioconferenza. Questo comando richiede che per il pool sia definito almeno un utente di test. Se non sono stati definiti utenti di test per atl-cs-001.litwareinc.com, il comando avrà esito negativo in quanto il cmdlet **Test-CsAudioConferencingProvider** non individua l'utente da utilizzare nella verifica. Se non sono stati definiti utenti di test per un pool, è necessario includere il parametro UserSipAddress e le credenziali dell'account utente che il comando dovrà utilizzare per verificare la connessione a un provider di servizi di audioconferenza.

    Test-CsAudioConferencingProvider -TargetFqdn atl-cs-001.litwareinc.com

## Esempio 2

I comandi riportati nell'esempio 2 verificano se un utente specifico (litwareinc\\kenmyer) è in grado di connettersi al proprio provider di servizi di audioconferenza. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell contenente il nome e la password dell'utente Ken Myer. Dal momento che il nome di accesso litwareinc\\kenmyer è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà solo immettere la password dell'account di Ken Myer. L'oggetto credenziali risultante viene archiviato in una variabile denominata $credential.

Il secondo comando verifica quindi se questo utente può connettersi al proprio provider di servizi di audioconferenza. A tale scopo, viene chiamato il cmdlet **Test-CsAudioConferencingProvider** con tre parametri, ovvero TargetFqdn (il nome di dominio completo del pool di registrazione), UserCredential (l'oggetto di Windows PowerShell contenente le credenziali utente di Ken Myer) e UserSipAddress (l'indirizzo SIP corrispondente alle credenziali utente fornite).

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAudioConferencingProvider -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## Descrizione dettagliata

Un provider di servizi di audioconferenza è una società terza che fornisce servizi di conferenza alle organizzazioni. Tra l'altro, i provider di servizi di audioconferenza consentono agli utenti in trasferta, non connessi alla rete aziendale o a Internet, di accedere ai contenuti audio di una conferenza o di una riunione. Tali provider offrono spesso servizi di qualità elevata come traduzione immediata, trascrizione e assistenza diretta di un operatore durante la conferenza.

Il cmdlet **Test-CsAudioConferencingProvider** viene utilizzato per verificare che un utente sia in grado di effettuare una connessione al proprio provider di servizi di audioconferenza. Questo cmdlet può essere eseguito in due modi. Molti amministratori utilizzeranno i cmdlet CsHealthMonitoringConfiguration per configurare utenti di test per ognuno dei propri pool di registrazione. Questi utenti di test sono costituiti da due account utente preconfigurati per l'utilizzo con le transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti reali. Se per un pool sono configurati utenti di test, gli amministratori possono eseguire il cmdlet **Test-CsAudioConferencingProvider** per tale pool senza dover specificare l'identità e fornire le credenziali dell'account utente coinvolto nella verifica.

In alternativa, gli amministratori possono eseguire il cmdlet **Test-CsAudioConferencingProvider** utilizzando un account utente reale. In questo caso, è necessario specificare nome di accesso e password dell'account.

La verifica avrà esito negativo se all'utente utilizzato dal cmdlet **Test-CsAudioConferencingProvider** non è stato assegnato un provider di servizi di audioconferenza.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Test-CsAudioConferencingProvider** i membri dei gruppi seguenti: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAudioConferencingProvider"}

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
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da verificare.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente dell'account da verificare. Il valore passato a UserCredential deve essere un riferimento oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Ad esempio, il codice seguente restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e lo archivia in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Questo parametro non è necessario se il comando sta utilizzando utenti di test configurati con i cmdlet CsHealthMonitoringConfiguration.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato durante l'esecuzione della verifica. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>DialoutUserCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente chiamate in uscita che deve essere verificato. Il valore passato a DialoutUserCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, il codice seguente restituisce un oggetto credenziali per l'utente litwareinc\pilar e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>DialoutUserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'account utente chiamate in uscita da che deve essere verificato. Ad esempio: -DialoutUserSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro DialoutUserSipAddress deve fare riferimento allo stesso account utente di DialoutUserCredential.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome della variabile.</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre il carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se presente, verifica la possibilità di Join Launcher di partecipare a una conferenza. Join Launcher viene utilizzato per facilitare la partecipazione degli utenti di dispositivi mobili, e di conseguenza degli utenti del servizio per dispositivi mobili, alle conferenze.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'account utente da verificare. Ad esempio: -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro UserSipAddress deve fare riferimento allo stesso account utente di UserCredential.</p>
<p>Questo parametro non è necessario se il comando sta utilizzando utenti di test configurati con i cmdlet CsHealthMonitoringConfiguration.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsAudioConferencingProvider** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsAudioConferencingProvider** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

