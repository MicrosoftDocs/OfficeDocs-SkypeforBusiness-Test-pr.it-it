---
title: Test-CsGroupExpansion
TOCTitle: Test-CsGroupExpansion
ms:assetid: e41db33d-d028-4171-9418-ec04885be2fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399009(v=OCS.15)
ms:contentKeyID: 49302264
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsGroupExpansion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di un utente di ricorrere all'espansione gruppo. Lync Server consente agli utenti di configurare un gruppo di distribuzione di Active Directory come contatto. Quando si "espande" un gruppo, vengono visualizzati il nome e le informazioni sulla presenza di ogni membro del gruppo. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsGroupExpansion -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsGroupExpansion -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsGroupExpansion -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -GroupEmailAddress <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 esegue la connessione al pool di registrazione atl-cs-001.litwareinc.com per verificare l'espansione dei gruppi. Per eseguire il test, nel comando viene utilizzato il gruppo FinanceGroup@litwareinc.com.

    Test-CsGroupExpansion -TargetFqdn atl-cs-001.litwareinc.com -GroupEmailAddress FinanceGroup@litwareinc.com 

## Descrizione dettagliata

Può accadere che gli utenti a volte abbiano necessità di comunicare regolarmente con tutti i membri di un gruppo di distribuzione di Active Directory, ad esempio perché tale gruppo include tutti i membri di un team o tutte le persone assegnate a un determinato progetto. Lync Server consente pertanto di configurare come contatto un gruppo di distribuzione. Eseguendo tale operazione, è possibile inviare lo stesso messaggio istantaneo a tutti i membri del gruppo semplicemente indirizzando il messaggio al gruppo anziché a ciascun singolo membro del gruppo.

Potrebbero ovviamente anche esservi occasioni in cui è necessario comunicare con (o verificare la presenza di) determinati individui di tale gruppo. l'espansione dei gruppi consente di visualizzare in modo semplice e rapido tutti i membri di un gruppo e il relativo stato corrente. È inoltre possibile selezionare uno o più membri del gruppo e inviare un messaggio istantaneo solo a tali utenti anziché a tutti i membri.

L'espansione dei gruppi viene abilitata e disabilitata utilizzando il cmdlet **Set-CsWebServiceConfiguration**. Se l'espansione dei gruppi è abilitata, sarà possibile determinare se funziona correttamente eseguendo il cmdlet **Test-CsGroupExpansion**. Con questo cmdlet, si specifica un gruppo di distribuzione di Active Directory utilizzando il relativo indirizzo di posta elettronica. Il cmdlet **Test-CsGroupExpansion** utilizza quindi la funzionalità di espansione dei gruppi per recuperare i membri del gruppo e confrontare l'elenco recuperato con i membri dell'indirizzo di posta elettronica di gruppo specificato. Se i due elenchi corrispondono, l'espansione dei gruppi sta funzionando correttamente.

Si noti che è possibile testare l'espansione dei gruppi in due modi diversi: testando il servizio stesso oppure testando il servizio Web associato.

Utenti autorizzati a eseguire il cmdlet: per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsGroupExpansion"}

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
<td><p><em>GroupEmailAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>l'indirizzo di posta elettronica del gruppo di distribuzione di destinazione. Ad esempio: -GroupEmailAddress &quot;FinanceGroup@litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione in cui testare l'espansione dei gruppi. Ad esempio: -TargetFqdn &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p>Si noti che non è possibile utilizzare il parametro TargetUri e il parametro TargetFqdn nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>URI (Uniform Resource Identifier) del servizio Web per l'espansione dei gruppi. Ad esempio: -TargetUri &quot;https://atl-cs-001.litwareinc.com/groupexpansion&quot;.</p>
<p>Si noti che non è possibile utilizzare il parametro TargetUri e il parametro TargetFqdn nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>l'oggetto credenziale utente per l'account utente da utilizzare nel test. Il valore passato a UserCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziale per l'utente litwareinc\davidegarghentini e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>È necessario fornire la password utente quando si esegue questo comando.</p>
<p>La credenziale utente non è richiesta se si esegue il test con le credenziali dell'utente connesso e utilizzando il parametro TargetFqdn. La credenziale utente è obbligatoria se si utilizza il parametro TargetUri.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.SyntheticTransactions.SipSyntheticTransaction+AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzata nel test. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>External</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di verificare se gli utenti esterni possono utilizzare l'espansione dei gruppi.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome della variabile. Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando analogo al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando analogo al seguente:</p>
<p></p>
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
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è necessario se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP dell'utente da utilizzare nel test. Se questo parametro non viene specificato, il cmdlet <strong>Test-CsGroupExpansion</strong> eseguirà le proprie verifiche utilizzando l'account dell'utente connesso.</p></td>
</tr>
<tr class="even">
<td><p><em>WebCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Oggetto contenente le credenziali utente per l'accesso al servizio Informazioni percorso. Questo oggetto può essere recuperato chiamando il cmdlet <strong>Get-Credential</strong> e specificando le credenziali appropriate.</p>
<p>Questo parametro è obbligatorio se sono stati specificati i parametri TargetUri e UserSipAddress e se il computer in cui viene eseguito il comando non dispone di un certificato del server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsGroupExpansion** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Test-CsGroupExpansion** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsAddressBookService](test-csaddressbookservice.md)  
[Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

