---
title: Test-CsAddressBookService
TOCTitle: Test-CsAddressBookService
ms:assetid: 8398c9ea-eaab-4a4d-9e09-473ea2b27e22
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398661(v=OCS.15)
ms:contentKeyID: 49301175
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookService

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di un utente di accedere al server che ospita il servizio Web di scaricamento della Rubrica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsAddressBookService -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsAddressBookService -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene verificato il servizio Web di scaricamento della Rubrica per il pool atl-cs-001.litwareinc.com. Questo comando verifica il servizio Web di scaricamento della Rubrica utilizzando utenti di test preconfigurati per il pool atl-cs-001.litwareinc.com.

    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

Anche i comandi mostrati nell'esempio 2 consentono di testare la disponibilità del server che eseguono il servizio Web di scaricamento della Rubrica; in questo caso, però, i comandi vengono eseguiti con le credenziali dell'utente Davide Garghentini (litwareinc\\davidegarghentini). A tal fine, il primo comando utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali Windows PowerShell contenente il nome e la password dell'utente Davide Garghentini. Poiché il nome di accesso litwareinc\\davidegarghentini è stato incluso come parametro, la finestra di dialogo Richiesta credenziali di Windows PowerShell richiede esclusivamente che l'amministratore immetta la password per l'account Davide Garghentini. L'oggetto credenziali risultante viene memorizzato in una variabile denominata $cred1.

Nel secondo comando viene utilizzato il cmdlet **Test-CsAddressBookService** per testare il servizio Web di scaricamento della Rubrica per il pool atl-cs-001.litwareinc.com. Per eseguire questo comando con le credenziali utente di Ken Myer, viene incluso il parametro UserCredential insieme al valore di parametro $cred1. È necessario inoltre fornire l'indirizzo SIP di Ken Myer utilizzando il parametro UserSipAddress.

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAddressBookService -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:kenmyer@litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 viene illustrato come testare il servizio Web di scaricamento della Rubrica per atl-cs-001.litwareinc.com. A tale scopo, viene chiamato il cmdlet **Test-CsAddressBookService** con due parametri: TargetUri, che specifica l'URI del servizio Web di scaricamento della Rubrica, e UserSipAddress, che include l'indirizzo SIP di Windows PowerShell per l'account utente utilizzato nel test.

``` 


Test-CsAddressBookService -TargetUri https://atl-cs-001.litwareinc.com/abs/handler -UserSipAddress "sip:kenmyer@litwareinc.com"
```

## Descrizione dettagliata

Il cmdlet **Test-CsAddressBookService** è un esempio di "transazione sintetica". Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite manualmente da un amministratore oppure automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Le transazioni sintetiche vengono in genere condotte in due modi distinti. Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascuno dei propri pool di registrazione. Questi utenti di test sono una coppia di utenti preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test e non di account appartenenti a utenti effettivi. Quando vengono configurati gli utenti di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su tale pool, senza dover specificare le identità degli account utente (e fornire le relative credenziali) coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando account utente effettivi. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (anziché una coppia di account di test) e provare a diagnosticare e risolvere il problema. Se si decide di condurre una transazione sintetica utilizzando gli account utente reali, sarà necessario fornire i nomi di accesso e le password per ogni utente.

Il cmdlet **Test-CsAddressBookService** consente di verificare se un utente può connettersi al servizio Web di scaricamento della Rubrica. Quando viene eseguito, il cmdlet, **Test-CsAddressBookService** si connette al servizio Web di scaricamento della Rubrica nel pool specificato e richiede il percorso dei file della Rubrica. Se il servizio Web di scaricamento della Rubrica fornisce tale percorso, il test è superato. Se la richiesta viene rifiutata, l'esito del test è negativo.

È possibile testare il servizio Web di scaricamento della Rubrica in due modi diversi: testando il servizio stesso oppure testando il servizio Web associato.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Test-CsAddressBookService** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAddressBookService"}

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
<td><p>Il nome di dominio completo del pool di registrazione in cui testare il servizio Web di scaricamento della Rubrica. Ad esempio: -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Non è possibile utilizzare il parametro TargetUri e il parametro TargetFqdn nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>L'URI (Uniform Resource Identifier) del servizio query Web della Rubrica. Ad esempio: -TargetUri &quot;https://atl-cs-001.litwareinc.com/abs/handler&quot;.</p>
<p>Non è possibile utilizzare il parametro TargetUri e il parametro TargetFqdn nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>L'oggetto credenziale utente per l'account utente da utilizzare nel test. Il valore trasmesso a UserCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziale per l'utente litwareinc\davidegarghentini e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>È necessario fornire la password utente quando si esegue questo comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato nella verifica. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di verificare se gli utenti esterni possono utilizzare il servizio Web di scaricamento della Rubrica.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome della variabile. Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando simile al seguente:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>La porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'utente da utilizzare nel test. Se questo parametro non viene specificato, <strong>Test-CsAddressBookService</strong> esegue i controlli utilizzando l'account dell'utente connesso.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto contenente le credenziali utente per l'accesso al servizio Informazioni percorso. Questo oggetto può essere recuperato chiamando il cmdlet <strong>Get-Credential</strong> e specificando le credenziali appropriate.</p>
<p>Questo parametro è obbligatorio se sono stati specificati i parametri TargetUri e UserSipAddress e se il computer in cui viene eseguito il comando non dispone di un certificato del server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsAddressBookService** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsAddressBookService** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)  
[Update-CsAddressBook](update-csaddressbook.md)

