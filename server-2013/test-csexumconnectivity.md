---
title: Test-CsExUMConnectivity
TOCTitle: Test-CsExUMConnectivity
ms:assetid: 2eb541d2-5f09-483c-adc2-4abb16391ea5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204784(v=OCS.15)
ms:contentKeyID: 49300060
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsExUMConnectivity

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di un utente test di connettersi al servizio Messaggistica unificata di Exchange. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsExUMConnectivity -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsExUMConnectivity -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsExUMConnectivity [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## Esempio 1

Nell'esempio viene verificata la connettività con il servizio Messaggistica unificata di Exchange per il pool atl-cs-001.litwareinc.com. Questo comando potrà essere eseguito correttamente solo se sono stati definiti utenti test per il pool atl-cs-001.litwareinc.com. In questo caso, il comando stabilisce se il primo utente test è in grado di connettersi al servizio Messaggistica unificata di Exchange. Se non sono stati configurati utenti test per il pool, il comando avrà esito negativo.

    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

I comandi riportati nell'esempio 2 verificano la connettività con il servizio Messaggistica unificata di Exchange per l'utente litwareinc\\kenmyer. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell per l'utente litwareinc\\kenmyer. È necessario specificare la password di questo account per creare un oggetto credenziali valido e per consentire al cmdlet **Test-CsExUMConnectivity** di eseguire la verifica.

Il secondo comando dell'esempio utilizza l'oggetto credenziali fornito ($x) e l'indirizzo SIP dell'utente litwareinc\\kenmyer per determinare se è possibile per l'utente connettersi al servizio Messaggistica unificata di Exchange.

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## Esempio 3

Il comando riportato nell'esempio 3 è una variante del comando dell'esempio 2. In questo caso tuttavia viene incluso il parametro OutLoggerVariable per generare un log dettagliato di ogni passaggio eseguito dal cmdlet **Test-CsExUMConnectivity** e dell'esito positivo o negativo dei singoli passaggi. A tale scopo, viene aggiunto il parametro OutLoggerVariable con valore ExumText. In questo modo, le informazioni di registrazione dettagliate vengono archiviate in una variabile denominata $ExumTest. Nell'ultimo comando dell'esempio viene utilizzato il metodo ToXML() per convertire le informazioni del log al formato XML. I dati XML vengono quindi scritti in un file denominato C:\\Logs\\ExumTest.xml utilizzando il cmdlet Out-File.

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsExUMConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential -OutLoggerVariable ExumTest
    
    $ExumTest.ToXML() | Out-File C:\Logs\ExumTest.xml

## Descrizione dettagliata

Il cmdlet **Test-CsExUMConnectivity** verifica che l'utente specificato sia in grado di connettersi al servizio Messaggistica unificata di Microsoft Exchange Server 2013. Si noti che questo cmdlet verifica solo la capacità di connettersi al servizio e non verifica il servizio stesso. Per verificare il servizio Messaggistica unificata (eseguendo un cmdlet di transazione sintetica che lascia un messaggio in segreteria telefonica nella cassetta postale di un utente), utilizzare il cmdlet [Test-CsExUMVoiceMail](test-csexumvoicemail.md).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsExUMConnectivity"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsExUMConnectivity** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool di cui viene testata la connettività con il servizio Messaggistica unificata di Exchange.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente da utilizzare nel test. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce ad esempio un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti test configurati tramite i cmdlet CsHealthMonitoringConfiguration.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato quando si esegue il test. I valori consentiti sono:</p>
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
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'utente da utilizzare nel test, ad esempio:</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti test configurati tramite i cmdlet CsHealthMonitoringConfiguration.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsExUMConnectivity** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsExUMConnectivity** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsExUMVoiceMail](test-csexumvoicemail.md)

