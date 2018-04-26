---
title: Test-CsWebAppAnonymous
TOCTitle: Test-CsWebAppAnonymous
ms:assetid: acfb28c1-8db6-4d2b-95ad-5c824660ea71
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690041(v=OCS.15)
ms:contentKeyID: 49301652
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsWebAppAnonymous

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che gli utenti anonimi possano utilizzare Lync Web App per partecipare a una conferenza di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

L'utilizzo di questo cmdlet è deprecato con la versione locale di Lync Server 2013.

## Sintassi

    Test-CsWebAppAnonymous -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsWebAppAnonymous -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsWebAppAnonymous -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 verifica se un utente di test configurato per il pool atl-cs-001.litwareinc.com può utilizzare Lync Web App per partecipare in modo anonimo a una conferenza. Questo comando ha esito positivo solo se è stato configurato un utente di test per il pool utilizzando i cmdlet **CsHealthMonitoringConfiguration**.

    Test-CsWebAppAnonymous -TargetFqdn atl-cs-001.litwareinc.com

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se l'utente Ken Myer può utilizzare o meno Lync Web App per partecipare in modo anonimo a una conferenza. Per utilizzare un account utente reale, nel primo comando dell'esempio viene eseguito il cmdlet **Get-Credential** per creare un oggetto credenziali di Windows PowerShell per l'utente litwareinc\\kenmyer. Tale oggetto credenziali, archiviato in una variabile denominata $cred1, viene quindi passato al parametro UserCredential nel secondo comando nell'esempio. Oltre al parametro UserCredential, viene incluso anche il parametro UserSipAddress, insieme all'indirizzo SIP di Ken Myer.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsWebApp -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1 

## Descrizione dettagliata

Il cmdlet **Test-CsWebAppAnonymous** consente agli amministratori di verificare che gli utenti anonimi possano utilizzare Microsoft Exchange Server 2013 per partecipare alle conferenze. Quando viene eseguito, il cmdlet **Test-CsWebAppAnonymous** tenta di ottenere un ticket Web anonimo utilizzando il servizio Ticket Web. Se è possibile ottenere il ticket, il cmdlet **Test-CsWebAppAnonymous** tenta quindi di connettersi a Lync Server tramite Lync Web App. Se la connessione viene stabilita, il cmdlet tenta di stabilire conferenze distinte per messaggistica istantanea, condivisione applicazioni e collaborazione dati.

Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ognuno dei propri pool di registrazione. Questi utenti di test sono costituiti da due account utente preconfigurati per l'utilizzo con le transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti reali. Se sono stati configurati utenti di test per un pool, gli amministratori possono eseguire il cmdlet **Test-CsWebAppAnonymous** per tale pool senza dover specificare le identità degli account utente coinvolti nel test e fornire le relative credenziali.

In alternativa, gli amministratori possono eseguire il cmdlet **Test-CsWebAppAnonymous** utilizzando un account utente reale. In questo caso, è necessario specificare nome di accesso e password dell'account.

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
<td><p>Nome di dominio completo (FQDN) del pool da testare. Ad esempio:</p>
<p>-TargetFqdn atl-cs-001.litwareinc.com</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>URI (Uniform Resource Identifier) di Reach Server. Ad esempio:</p>
<p>-TargetUri &quot;https://atl-cs-001.litwareinc.com/reach&quot;</p>
<p>Non è possibile utilizzare il parametro TargetUri e il parametro TargetFqdn nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti di test configurati tramite i cmdlet <strong>CsHealthMonitoringConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato durante l'esecuzione della verifica. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Quando presente, tramite il cmdlet <strong>Test-CsWebAppAnonymous</strong> viene testato il server Web di inoltro esterno di Reach Server. Se questo parametro non è presente, tramite il cmdlet viene testato il server Web di inoltro interno. Il server Web di inoltro funge da intermediario tra la rete interna e Internet.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non irreversibile che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
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
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del primo dei due account utente da testare. Ad esempio:</p>
<p>-UserSipAddress &quot;sip:davidegarghentini@litwareinc.com&quot;</p>
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti test configurati tramite i cmdlet CsHealthMonitoringConfiguration.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente da utilizzare nel test. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\davidegarghentini e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>Questo parametro è obbligatorio se è stato specificato il parametro TargetUri o UserSipAddress e se il computer in cui viene eseguito il comando non dispone di un certificato del server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Test-CsWebAppAnonymous** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

