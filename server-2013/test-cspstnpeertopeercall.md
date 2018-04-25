---
title: Test-CsPstnPeerToPeerCall
TOCTitle: Test-CsPstnPeerToPeerCall
ms:assetid: 839cf83f-b667-4cbe-b1ab-28f54a8a9d0b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398662(v=OCS.15)
ms:contentKeyID: 49301178
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnPeerToPeerCall

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di due utenti di effettuare una chiamata peer-to-peer su un gateway PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsPstnPeerToPeerCall -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnPeerToPeerCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene verificato se due utenti di test preconfigurati possono accedere al pool atl-cs-001.litwareinc.com. Dopo l'accesso degli utenti di test,il cmdlet **Test-CsPstnPeerToPeerCall** verifica se i due utenti possono effettuare una chiamata peer-to-peer sul gateway PSTN. Il comando funziona soltanto se sono stati definiti utenti di test per il pool atl-cs-001.litwareinc.com. Se sono disponibili, il comando determina se il primo utente di test può accedere al sistema, quindi verifica se questo utente può chiamare il secondo utente definito per il pool.

Se non sono stati definiti utenti di test, il comando avrà esito negativo in quanto non sarà in grado di stabilire con quali utenti effettuare la verifica. Se non sono stati definiti utenti di test per un pool e non si utilizza la modalità piattaforma server, è necessario includere i parametri SenderSipAddress e ReceiverSipAddress, nonché le credenziali corrispondenti per gli utenti che fungono da account di test. Il cmdlet **Test-CsPstnPeerToPeerCall** eseguirà quindi le verifiche utilizzando i due utenti specificati.

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano la capacità di una coppia di utenti (litwareinc\\pilar e litwareinc\\kenmyer) di accedere a Lync Server e di effettuare una chiamata peer-to-peer sul gateway PSTN. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali di Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché il nome di accesso litwareinc\\pilar è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell viene richiesto soltanto che l'amministratore immetta la password per l'account Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1. Il secondo comando effettua la stessa operazione, questa volta restituendo un oggetto credenziali per l'account Ken Myer.

Con i due oggetti credenziali disponibili, il terzo comando dell'esempio determina se i due utenti possono accedere a Lync Server ed effettuare una chiamata peer-to-peer tramite il gateway PSTN. A tale scopo, viene chiamato il cmdlet **Test-CsPstnPeerToPeerCall** con i parametri seguenti: TargetFqdn (nome di dominio completo del pool di registrazione), SenderSipAddress (indirizzo SIP del primo utente di test), SenderCredential (oggetto di Windows PowerShell contenente le credenziali per lo stesso utente), ReceiverSipAddress (indirizzo SIP dell'altro utente di test) e ReceiverCredential (oggetto di Windows PowerShell contenente le credenziali dell'altro utente).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## ESEMPIO 3

Nell'esempio 3 viene illustrato come utilizzare il cmdlet Test-CsPstnPeerToPeerCall nella modalità piattaforma server. In questa modalità vengono specificati gli indirizzi SIP degli utenti di test, senza includere le credenziali utente. In questa modalità di esecuzione in Lync Server vengono utilizzati i certificati per autenticare i due utenti di test.

    Test-CsPstnPeerToPeerCall -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:jhaas@litwareinc.com" -ReceiverSipAddress "sip:kenmyer@litwareinc.com" 

## Descrizione dettagliata

Il cmdlet **Test-CsPstnPeerToPeerCall** è un esempio di "transazione sintetica" di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite manualmente da un amministratore oppure automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Le transazioni sintetiche vengono eseguite in genere in due modi diversi. Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ognuno dei propri pool di registrazione. Questi utenti di test sono due utenti preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti effettivi. Quando vengono configurati gli utenti di test per un pool, gli amministratori possono eseguire una transazione sintetica per tale pool, senza dover specificare le identità degli account utente (e fornire le relative credenziali) coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando account utente effettivi. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (anziché una coppia di account di test) e provare a diagnosticare e risolvere il problema. Se si decide di condurre una transazione sintetica utilizzando gli account utente reali, sarà necessario fornire i nomi di accesso e le password per ogni utente.

Il cmdlet **Test-CsPstnPeerToPeerCall** può essere utilizzato anche nella modalità piattaforma server. In questo caso è sufficiente specificare l'indirizzo SIP degli utenti affinché Lync Server utilizzi i certificati per autenticare tali utenti.

Quando viene chiamato, il cmdlet **Test-CsPstnPeerToPeerCall** tenta innanzitutto di accedere ai due utenti di test su Lync Server. Supponendo che l'accesso abbia esito positivo, il cmdlet fa sì che l'utente 1 tenti di chiamare l'utente 2 sul gateway PSTN. Il cmdlet **Test-CsPstnPeerToPeerCall** effettua questa chiamata utilizzando il dial plan, il criterio vocale, gli altri criteri e le altre impostazioni di configurazione assegnati all'utente di test. Se il test procede come previsto, il cmdlet verifica che l'utente 2 sia in grado di rispondere alla chiamata e quindi disconnette entrambi gli account di test dal sistema.

Il cmdlet **Test-CsPstnPeerToPeerCall** effettua una vera e propria chiamata telefonica, che verifica se è possibile effettuare una connessione e trasmette codici DTMF sulla rete per determinare se è possibile inviare elementi multimediali sulla connessione. Alla chiamata tuttavia risponde il cmdlet stesso, pertanto non è necessaria una conclusione manuale della chiamata. In pratica, nessuno deve rispondere e riagganciare il telefono chiamato.

Utenti che possono eseguire questo cmdlet: Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnPeerToPeerCall"}

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
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore trasmesso a ReceiverCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, il codice seguente restituisce un oggetto credenziali per l'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>È necessario fornire la password utente quando si esegue questo comando.</p>
<p>Le credenziali del destinatario non sono richieste se si esegue il test con le impostazioni di configurazione di monitoraggio dello stato per il pool o se si esegue il test nella modalità piattaforma server.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore trasmesso a SenderCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziale per l'utente litwareinc\davidegarghentini e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>È necessario fornire la password utente quando si esegue questo comando.</p>
<p>Le credenziali del mittente non sono richieste se si esegue il test con le impostazioni di configurazione di monitoraggio dello stato per il pool o se si esegue il test nella modalità piattaforma server.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo del pool da testare.</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del primo dei due account utente da verificare. Ad esempio: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro ReceiverSipAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
<p>L'indirizzo SIP non è richiesto se si esegue il test con le impostazioni di configurazione di monitoraggio dello stato per il pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>La porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del secondo dei due account utente da verificare. Ad esempio: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro SenderSipAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è richiesto se si esegue il test con le impostazioni di configurazione di monitoraggio dello stato per il pool.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsPstnPeerToPeerCall** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsPstnPeerToPeerCall** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsPstnOutboundCall](test-cspstnoutboundcall.md)

