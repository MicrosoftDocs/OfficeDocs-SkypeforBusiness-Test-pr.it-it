---
title: Test-CsPersistentChatMessage
TOCTitle: Test-CsPersistentChatMessage
ms:assetid: 08c6db0b-23e2-4fbe-8276-181275a40daf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204656(v=OCS.15)
ms:contentKeyID: 49299605
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPersistentChatMessage

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se una coppia di utenti può scambiare messaggi utilizzando il servizio Chat persistente (noto in precedenza come servizio Group Chat). Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsPersistentChatMessage -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPersistentChatMessage -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPersistentChatMessage [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ChatRoomUri <String>] [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Setup <$true | $false>] [-TestUser1SipAddress <String>] [-TestUser2SipAddress <String>]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 2 verificano la capacità di una coppia di utenti (litwareinc\\pilar e litwareinc\\kenmyer) di accedere a Lync Server 2013 e quindi scambiare messaggi utilizzando il servizio Chat persistente. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché è stato incluso come parametro il nome di accesso litwareinc\\pilar, l'amministratore deve immettere solo la password dell'account Pilar Ackerman nella finestra di dialogo Richiesta credenziali di Windows PowerShell. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1. Il secondo comando esegue la stessa operazione, questa volta restituendo un oggetto credenziali per l'account Ken Myer.

Con i due oggetti credenziali disponibili, il terzo comando determina se i due utenti possono o meno accedere a Lync Server 2013 e scambiare messaggi utilizzando Chat persistente. A tale scopo, viene chiamato il cmdlet **Test-CsPersistentChatMessage** con i parametri seguenti: TargetFqdn (FQDN del pool di registrazione), SenderSipAddress (indirizzo SIP del primo utente di test), SenderCredential (oggetto di Windows PowerShell contenente le credenziali di questo stesso utente), ReceiverSipAddress (indirizzo SIP dell'altro utente di test) e ReceiverCredential (oggetto di Windows PowerShell contenente le credenziali dell'altro utente di test).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPersistentChatMessage -TargetFqdn atl-persistentchat-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsPersistentChatMessage** verifica che una coppia di utenti di test sia in grado di scambiare messaggi utilizzando il servizio Chat persistente. A tale scopo, il cmdlet esegue l'accesso a Lync Server 2013 per i due utenti, connette gli utenti a una chat room di Chat persistente, scambia alcuni messaggi e quindi esce dalla chat room e disconnette i due utenti. Si noti che le chiamate a questo cmdlet avranno esito negativo se non è stata creata una chat room o se agli account dei due utenti di test non è stato assegnato un criterio di Chat persistente che consente loro di accedere al servizio Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPersistentChatMessage"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Test-CsPersistentChatMessage** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore passato a ReceiverCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet Get-Credential. Il codice seguente ad esempio restituisce un oggetto credenziali dell'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali del destinatario non sono necessarie se si esegue il test con le impostazioni di configurazione per il monitoraggio dello stato del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore passato a SenderCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce ad esempio un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p>
<p>Le credenziali del mittente non sono necessarie se si esegue il test con le impostazioni di configurazione per il monitoraggio dello stato del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione da testare.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato quando si esegue il test. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>ChatRoomUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Percorso della chat room costituito dal nome di dominio completo del server Chat persistente e dal nome della chat room, ad esempio:</p>
<p>-ChatRoomIdentity &quot;atl-persistentchat-001.litwareinc.com\ITChatRoom&quot;</p></td>
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
<p>$TestOutput. ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput. ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
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
<td><p>Indirizzo SIP del primo dei due account utente da testare, ad esempio:</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>Il parametro ReceiverSIPAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue il test con le impostazioni di configurazione per il monitoraggio dello stato del pool.</p></td>
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
<td><p>Indirizzo SIP del secondo dei due account utente da testare, ad esempio:</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Il parametro SenderSipAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue il test con le impostazioni di configurazione per il monitoraggio dello stato del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>Setup</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Consente di eseguire il cmdlet in un computer nodo Watcher che non dispone dell'accesso alla topologia di Lync Server. A tale scopo, eseguire innanzitutto <strong>Test-CsPersistentChatMessage</strong> con il parametro Setup da un computer che non dispone dell'accesso alla topologia. In questo modo sarà quindi possibile eseguire il cmdlet nei computer nodo Watcher.</p>
<p>Se si utilizza il parametro Setup, è necessario utilizzare anche i parametri TestUser1SipAddress e TestUser2SipAddress.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestUser1SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del primo utente test utilizzato con il parametro Setup.</p></td>
</tr>
<tr class="even">
<td><p><em>TestUser2SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del secondo utente test utilizzato con il parametro Setup.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsPersistentChatMessage** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsPersistentChatMessage** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Grant-CsPersistentChatPolicy](grant-cspersistentchatpolicy.md)  
[New-CsPersistentChatPolicy](new-cspersistentchatpolicy.md)  
[Set-CsPersistentChatPolicy](set-cspersistentchatpolicy.md)

