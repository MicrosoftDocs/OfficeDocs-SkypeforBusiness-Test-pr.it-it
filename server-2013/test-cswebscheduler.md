---
title: Test-CsWebScheduler
TOCTitle: Test-CsWebScheduler
ms:assetid: 3dbd7ef6-a60f-4350-8831-73818e10863b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204829(v=OCS.15)
ms:contentKeyID: 49300286
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsWebScheduler

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se un utente può eseguire l'utilità di pianificazione Web di Lync Server 2013 per pianificare una riunione online. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsWebScheduler -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsWebScheduler -TargetUri <String> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-WebCredential <PSCredential>] <COMMON PARAMETERS>

    Test-CsWebScheduler -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-External <SwitchParameter>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## Esempio 1

Nell'esempio viene verificata l'Utilità di pianificazione Web per il pool atl-cs-001.litwareinc.com. Questo comando potrà essere eseguito correttamente solo se sono stati definiti utenti test per il pool atl-cs-001.litwareinc.com. In questo caso, il comando stabilisce se il primo utente test è in grado di pianificare una riunione online utilizzando l'Utilità di pianificazione Web.

Se gli utenti di test non sono stati definiti, il comando avrà esito negativo in quanto non sarà in grado di stabilire con quale account utente tentare di accedere al sistema. Se non sono stati definiti gli utenti di test per un pool, è necessario includere il parametro UserSipAddress e le credenziali dell'utente che il comando dovrà utilizzare quando tenta di eseguire l'accesso.

    Test-CsWebScheduler -TargetFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

I comandi riportati nell'esempio 2 verificano se un utente specifico (litwareinc\\pilar) può pianificare una riunione online eseguendo l'utilità di pianificazione Web. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché è stato incluso come parametro il nome di accesso litwareinc\\pilar, l'amministratore deve immettere solo la password dell'account di Pilar Ackerman nella finestra di dialogo Richiesta credenziali di Windows PowerShell. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1.

Il secondo comando verifica quindi se l'utente è in grado di eseguire l'accesso al pool atl-cs-001.litwareinc.com e pianificare una riunione online. A tale scopo, viene chiamato il cmdlet **Test-CsWebScheduler** con tre parametri: TargetFqdn (FQDN del pool di registrazione), UserCredential (oggetto di Windows PowerShell contenente le credenziali utente di Pilar Ackerman) e UserSipAddress (indirizzo SIP che corrisponde alle credenziali utente fornite).

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsWebScheduler -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## Descrizione dettagliata

L'Utilità di pianificazione Web consente agli utenti che non eseguono Microsoft Outlook di pianificare riunioni online. Questa nuova funzionalità, che incorpora la funzionalità dell'Utilità di pianificazione Web disponibile con il Resource Kit di Microsoft Lync Server 2010, consente inoltre agli utenti di eseguire le operazioni seguenti:

  - Pianificare una nuova riunione online.

  - Elencare tutte le riunioni pianificate.

  - Visualizzare/modificare una riunione esistente.

  - Eliminare una riunione esistente.

  - Inviare un invito tramite posta elettronica ai partecipanti di una riunione utilizzando un server di posta elettronica SMTP preconfigurato.

  - Partecipare a una conferenza esistente.

Il cmdlet **Test-CsWebScheduler** consente di verificare se un utente specifico può pianificare una riunione eseguendo l'utilità di pianificazione Web.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsWebScheduler"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsWebScheduler** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo (FQDN) del pool da sottoporre a test.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>URI (Uniform Resource IdentifierI) dell'Utilità di pianificazione Web. Non è possibile utilizzare i parametri TargetUri e TargetFqdn nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente dell'account da sottoporre a test. Il valore passato al parametro UserCredential deve essere un riferimento oggetto ottenuto tramite il cmdlet Get-Credential. Il codice seguente ad esempio restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e lo archivia nella variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando. Questo parametro non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>External</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di verificare se gli utenti esterni possono utilizzare l'Utilità di pianificazione Web.</p></td>
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
<td><p>Indirizzo SIP dell'account utente da sottoporre a test, ad esempio:</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Il parametro UserSipAddress deve fare riferimento allo stesso account utente di UserCredential. Questo parametro non è obbligatorio se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente da utilizzare nel test. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziali per l'utente litwareinc\kenmyer e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Questo parametro è obbligatorio se è specificato il parametro TargetUri o UserSipAddress e se il computer in cui viene eseguito il comando non dispone di un certificato del server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsWebScheduler** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsWebScheduler** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.WebTaskOutput.

## Vedere anche

#### Ulteriori risorse

[Set-CsWebServer](set-cswebserver.md)

