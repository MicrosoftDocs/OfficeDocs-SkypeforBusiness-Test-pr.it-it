---
title: Test-CsLisConfiguration
TOCTitle: Test-CsLisConfiguration
ms:assetid: 6983d42e-6b93-4365-b0f1-81031d6e251b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398497(v=OCS.15)
ms:contentKeyID: 49300855
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsLisConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la configurazione del server Informazioni percorso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsLisConfiguration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsLisConfiguration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BssId <String>] [-ChassisId <String>] [-Force <SwitchParameter>] [-Mac <String>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-PortId <String>] [-PortIdSubType <InterfaceAlias | InterfaceName | LocallyAssigned>] [-Subnet <String>]

## Esempi

## ESEMPIO 1

Con questo esempio viene testata la configurazione LIS per il nome di dominio completo atl-cs-001.litwareinc.com. Il test avrà esito positivo se è possibile effettuare una connessione al servizio Web LIS in corrispondenza di tale nome di dominio completo con le credenziali dell'utente corrente. Se viene individuata una posizione che può essere mappata all'indirizzo IP della subnet 192.168.0.0, viene restituito l'indirizzo di tale posizione.

Perché il comando abbia esito positivo deve esistere una configurazione di monitoraggio dello stato contenente utenti di transazione sintetica. Per vedere se esiste una configurazione di monitoraggio dello stato, eseguire il cmdlet **Get-CsHealthMonitoringConfiguration**. Per creare una nuova configurazione di monitoraggio dello stato, eseguire il cmdlet **New-CsHealthMonitoringConfiguration**.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0

## ESEMPIO 2

Questo esempio è identico all'esempio 1, ma con l'aggiunta del parametro UserSipAddress. Utilizzare questo comando se non sono stati configurati utenti di transazione sintetica e se il computer su cui è in esecuzione il comando dispone di un certificato del server.

    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com

## ESEMPIO 3

Nella prima riga di questo esempio viene chiamato il cmdlet **Get-Credential** di Windows PowerShell, che richiede all'utente un ID e una password. Queste informazioni vengono crittografate e archiviate nella variabile $cred.

La seconda riga è identica al comando nell'esempio 2, ma con l'aggiunta del parametro UserSipAddress. Utilizzare questo comando se non sono stati configurati utenti di transazione sintetica e se il computer su cui è in esecuzione il comando non dispone di un certificato del server.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetFqdn atl-cs-001.litwareinc.com -Subnet 192.168.0.0 -UserSipAddress sip:kmyer@litwareinc.com -UserCredential $cred

## ESEMPIO 4

Nella prima riga di questo esempio viene chiamato il cmdlet **Get-Credential**, che richiede all'utente un ID e una password. Queste informazioni vengono crittografate e archiviate nella variabile $cred.

Nella riga 2 viene testata la configurazione LIS effettuando una chiamata all'URI del servizio Web (https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc) in base all'indirizzo SIP dell'utente remoto (sip:kmyer@litwareinc.com) e fornendo le credenziali ottenute nella riga 1 al parametro WebCredential. Il test avrà esito positivo se è possibile effettuare una connessione al servizio Web LIS in corrispondenza di tale URI con le credenziali utente fornite. Se viene individuata una posizione che può essere mappata all'indirizzo IP della subnet 192.168.0.0, all'indirizzo MAC 0A-23-00-00-00-AA o all'ID di porta 4500 e allo ChassisId 0A-23-00-00-00-AA, viene restituito l'indirizzo di tale posizione.

Utilizzare questo comando se il computer su cui è in esecuzione il comando non dispone di un certificato del server.

    $cred = Get-Credential
    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -WebCredential $cred -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## ESEMPIO 5

Questo esempio è identico all'esempio 4, con la differenza che il comando non utilizza il parametro WebCredential e di conseguenza non chiama il cmdlet **Get-Credential**. Utilizzare questo comando se il computer in cui è in esecuzione il comando dispone di un certificato del server.

    Test-CsLisConfiguration -TargetUri https://atl-cs-001.litwareinc.com/locationinformation/lisservice.svc -UserSipAddress sip:kmyer@litwareinc.com -Subnet 192.168.0.0 -Mac 0A-23-00-00-00-AA -PortId 4500 -ChassisId 0A-23-00-00-00-AA

## Descrizione dettagliata

