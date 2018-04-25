---
title: Test-CsUnifiedContactStore
TOCTitle: Test-CsUnifiedContactStore
ms:assetid: 0aeca874-87da-4bc8-b2f2-c9c7e0d86883
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204662(v=OCS.15)
ms:contentKeyID: 49299632
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsUnifiedContactStore

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se è possibile accedere ai contatti di un utente tramite l'archivio contatti unificato. Tale archivio consente agli utenti di gestire un unico insieme di contatti accessibili tramite Lync 2013, Outlook e/o Outlook Web Access. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsUnifiedContactStore -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsUnifiedContactStore -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsUnifiedContactStore [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 2 verificano se è possibile trovare i contatti dell'utente litwareinc\\kenmyer nell'archivio contatti unificato. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell per l'utente litwareinc\\kenmyer. È necessario specificare la password di questo account per creare un oggetto credenziali valido e per consentire al cmdlet **Test-CsUnifiedContactStore** di eseguire la verifica.

Il secondo comando dell'esempio utilizza l'oggetto credenziali fornito ($x) e l'indirizzo SIP dell'utente litwareinc\\kenmyer per determinare se è possibile trovare i relativi contatti nell'archivio contatti unificato.

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsUnifiedContactStore -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli amministratori di archiviare i contatti di un utente in Microsoft Exchange Server 2013 anziché in Lync Server. In questo modo l'utente può accedere allo stesso insieme di contatti in Outlook e Outlook Web Access e in Lync 2013. In alternativa, è possibile continuare ad archiviare i contatti in Lync Server. In tal caso gli utenti dovranno gestire due insiemi separati di contatti: uno da utilizzare con Outlook e Outlook Web Access e un altro da utilizzare con Lync 2013.

È possibile verificare se i contatti di un utente sono stati effettivamente spostati nell'archivio contatti unificato eseguendo il cmdlet **Test-CsUnifiedContactStore**. Il cmdlet **Test-CsUnifiedContactStore** selezionerà l'account utente specificato, si connetterà all'archivio contatti unificato e tenterà di recuperare un contatto dell'utente. Se non è possibile recuperare alcun contatto, il comando avrà esito negativo e un messaggio indicherà che non sono stati ricevuti contatti per l'utente e che è necessario verificare l'esistenza di contatti per l'utente.

Si noti che il cmdlet **Test-CsUnifiedContactStore** avrà esito negativo se l'utente di cui è stata eseguita la migrazione nell'archivio contatti unificato non dispone di contatti nel relativo elenco contatti. L'utente specificato deve disporre di almeno un contatto affinché il cmdlet **Test-CsUnifiedContactStore** abbia esito positivo.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsUnifiedContactStore"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Test-csUnifiedContactStore** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo (FQDN) del pool da testare.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente da utilizzare nel test. Il valore passato a UserCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet G<strong>et-Credential</strong>. Il codice seguente restituisce ad esempio un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti di test configurati tramite i cmdlet <strong>CsHealthMonitoringConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
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
<p>Questo parametro non è obbligatorio se si sta eseguendo il test utilizzando utenti di test configurati tramite i cmdlet <strong>CsHealthMonitoringConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsUnifiedContactStore** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsUnifiedContactStore** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.WebTaskOutput.

## Vedere anche

#### Ulteriori risorse

[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

