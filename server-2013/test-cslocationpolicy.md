---
title: Test-CsLocationPolicy
TOCTitle: Test-CsLocationPolicy
ms:assetid: 49f7d148-d46d-4bcc-af9d-6a3a0fdde8ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425962(v=OCS.15)
ms:contentKeyID: 49300452
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLocationPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esegue un test per determinare i criteri percorso che verranno utilizzati in base ai criteri specificati nei valori dei parametri. I criteri percorso includono le impostazioni che stabiliscono se e come verrà applicata la funzionalità per le chiamate di emergenza Enhanced 9-1-1 (E9-1-1), che consente all'operatore che risponde alle chiamate di emergenza di determinare la posizione geografica del chiamante. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsLocationPolicy -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsLocationPolicy [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Subnet <String>]

## Esempi

## ESEMPIO 1

Questo esempio determina i criteri percorso dell'utente corrente (o correntemente configurato). TargetFqdn è obbligatorio.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

Nella prima riga dell'Esempio 2 viene utilizzato il cmdlet **Get-Credential** di Windows PowerShell. Questo cmdlet recupererà le credenziali dell'utente e le restituisce come un oggetto protetto. Il solo parametro fornito a questo cmdlet è l'ID utente. Quando si utilizza questo cmdlet, si aprirà una finestra di dialogo in cui l'ID utente è già inserito e dove è disponibile una casella di testo in cui digitare la password dell'utente. Queste credenziali utente vengono salvate nella variabile $cred.

Nella riga 2 viene utilizzato il cmdlet **Test-CsLocationPolicy**. Proprio come nell'Esempio 1, viene fornita la destinazione FQDN. Tuttavia, in questo esempio, invece di usare l'utente preconfigurato, il test verrà eseguito per l'utente con indirizzo SIP kenmyer@litwareinc.com. Viene fornito il valore (con prefisso sip: prefix) per il parametro UserSipAddress e le credenziali per quell'utente (memorizzate nella variabile $cred) per il parametro UserCredential.

    $cred = Get-Credential "litwareinc\kenmyer"
    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred -UserSipAddress "sip:kenmyer@litwareinc.com"

## ESEMPIO 3

Questo esempio è simile all'esempio 2, ma non prevede che vengano specificate le credenziali utente. Quando il cmdlet **Test-CsLocationPolicy** viene chiamato senza specificare le credenziali utente, per autenticare e rilevare i criteri percorso dell'utente viene utilizzato il certificato server presente sul computer in cui viene eseguito il cmdlet. Se il computer non dispone di un certificato server, è necessario specificare le credenziali come mostrato nell'esempio 2. Per verificare se sul computer è presente un certificato server, utilizzare il cmdlet **Get-CsCertificate**.

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com"

## ESEMPIO 4

Questo esempio determina i criteri percorso per la subnet con subnet ID 172.15.11.0. Se alla subnet non sono associati criteri percorso, verranno recuperati i criteri percorso dell'utente configurato.

Nota: per definire i criteri percorso su una subnet, impostare il parametro LocationPolicy del cmdlet **Set-CsNetworkSite** sull'ID dei criteri percorso e il parametro NetworkSiteId del cmdlet **Set-CsNetworkSubnet** sull'ID di quel sito. Ad esempio:

Set-CsNetworkSite Portland –LocationPolicy Reno

Set-CsNetworkSubnet 175.15.11.0 –NetworkSiteID Portland

    Test-CsLocationPolicy -TargetFqdn atl-cs-001.litwareinc.com -Subnet 172.15.11.0

## Descrizione dettagliata

I criteri percorso vengono utilizzati per applicare impostazioni che mettono in relazione la funzionalità E9-1-1 con la posizione del client. I criteri percorso stabiliscono se un utente è abilitato per la funzionalità E9-1-1 e, in caso affermativo, quale comportamento tenere per una chiamata di emergenza. Ad esempio, è possibile utilizzare i criteri percorso per definire quale numero costituisce una chiamata di emergenza (112 in Italia), se inviare o meno una notifica all'ufficio di sicurezza aziendale, la modalità di instradamento della chiamata e così via. Questo cmdlet restituisce le informazioni sui criteri percorso che verranno utilizzati quando la chiamata viene effettuata da un particolare client su uno specifico pool, subnet, switch o punto di accesso wireless.

Se non viene specificato un utente nella chiamata a questo cmdlet, verrà testato l'utente attualmente configurato. Per trovare l'utente attualmente configurato, chiamare il cmdlet **Get-CsHealthMonitoringConfiguration**. Per impostare l'utente configurato, chiamare il cmdlet **Set-CsHealthMonitoringConfiguration**.

Se vengono trovati i criteri percorso per l'utente o per la subnet, il test termina correttamente. Per impostazione predefinita, le informazioni ottenute includono il nome dei criteri percorso (se sono assegnati criteri per utente) e l'indicazione se l'utente o la subnet è abilitato per la funzionalità E9-1-1. Includere il parametro Verbose di Windows PowerShell per ottenere informazioni aggiuntive sul test.

È possibile testare i criteri percorso su utenti o subnet di rete. Se si esegue il test su una subnet (specificando un valore per il parametro Subnet), il cmdlet tenterà di risolvere i criteri percorso per quella subnet. Se alla subnet non sono assegnati criteri percorso, verranno recuperati i criteri percorso per l'utente configurato. Se i criteri percorso vengono recuperati correttamente, l'output includerà un valore LocationPolicyTagID che inizia con subnet-tagid. Se non vengono trovati criteri percorso per la subnet, LocationPolicyTagID inizierà con user-tagid.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, il cmdlet **Test-CsLocationPolicy** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsLocationPolicy"}

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
<td><p>Il nome di dominio completo (FQDN) del pool su cui è in esecuzione il servizio di registrazione. Se non viene specificato un utente verrà assunto l'utente preconfigurato o corrente.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Un oggetto che contiene l'ID utente e la password dell'account utente del quale vengono testati i criteri percorso. Un oggetto Credential può essere recuperato utilizzando il cmdlet <strong>Get-Credential</strong>, specificando le informazioni necessarie e salvando l'output in una variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato nel test. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando si specifica questo parametro, l'output dettagliato relativo all'esecuzione del cmdlet viene archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome di una variabile. Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando simile al seguente:</p>
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
<td><p>Il numero di porta del servizio di registrazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Subnet</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'ID (l'indirizzo IP) della subnet di rete per la quale si vogliono testare i criteri percorso.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP dell'utente del quale si vogliono testare i criteri percorso. Deve essere nel formato sip:&lt;ID utente&gt;, ad esempio, sip:kenmyer@litwareinc.com.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Test-CsLocationPolicy** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)  
[Set-CsNetworkSite](set-csnetworksite.md)

