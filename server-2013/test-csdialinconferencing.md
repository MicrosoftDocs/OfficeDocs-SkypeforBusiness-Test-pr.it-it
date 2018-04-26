---
title: Test-CsDialInConferencing
TOCTitle: Test-CsDialInConferencing
ms:assetid: e4aedf4f-77ac-4c8b-9613-07f8ea12c041
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399013(v=OCS.15)
ms:contentKeyID: 49302289
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialInConferencing

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Test-CsDialInConferencing** verifica se un utente può partecipare a una sessione di una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsDialInConferencing -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetPstnPhoneNumber <String>] [-UserSipAddress <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetPstnPhoneNumber <String>] [-VerifyConferenceJoin <$true | $false>] <COMMON PARAMETERS>

    Test-CsDialInConferencing [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene verificato se un utente di prova preconfigurato può partecipare a una conferenza telefonica con accesso esterno sul pool atl-cs-001.litwareinc.com. Il comando funzionerà soltanto se sono stati definiti utenti di prova per il pool atl-cs-001.litwareinc.com. In caso affermativo, il comando stabilirà se il primo utente di prova è o meno in grado di accedere a Lync Server.

Se non sono stati definiti utenti di prova, il comando avrà esito negativo perché non sarà in grado di stabilire con quale utente tentare di eseguire l'accesso. Se non sono stati definiti utenti di prova per un pool, sarà necessario includere il parametro UserCredential e le credenziali dell'utente che devono essere utilizzate dal comando quando verrà tentato l'accesso.

    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

I comandi mostrati nell'esempio 2 verificano la capacità di un utente specifico (litwareinc\\pilar) di partecipare a una conferenza telefonica con accesso esterno sul pool atl-cs-001.litwareinc.com. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali di Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché il nome di accesso –litwareinc\\pilar è stato incluso come parametro, l'amministratore deve solo immettere la password dell'account di Pilar Ackerman nella finestra di dialogo Richiesta credenziali di Windows PowerShell. L'oggetto credenziali risultante viene memorizzato in una variabile denominata $cred1.

Il secondo comando verifica quindi se l'utente Pilar Ackerman può accedere al pool atl-cs-001.litwareinc.com e partecipare a una conferenza telefonica con accesso esterno. Per eseguire questa attività, viene chiamato il cmdlet **Test-CsDialInConferencing** con tre parametri, ovvero TargetFqdn (il nome di dominio completo del pool di registrazione), UserCredential (l'oggetto di Windows PowerShell contenente le credenziali utente di Pilar Ackerman) e UserSipAddress (l'indirizzo SIP corrispondente alle credenziali utente fornite).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsDialInConferencing -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress "sip:pilar@litwareinc.com" -UserCredential $cred1

## Descrizione dettagliata

Il cmdlet **Test-CsDialInConferencing** è un esempio di "transazione sintetica" di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere svolte manualmente da un amministratore oppure possono essere eseguite automaticamente tramite un'applicazione quale Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Le transazioni sintetiche vengono in genere condotte in due modi distinti. Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascuno dei pool di registrazione. Questi utenti di test sono coppie di utenti preconfigurati per l'utilizzo con le transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti effettivi. Con gli utenti di test configurati per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su tale pool senza dover specificare le identità (e fornire le credenziali) degli account utente coinvolti nella verifica.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando account utente effettivi. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (anziché una coppia di account di test) e provare a diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando account utente effettivi, sarà necessario fornire i nomi e le password di accesso per ogni utente.

Il cmdlet **Test-CsDialInConferencing** funziona tentando di connettere un utente di test al sistema. Se si utilizzano utenti di test, il cmdlet **Test-CsDialInConferencing** utilizzerà il primo account di test configurato per il pool. Se l'accesso riesce, il cmdlet consente di utilizzare le credenziali e le autorizzazioni dell'utente per verificare i numeri di accesso disponibili alla conferenza telefonica con accesso esterno. La corretta esecuzione o la mancata riuscita di ogni tentativo di accesso verrà registrata, quindi l'utente di test verrà disconnesso da Lync Server.

Il cmdlet **Test-CsDialInConferencing** verifica soltanto che sia possibile effettuare le connessioni appropriate. Con il cmdlet non vengono infatti effettuate chiamate telefoniche né create conferenze telefoniche con accesso esterno a cui possano partecipare altri utenti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Test-CsDialInConferencing** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialInConferencing"}

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
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo (FQDN) del pool da verificare.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>l'oggetto credenziale utente per l'account utente che deve essere verificato. Il valore passato a UserCredential deve essere un riferimento oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziale per l'utente litwareinc\davidegarghentini e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>È necessario fornire la password utente quando si esegue questo comando. Questo parametro non è necessario se si esegue la verifica utilizzando le impostazioni di configurazione del monitoraggio dell'integrità.</p></td>
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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
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
<tr class="even">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>La porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di un telefono PSTN che verrà utilizzato per verificare che gli utenti della rete PSTN possano partecipare a una conferenza telefonica con accesso esterno. Ad esempio:</p>
<p>-TargetPstnPhoneNumber &quot;+12065551219&quot;</p>
<p>Si noti che il parametro TargetPstnPhoneNumber deve essere incluso solo quando si utilizza il parametro VerifyConferenceJoinType.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>l'indirizzo SIP dell'account utente che deve essere verificato. Ad esempio: -UserSipAddress &quot;sip:davidegarghentini@litwareinc.com&quot;. Il parametro UserSipAddress deve fare riferimento allo stesso account utente di UserCredential. Questo parametro non è necessario se si esegue la verifica utilizzando le impostazioni di configurazione del monitoraggio dell'integrità.</p></td>
</tr>
<tr class="even">
<td><p><em>VerifyConferenceJoin</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, verifica che sia possibile partecipare alla conferenza telefonica con accesso esterno tramite un telefono PSTN. Per l'esecuzione di questo test è possibile includere facoltativamente il parametro TargetPstnPhoneNumber. In questo caso, il parametro TargetPstnPhoneNumber deve specificare il numero del telefono PSTN da utilizzare per partecipare alla conferenza. Se non si include TargetPstnPhoneNumber, il cmdlet <strong>Test-CsDialInConferencing</strong> utilizzerà i numeri di telefono con accesso esterno preassegnati all'area di conferenza telefonica con accesso esterno appropriata.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsDialInConferencing** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsDialInConferencing** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsAVConference](test-csavconference.md)