Questo cmdlet consente di determinare se il servizio Web LIS (Location Information Server) può essere contattato in base alle informazioni nei parametri forniti. Se il servizio Web può essere contattato e viene individuata una posizione corrispondente a uno dei parametri forniti, il test viene considerato come superato, quindi viene visualizzata la posizione. Anche nel caso in cui la posizione non venga trovata, il test viene superato se il servizio Web può essere contattato, sebbene senza informazioni sulla posizione. Inoltre, se si chiama questo cmdlet senza fornire i parametri opzionali, il test sarà lo stesso superato (purché sia possibile contattare il servizio Web), ma non saranno restituite informazioni sulla posizione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Test-CsLisConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsConfiguration"}

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
<td><p>Il nome di dominio completo (nella forma server.litwareinc.com) del server su cui eseguire il test.</p>
<p>Questo parametro è obbligatorio se non è stato specificato il parametro TargetUri, caso in cui non è possibile specificare TargetFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>L'URI (Uniform Resource Identifier) del servizio Informazioni percorso. È possibile recuperare l'URI del servizio Informazioni percorso eseguendo il comando riportato di seguito: Get-CsService –WebServer | Select-Object LIServiceInternalUri</p>
<p>Se si specifica un valore per questo parametro, è obbligatorio specificare anche il parametro UserSipAddress. Se il computer su cui è in esecuzione il comando non dispone di un certificato del server, è necessario specificare un valore anche per il parametro WebCredential.</p>
<p>Questo parametro è obbligatorio se non è stato specificato il parametro TargetFqdn.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Un oggetto contenente le credenziali utente per l'accesso al servizio Informazioni percorso. Questo oggetto può essere recuperato chiamando il cmdlet <strong>Get-Credential</strong> e specificando le credenziali appropriate.</p>
<p>Questo parametro è obbligatorio se sono stati specificati i parametri TargetFqdn e UserSipAddress e se il computer da cui viene eseguito il cmdlet non dispone di un certificato del server.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato nel test. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>BssId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identificatore del set di servizi di base (BSSID) di un punto di accesso wireless. Questo valore deve essere nella forma nn-nn-nn-nn-nn-nn, ad esempio 12-34-56-78-90-ab.</p></td>
</tr>
<tr class="even">
<td><p><em>ChassisId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo MAC (Media Access Control) di uno switch di rete. Questo valore deve essere nella forma nn-nn-nn-nn-nn-nn, ad esempio 12-34-56-78-90-ab, oppure deve essere un indirizzo IP.</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Questo parametro non è utilizzato per Location Information Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mac</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo MAC del commutatore di porte. Questo valore deve essere nella forma nn-nn-nn-nn-nn-nn, ad esempio 12-34-56-78-90-ab.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando si specifica questo parametro, l'output dettagliato relativo all'esecuzione del cmdlet viene archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome di una variabile. Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando simile al seguente:</p>
<p></p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="even">
<td><p><em>PortId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'ID della porta associata alla posizione da testare. Può anche contenere un indirizzo MAC o IP.</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIdSubType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PortIDSubType</p></td>
<td><p>Il sottotipo della porta. Questo valore può essere immesso come valore numerico o stringa ma deve essere un sottotipo valido. I sottotipi validi sono:</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Il numero di porta del servizio di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnet</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo IP di una subnet. Il valore dovrebbe essere immesso come un indirizzo IPv4 (cifre separate da punti come 192.0.2.0).</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP di un utente remoto.</p>
<p>Se si specifica un valore per questo parametro, è necessario specificare anche un valore per il parametro TargetFqdn o TargetUri.</p>
<p>Questo parametro è obbligatorio se si specifica il parametro TargetFqdn, ma solo se non sono stati impostati utenti di transazione sintetica. Per vedere se sono stati configurati utenti di transazione sintetica, eseguire il cmdlet <strong>Get-CsHealthMonitoringConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSCredential</p></td>
<td><p>Un oggetto contenente le credenziali utente per l'accesso al servizio Informazioni percorso. Questo oggetto può essere recuperato chiamando il cmdlet <strong>Get-Credential</strong> e specificando le credenziali appropriate.</p>
<p>Questo parametro è obbligatorio se sono stati specificati i parametri TargetUri e UserSipAddress e se il computer su cui viene eseguito il cmdlet non dispone di un certificato del server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Test-CsLisConfiguration** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Export-CsLisConfiguration](export-cslisconfiguration.md)

