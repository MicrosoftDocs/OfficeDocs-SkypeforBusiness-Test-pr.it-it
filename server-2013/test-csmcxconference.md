---
title: Test-CsMcxConference
TOCTitle: Test-CsMcxConference
ms:assetid: c6ca9019-1535-489d-a42e-1a50070b2f67
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690045(v=OCS.15)
ms:contentKeyID: 49301947
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsMcxConference

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la possibilità per tre utenti di partecipare a una conferenza del servizio per dispositivi mobili di Lync Server 2013. Il servizio per dispositivi mobili consente agli utenti di cellulari come iPhone e Windows Phone di eseguire operazioni quali lo scambio di messaggi istantanei e di informazioni sulla presenza, l'archiviazione e il recupero dei messaggi in segreteria telefonica internamente anziché tramite il provider wireless e l'utilizzo di funzionalità di Lync Server come Chiamata tramite ufficio e le conferenze telefoniche con chiamata esterna. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Test-CsMcxConference -OrganizerCredential <PSCredential> -OrganizerSipAddress <String> -User2Credential <PSCredential> -User2SipAddress <String> -UserCredential <PSCredential> -UserSipAddress <String> <COMMON PARAMETERS>

    Test-CsMcxConference -OrganizerSipAddress <String> -User2SipAddress <String> -UserSipAddress <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -TargetFqdn <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 consente di verificare se è possibile svolgere una conferenza del servizio per dispositivi mobili utilizzando tre account utente: Davide Garghentini, l'organizzatore della riunione, Pilar Ackerman e Aidan Delaney. Per eseguire questo test, è innanzitutto necessario creare oggetti credenziali per ogni account utente. Questi oggetti vengono creati nelle prime tre righe di codice e archiviati nelle variabili $organizerCred (Ken Myer), $user1Cred (Pilar Ackerman) e $user2Cred (Aidan Delaney).

Dopo la creazione degli oggetti credenziali, viene chiamato il cmdlet **Test-CsMcxConference** specificando il pool di registrazione di destinazione (atl-cs-001.litwareinc.com), il tipo di autenticazione (Negoziazione), nonché gli indirizzi SIP e le credenziali dei tre account utente che partecipano alla conferenza.

    $organizerCred = Get-Credential "litwareinc\kenmyer"
    $user1Cred = Get-Credential "litwareinc\packerman"
    $user2Cred = Get-Credential "litwareinc\adelaney"
    
    Test-CsMcxConference -TargetFqdn "atl-cs-001.litwareinc.com" -Authentication Negotiate -OrganizerSipAddress "sip:kenmyer@litwareinc.com" -OrganizerCredential $organizerCred -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $user1Cred -User2SipAddress "sip:adelaney@litwareinc.com" -User2Credential $user2Cred

## Descrizione dettagliata

Il servizio per dispositivi mobili estende numerose funzionalità di Lync Server a dispositivi mobili come Apple iPhone, Windows Phone, telefoni Android e telefoni Nokia. Gli utenti possono tra l'altro utilizzare questi telefoni per scambiare messaggi istantanei e informazioni sulla presenza e per ricevere notifiche di nuovi messaggi in segreteria telefonica. Grazie al servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft), gli utenti con telefoni iPhone o Windows Phone possono ricevere queste notifiche anche se Lync è in esecuzione in background. Il servizio per dispositivi mobili consente inoltre alle organizzazioni di abilitare la caratteristica Chiamata tramite ufficio. Con questa caratteristica, gli utenti possono effettuare una chiamata dal proprio cellulare e fare in modo che risulti provenire dal telefono dell'ufficio. Ad esempio, tramite i sistemi ID chiamante verrà visualizzato il numero dell'ufficio dell'utente anziché il numero del relativo cellulare.

Il cmdlet **Test-CsMcxConference** viene utilizzato per determinare se un gruppo di tre utenti può partecipare a una conferenza utilizzando il servizio per dispositivi mobili. Si noti che l'esecuzione di questo cmdlet non richiede l'utilizzo di telefoni cellulari né comporta la creazione di una vera conferenza. Il cmdlet verifica invece che i tre utenti possano accedere a Lync Server e che tramite il servizio per dispositivi mobili possano essere stabilite le connessioni necessarie per svolgere una conferenza. Il cmdlet verifica inoltre che l'organizzatore della conferenza possa inviare un messaggio istantaneo agli altri due partecipanti.

Quali utenti sono autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Test-CsMcxConference** localmente: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato sui ruoli (RBAC) a cui questo cmdlet è stato assegnato, inclusi i ruoli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsMcxConference"}

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
<td><p><em>Authentication</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>I valori consentiti sono: TrustedServer; Negotiate; ClientCertificate; LiveID.</p></td>
</tr>
<tr class="even">
<td><p><em>OrganizerCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente che funge da organizzatore della riunione. Il valore passato a OrganizerCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente, ad esempio, restituisce un oggetto credenziali per l'utente litwareinc\adelaney e archivia tale oggetto in una variabile denominata $z:</p>
<p>$z = Get-Credential &quot;litwareinc\adelaney&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>OrganizerSipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP per l'account utente che funge da organizzatore della riunione. Ad esempio:</p>
<p>-OrganizerSipAddress &quot;sip:adelaney@litwareinc.com&quot;</p>
<p>Il parametro OrganizerSipAddress deve fare riferimento allo stesso account utente del parametro OrganizerCredential.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da testare.</p></td>
</tr>
<tr class="odd">
<td><p><em>User2Credential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore passato a Use2rCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\davidegarghentini e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="even">
<td><p><em>User2SipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del secondo dei due account utente da testare. Ad esempio:</p>
<p>-User2SipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>Il parametro User2SipAddress deve fare riferimento allo stesso account utente di User2Credential.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del primo dei due account utente da testare. Ad esempio:</p>
<p>-UserSipAddress &quot;sip:davidegarghentini@litwareinc.com&quot;</p>
<p>Il parametro UserSipAddress deve fare riferimento allo stesso account utente del parametro UserCredential.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre il carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsMcxConference** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsMcxConference** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

