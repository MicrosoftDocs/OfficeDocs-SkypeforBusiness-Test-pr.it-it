---
title: Test-CsExUMVoiceMail
TOCTitle: Test-CsExUMVoiceMail
ms:assetid: 88734ae8-1339-4080-a4bb-544181f6d1d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205058(v=OCS.15)
ms:contentKeyID: 49301242
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExUMVoiceMail

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se un utente può connettersi al servizio Messaggistica unificata di Exchange e lasciare un messaggio in segreteria telefonica per un altro utente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsExUMVoiceMail -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-WaveFile <String>] <COMMON PARAMETERS>

    Test-CsExUMVoiceMail -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] [-WaveFile <String>] <COMMON PARAMETERS>

    Test-CsExUMVoiceMail [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## Esempio 1

Nell'esempio seguente viene verificata la connettività della segreteria telefonica della messaggistica unificata di Exchange per il pool atl-cs-001.litwareinc.com. Questo comando potrà essere eseguito correttamente solo se sono stati definiti utenti di test per il pool atl-cs-001.litwareinc.com. In questo caso, il comando consente di stabilire se il primo utente di test è in grado di utilizzare la segreteria telefonica della messaggistica unificata. Se gli utenti di test non sono stati configurati per il pool, il comando avrà esito negativo.

    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com"

## Esempio 2

I comandi riportati nell'esempio 2 verificano la connettività della segreteria telefonica della messaggistica unificata di Exchange per l'utente litwareinc\\kenmyer. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell per l'utente litwareinc\\kenmyer. È necessario fornire la password di tale account per creare un oggetto credenziali valido ed essere certi che il cmdlet **Test-CsExUMVoiceMail** possa eseguire tale verifica.

Nel secondo comando dell'esempio vengono utilizzati l'oggetto credenziali fornito ($x) e l'indirizzo SIP dell'utente litwareinc\\kenmyer per determinare se l'utente può connettersi alla segreteria telefonica della messaggistica unificata di Exchange.

    $credential = Get-Credential "litwareinc\pilar"
    
    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $credential

## Esempio 3

Il comando riportato nell'esempio 3 è una variante del comando riportato nell'esempio 1. In questo caso, viene però incluso il parametro OutLoggerVariable per generare un log dettagliato di ogni passaggio eseguito dal cmdlet **Test-CsExUMVoiceMail**, nonché dell'esito positivo o negativo di ognuno di tali passaggi. A tale scopo, il parametro OutLoggerVariable viene aggiunto insieme al valore ExumText, in modo che le informazioni di registrazione dettagliate vengano archiviate in una variabile denominata $ExumTest. Nel comando finale dell'esempio viene utilizzato il metodo ToXML() per convertire le informazioni del log nel formato XML. Tali dati XML vengono quindi scritti in un file denominato C:\\Logs\\VoicemailTest.xml mediante il cmdlet Out-File.

    Test-CsExUMVoiceMail -TargetFqdn "atl-cs-001.litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -OutLoggerVariable VoicemailTest
    
    $VoicemailTest.ToXML() | Out-File C:\Logs\VoicemailTest.xml

## Descrizione dettagliata

Il cmdlet **Test-CsExUMVoiceMail** consente agli amministratori di verificare che un utente sia in grado di accedere al servizio Messaggistica unificata di Microsoft Exchange Server 2013 e di utilizzarlo. A tale scopo, il cmdlet si connette al servizio Messaggistica unificata di Exchange e lascia un messaggio in segreteria telefonica nella cassetta postale specificata. Il messaggio può essere fornito dal sistema o essere contenuto in un file WAV personalizzato registrato personalmente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExUMVoiceMail"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Test-CsExUMVoiceMail non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente che lascerà il messaggio in segreteria telefonica. Il valore passato a SenderCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce ad esempio un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali del mittente non sono necessarie se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da verificare. Ad esempio:</p>
<p>-TargetFqdn atl-cs-001.litwareinc.com</p></td>
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
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'account utente che deve ricevere il messaggio di verifica in segreteria telefonica. Deve essere un indirizzo SIP diverso da quello utilizzato per il mittente. Ad esempio:</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>Non è necessario includere le credenziali per il destinatario del messaggio in segreteria telefonica.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="odd">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'account utente che lascerà il messaggio in segreteria telefonica. Deve essere un indirizzo SIP diverso da quello utilizzato per il destinatario. Ad esempio:</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Il parametro SenderSIPAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue la verifica con le impostazioni di configurazione del monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>WaveFile</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Percorso del file audio con estensione WAV che può essere utilizzato durante la verifica del servizio di segreteria telefonica. Se viene incluso questo parametro, il cmdlet <strong>Test-CsExUMVoiceMail</strong> riprodurrà durante la connessione alla segreteria telefonica di Exchange il file WAV specificato. Se non viene incluso questo parametro, verrà riprodotto un file audio predefinito.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet Test-CsExUMVoiceMail non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsExUMVoiceMail** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsExUMConnectivity](test-csexumconnectivity.md)

