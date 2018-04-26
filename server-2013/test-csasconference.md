---
title: Test-CsASConference
TOCTitle: Test-CsASConference
ms:assetid: bf926005-1146-484c-90fa-246a9c082774
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205227(v=OCS.15)
ms:contentKeyID: 49301835
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsASConference

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che due utenti possano partecipare a una conferenza di condivisione applicazioni. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsASConference -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsASConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsASConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 verifica che sia possibile tenere una conferenza di condivisione applicazioni nel pool atl-cs-001.litwareinc.com. Nel comando si presuppone che sia stata configurata una coppia di utenti di test per il pool specificato. Se non esistono utenti di test, il comando avrà esito negativo.

    Test-CsASConference -TargetFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'esempio 2 viene verificato che il servizio Join Launcher possa partecipare a una conferenza di condivisione applicazioni nel pool atl-cs-001.litwareinc.com. Questo comando verifica solo il servizio. Non è necessario alcun dispositivo mobile per eseguire il comando.

    Test-CsASConference -TargetFqdn "atl-cs-001.litwareinc.com" -TestJoinLauncher

## Esempio 3

I comandi riportati nell'esempio 2 verificano se due utenti (litwareinc\\pilar e litwareinc\\kenmyer) sono in grado di accedere a Lync Server 2013 e quindi partecipare a una conferenza di condivisione applicazioni. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché il nome di accesso litwareinc\\pilar è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà solo immettere la password dell'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1. Il secondo comando effettua la stessa operazione, questa volta restituendo un oggetto credenziali per l'account di Ken Myer.

Con gli oggetti credenziali disponibili, il terzo comando determina se i due utenti possono accedere a Lync Server 2013 e tenere una conferenza di condivisione applicazioni. A tale scopo, viene chiamato il cmdlet **Test-CsASConference** con i parametri seguenti: TargetFqdn (FQDN del pool di registrazione), SenderSipAddress (indirizzo SIP del primo utente test), SenderCredential (oggetto di Windows PowerShell contenente le credenziali di questo stesso utente), ReceiverSipAddress (indirizzo SIP dell'altro utente test) e ReceiverCredential (oggetto di Windows PowerShell contenente le credenziali dell'altro utente test).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsASConference -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsASConference** verifica che due utenti test possano partecipare a una conferenza online che prevede la condivisione applicazioni. A tale scopo, il cmdlet registra i due utenti in Lync Server 2013 e quindi utilizza uno degli account utente per creare una nuova conferenza che include la condivisione applicazioni. Il cmdlet verifica quindi che il secondo utente sia in grado di partecipare alla conferenza.

Si noti che questo comando avrà esito negativo se agli utenti test è stato assegnato un criterio conferenza che impedisce loro di utilizzare la condivisione applicazioni.

Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsASConference"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Test-CsASConference non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore passato a ReceiverCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente, ad esempio, restituisce un oggetto credenziali per l'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali del destinatario non sono necessarie se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore passato a SenderCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziali per l'utente litwareinc\kenmyer e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali del mittente non sono necessarie se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da verificare.</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
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
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del primo dei due account utente da testare. Ad esempio: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro ReceiverSIPAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP del secondo dei due account utente da sottoporre a test. Ad esempio: -SenderSipAddress &quot;sip:davidegarghentini@litwareinc.com&quot;. Il parametro SenderSipAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se presente, verifica la possibilità di Join Launcher di partecipare a una conferenza. Join Launcher viene utilizzato per facilitare la partecipazione degli utenti di dispositivi mobili, e di conseguenza degli utenti del servizio per dispositivi mobili, alle conferenze.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsASConference** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsASConference** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[Test-CsDataConference](test-csdataconference.md)

