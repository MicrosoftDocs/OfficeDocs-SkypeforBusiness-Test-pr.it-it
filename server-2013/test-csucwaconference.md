---
title: Test-CsUcwaConference
TOCTitle: Test-CsUcwaConference
ms:assetid: 4e01c4d6-7b81-4932-a8e1-4d14989b71bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619178(v=OCS.15)
ms:contentKeyID: 49300489
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsUcwaConference

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di due utenti di pianificare, partecipare e condurre una conferenza online utilizzando UCWA (Unified Communications Web API). Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsUcwaConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-OrganizerSipAddress <String>] [-ParticipantSipAddress <String>] [-RegistrarPort <Int32>] <COMMON PARAMETERS>

    Test-CsUcwaConference -OrganizerCredential <PSCredential> -OrganizerSipAddress <String> -ParticipantCredential <PSCredential> -ParticipantSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsUcwaConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-ParticipantSipAddress <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 verifica che due utenti test possano partecipare a una conferenza UCWA nel pool atl-cs-001.litwareinc.com. Si noti che questo comando avrà esito negativo se non è stata predefinita una coppia di utenti test per la configurazione del monitoraggio dello stato per atl-cs-001.litwareinc.com.

    Test-CsUcwaConference -TargetFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

I comandi riportati nell'esempio 2 verificano la capacità di due utenti (litwareinc\\pilar e litwareinc\\kenmyer) di partecipare a una conferenza UCWA. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché il nome di accesso, litwareinc\\pilar, è stato incluso come parametro, la finestra di dialogo Richiesta credenziali di Windows PowerShell richiede solo che l'amministratore immetta la password dell'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1. Il secondo comando effettua la stessa operazione, questa volta restituendo un oggetto credenziali per l'account di Ken Myer.

Con i due oggetti credenziali disponibili, il terzo comando dell'esempio determina se i due utenti sono o meno in grado di partecipare a una conferenza UCWA. A tale scopo, viene chiamato il cmdlet **Test-CsUcwaConference** con i parametri seguenti: TargetFqdn (nome di dominio completo del pool di registrazione), OrganizerSipAddress (indirizzo SIP dell'organizzatore della riunione), OrganizerCredential (oggetto di Windows PowerShell contenente le credenziali per questo stesso utente), ParticipantSipAddress (indirizzo SIP dell'altro utente di test) e ParticipantCredential (oggetto dell'interfaccia della riga di comando Windows PowerShell contenente le credenziali dell'altro utente).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsUcwaConference -TargetFqdn atl-cs-001.litwareinc.com -OrganizerSipAddress "sip:pilar@litwareinc.com" -OrganizerCredential $cred1 -ParticipantSipAddress "sip:kenmyer@litwareinc.com" -ParticipantCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsUcwaConference** verifica che due utenti di test possano pianificare, partecipare e condurre una conferenza online utilizzando UCWA (Unified Communications Web API). A tale scopo, il cmdlet utilizza il servizio ticket Web di Lync Server per autenticare i due utenti di test e registrarli in Lync Server. Il cmdlet quindi avvia una conferenza utilizzando le credenziali dell'organizzatore e invita l'utente a partecipare alla riunione. Dopo l'accesso alla riunione, il cmdlet **Test-CsUcwaConference** verifica che gli utenti possano eseguire operazioni quali lo scambio di messaggi istantanei e la conduzione di pool, quindi termina la conferenza e annulla la registrazione dei due utenti di test. La conferenza pianificata inoltre verrà eliminata al termine del test.

Il cmdlet **Test-CsUcwaConference** inoltre può essere utilizzato per determinare se gli utenti anonimi possono o meno partecipare a conferenze online.

Si noti che il cmdlet **Test-CsUcwaConference** non deve essere eseguito su un pool di Microsoft Lync Server 2010, a meno che l'installazione di UCWA non sia stata effettuata in tale pool. Se l'installazione di UCWA non è stata eseguita, la chiamata al cmdlet **Test-CsUcwaConference** avrà esito negativo.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsUcwaConference"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsUcwaConference** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>OrganizerCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente che funge da organizzatore della riunione. Il valore passato a OrganizerCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali di organizzatore non sono necessarie se si sta eseguendo il test con le impostazioni di configurazione del monitoraggio dello stato del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipantCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente che funge da partecipante della riunione. Il valore passato a ParticipantCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il seguente codice restituisce ad esempio un oggetto credenziali per l'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali di partecipante non sono necessarie se si sta eseguendo il test con le impostazioni di configurazione del monitoraggio dello stato del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da testare.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato per l'esecuzione del test. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OrganizerSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'organizzatore della riunione. Ad esempio: -OrganizerSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro OrganizerSIPAddress deve fare riferimento allo stesso account utente di OrganizerCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue il test con le impostazioni di configurazione per il monitoraggio dell'integrità del pool.</p></td>
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
<td><p><em>ParticipantSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del partecipante della riunione. Ad esempio: -ParticipantSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro ParticipantSIPAddress deve fare riferimento allo stesso account utente di ParticipantCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue il test con le impostazioni di configurazione per il monitoraggio dell'integrità del pool.</p></td>
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

Nessuno. Il cmdlet **Test-CsUcwaConference** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsUcwaConference** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.WebTaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsASConference](test-csasconference.md)  
[Test-CsDataConference](test-csdataconference.md)  
[Test-CsAVConference](test-csavconference.md)

