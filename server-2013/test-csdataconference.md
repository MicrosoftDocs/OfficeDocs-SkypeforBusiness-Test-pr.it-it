---
title: Test-CsDataConference
TOCTitle: Test-CsDataConference
ms:assetid: bd7f3c98-7b10-494e-adce-a9b20428b6cc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205219(v=OCS.15)
ms:contentKeyID: 49301816
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDataConference

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di due utenti di partecipare o meno a una conferenza Web di Lync Server 2013 che include attività quali la condivisione o la visualizzazione di diapositive di PowerPoint, lavagne o sondaggi. Il cmdlet verifica inoltre che il servizio Web Conferencing di Lync Server sia in grado di rilevare Office Web Apps Server e che un client possa caricare un file di PowerPoint da trasmettere tramite Office Web Apps Server.

Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsDataConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsDataConference -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsDataConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 verifica che sia possibile tenere una conferenza dati nel pool atl-cs-001.litwareinc.com. Nel comando si presuppone che sia stata configurata una coppia di utenti di test per il pool specificato. Se non esistono utenti di test, il comando avrà esito negativo.

    Test-CsDataConference -TargetFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

I comandi riportati nell'esempio 2 verificano la capacità di due utenti (litwareinc\\pilar e litwareinc\\kenmyer) di accedere a Lync Server 2013 e quindi eseguire una conferenza dati. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché il nome di accesso litwareinc\\pilar è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà immettere esclusivamente la password dell'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1. Il secondo comando effettua la stessa operazione, questa volta restituendo un oggetto credenziali per l'account di Ken Myer.

Con gli oggetti credenziali disponibili, il terzo comando determina se i due utenti possono accedere a Lync Server 2013 ed eseguire una conferenza dati. A tale scopo, viene chiamato il cmdlet **Test-CsDataConference** con i parametri seguenti: TargetFqdn (nome di dominio completo del pool di registrazione), SenderSipAddress (indirizzo SIP del primo utente di test), SenderCredential (oggetto di Windows PowerShell contenente le credenziali di questo stesso utente), ReceiverSipAddress (indirizzo SIP dell'altro utente di test) e ReceiverCredential (oggetto di Windows PowerShell contenente le credenziali dell'altro utente di test).

    $credential1 = Get-Credential "litwareinc\pilar"
    $credential2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsDataConference -TargetFqdn "atl-cs-001.litwareinc.com" -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $credential1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $credential2

## Descrizione dettagliata

In Lync Server 2013 per conferenza dati si intende una conferenza in cui vengono utilizzate attività quali lavagne o annotazioni. Il cmdlet **Test-CsDataConference** consente di verificare la capacità di due utenti di partecipare a una conferenza di questo tipo.

La capacità di eseguire una conferenza dati dipende dal criterio conferenza assegnato all'utente che ha organizzato la conferenza (nel caso del cmdlet **Test-CsDataConference**, il "mittente"). Se l'organizzatore non è autorizzato a includere attività di collaborazione nella riunione (ad esempio se la proprietà EnableDataCollaboration del relativo criterio conferenza è impostata su False), il cmdlet **Test-CsDataConference** avrà esito negativo.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDataConference"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsDataConference** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore passato a ReceiverCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente ad esempio restituisce un oggetto credenziali dell'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali del destinatario non sono necessarie se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore passato a SenderCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziali per l'utente litwareinc\kenmyer e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali del mittente non sono necessarie se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool di Chat persistente da verificare.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato durante l'esecuzione della verifica. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre un carattere $ quando si specifica il nome della variabile.</p>
<p>Per salvare le informazioni archiviate nella variabile del logger su un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando analogo al seguente:</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP del primo dei due account utente da verificare. Ad esempio:</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>Il parametro ReceiverSIPAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è necessario se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP del secondo dei due account utente da verificare. Ad esempio:</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Il parametro SenderSipAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, verifica la possibilità di Join Launcher di partecipare a una conferenza. Join Launcher viene utilizzato per facilitare la partecipazione degli utenti di dispositivi mobili, e di conseguenza degli utenti del servizio per dispositivi mobili, alle conferenze.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsDataConference** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Test-CsDataConference** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsASConference](test-csasconference.md)

