---
title: Test-CsClientAuthentication
TOCTitle: Test-CsClientAuthentication
ms:assetid: 6a25b2c6-0cb2-473c-af92-0be5cead8a19
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619181(v=OCS.15)
ms:contentKeyID: 49300865
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsClientAuthentication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Determina se un utente può o non può accedere a Lync Server utilizzando un certificato scaricato dal servizio di provisioning dei certificati. Questo cmdlet è stato introdotto in Lync Server 2013. Sostituisce il cmdlet **Test-CSClientAuth** utilizzato in Lync Server 2010.

## Sintassi

    Test-CsClientAuthentication -UserCredential <PSCredential> -UserSipAddress <String> [-Force <SwitchParameter>] [-LiveIdAuthentication <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetUri <String>]

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 consentono di verificare la possibilità dell'utente litwareinc\\kenmyer di accedere al pool di registrazione atl-cs-001.litwareinc.com utilizzando un certificato client. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali per l'utente. L'oggetto credenziali risultante (che richiede l'immissione della password dell'utente) viene archiviato in una variabile denominata $cred1.

Il secondo comando utilizza il cmdlet **Test-CsClientAuthentication**, specificando il nome completo del dominio del pool di registrazione (TargetFqdn), l'indirizzo SIP dell'utente (UserSipAddress) e l'oggetto credenziali creato con il comando iniziale (UserCredential).

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsClientAuthentication -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## Descrizione dettagliata

I certificati client offrono agli utenti un metodo alternativo per essere autenticati tramite Lync Server. Per stabilire se un utente può o non può accedere al sistema utilizzando un certificato client, è possibile eseguire il cmdlet **Test-CsClientAuthentication**. Quando si esegue il cmdlet **Test-CsClientAuthentication**, è necessario specificare il pool di registrazione e l'indirizzo SIP dell'account da testare. È inoltre necessario specificare il nome e la password di accesso. Dopo la chiamata al cmdlet **Test-CsClientAuthentication**, il cmdlet contatterà il servizio di provisioning dei certificati e scaricherà una copia di ogni certificato client dell'utente specificato. Se è possibile individuare e scaricare un certificato client, il cmdlet **Test-CsClientAuthentication** tenterà di accedere utilizzando tale certificato. Se l'accesso riesce, il cmdlet **Test-CsClientAuthentication** si disconnetterà e segnalerà l'esito positivo del test.

Se non è possibile trovare o scaricare un certificato oppure se il cmdlet non riesce a eseguire l'accesso utilizzando il certificato, il cmdlet **Test-CsClientAuthentication** segnalerà l'esito negativo del test.

Utenti autorizzati a eseguire il cmdlet: per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, eseguire il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsClientAuthentication"}

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
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente da utilizzare nel test. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP dell'utente da utilizzare nel test. Ad esempio: -UserSipAddress sip:kenmyer@litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione degli eventuali messaggi di errore non grave che potrebbero essere generati durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>LiveIdAuthentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Verifica la capacità dell'utente test di accedere utilizzando le proprie credenziali OrgId (Business LiveId).</p></td>
</tr>
<tr class="odd">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
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
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre il carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome completo del dominio (FQDN) del pool di registrazione dove testare l'autenticazione del client. Ad esempio: -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio di provisioning dei certificati. Se questo parametro non viene incluso, il cmdlet <strong>Test-CsClientAuthentication</strong> utilizzerà il servizio di provisioning dei certificati configurato per il pool di registrazione.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Test-CsClientAuthentication** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[Test-CsRegistration](test-csregistration.md)

