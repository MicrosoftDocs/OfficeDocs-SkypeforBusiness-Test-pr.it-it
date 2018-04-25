---
title: Test-CsWebApp
TOCTitle: Test-CsWebApp
ms:assetid: 0333a4a5-9bd5-4a45-aea8-e7af1a394ec3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh689989(v=OCS.15)
ms:contentKeyID: 49299514
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsWebApp

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che gli utenti autenticati possano utilizzare Lync Web App per partecipare a una conferenza di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

L'utilizzo di questo cmdlet è deprecato con la versione locale di Lync Server 2013. In alternativa, gli amministratori dovrebbero utilizzare i cmdlet [Test-CsUcwaConference](test-csucwaconference.md) per eseguire questi test.

## Sintassi

    Test-CsWebApp -User2Credential <PSCredential> -User2SipAddress <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsWebApp -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsWebApp -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene verificato se una coppia di utenti di test configurati per il pool atl-cs-001.litwareinc.com può utilizzare Lync Web App per partecipare a una conferenza. Questo comando ha esito positivo solo se sono stati configurati utenti di test per il pool utilizzando i cmdlet **CsHealthMonitoringConfiguration**.

    Test-CsWebApp -TargetFqdn atl-cs-001.litwareinc.com

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se gli utenti Ken Myer e Pilar Ackerman possono utilizzare Lync Web App per partecipare a una conferenza. Per utilizzare account utente effettivi, nei primi due comandi dell'esempio viene utilizzato il cmdlet Get-Credential per creare oggetti credenziali dell'interfaccia della riga di comando Windows PowerShell per i due utenti (litwareinc\\kenmyer e litwareinc\\pilar). Tali oggetti credenziali (archiviati nelle variabili $cred1 e $cred2) vengono quindi utilizzati come valori per i parametri UserCredential e User2Credential nel comando finale dell'esempio. Oltre ai parametri delle credenziali utente, sono inclusi i parametri UserSipAddress e User2SipAddress, insieme agli indirizzi SIP dei due account utente utilizzati nel test.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    $cred2 = Get-Credential "litwareinc\pilar"
    
    Test-CsWebApp -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1 -User2SipAddress "sip:pilar@litwareinc.com" -User2Credential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsWebApp** consente agli amministratori di verificare che gli utenti autenticati possano utilizzare Lync Web App per partecipare alle conferenze. Quando si esegue il cmdlet **Test-CsWebApp**, il cmdlet tenta di ottenere i ticket Web per una coppia di utenti di test utilizzando il servizio Ticket Web. Se è possibile ottenere i ticket e autenticare gli utenti di test, il cmdlet **Test-CsWebApp** tenta quindi di connettersi a Lync Server tramite Lync Web App. Se la connessione viene stabilita, il cmdlet tenta quindi di stabilire conferenze distinte per messaggistica istantanea, condivisione applicazioni e collaborazione dati.

Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ognuno dei propri pool di registrazione. Questi utenti di test rappresentano una coppia di account utente preconfigurati per l'utilizzo con le transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti effettivi. Se gli utenti di test sono configurati per un pool, gli amministratori possono eseguire il cmdlet **Test-CsWebApp** su tale pool senza dover specificare le identità degli account utente coinvolti nel test né fornire le relative credenziali.

In alternativa, gli amministratori possono eseguire il cmdlet **Test-CsWebApp** utilizzando account utente effettivi. In questo caso, per eseguire il test, è necessario specificare nome di accesso e password per ogni account.

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
<td><p><em>User2Credential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore passato a User2Credential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce ad esempio un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="even">
<td><p><em>User2SipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del secondo dei due account utente da testare. Ad esempio:</p>
<p>-User2SipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti di test configurati tramite i cmdlet <strong>CsHealthMonitoringConfiguration</strong>.</p></td>
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
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato quando si esegue il test. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Quando presente, consente al cmdlet <strong>Test-CsWebApp</strong> di testare il relay Web esterno di Reach Server. Se questo parametro non è presente, il cmdlet testa il relay Web interno. Il relay Web funge da intermediario tra la rete interna e Internet.</p></td>
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
<td><p>Quando si specifica questo parametro, l'output dettagliato relativo all'esecuzione del cmdlet viene archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
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
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti test configurati tramite i cmdlet CsHealthMonitoringConfiguration.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente da utilizzare nel test. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Questo parametro è obbligatorio se è stato specificato il parametro TargetUri o UserSipAddress/User2SipAddress e se il computer in cui viene eseguito il comando non dispone di un certificato del server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Test-CsWebApp** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

