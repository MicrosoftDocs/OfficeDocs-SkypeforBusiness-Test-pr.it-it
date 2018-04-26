---
title: Test-CsAVConference
TOCTitle: Test-CsAVConference
ms:assetid: a1492563-9a97-44ac-b19a-8d5972cdd062
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412749(v=OCS.15)
ms:contentKeyID: 49301521
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAVConference

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se due utenti possono partecipare a una conferenza audio/video (A/V). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsAVConference -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAVConference -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAVConference [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene verificato se una coppia di utenti di test preconfigurati può accedere al pool atl-cs-001.litwareinc.com e quindi partecipare a una conferenza A/V. Il comando funzionerà soltanto se sono stati definiti utenti di test per il pool atl-cs-001.litwareinc.com. In questo caso, il comando determinerà se i due utenti possono eseguire l'accesso al sistema. In caso affermativo, il primo utente di test creerà una conferenza A/V e inviterà il secondo utente a partecipare. Il cmdlet verificherà quindi se i due utenti di test sono stati in grado o meno di effettuare una connessione.

Se non sono stati definiti utenti di test, il comando avrà esito negativo in quanto non sarà in grado di stabilire l'account utente da utilizzare per effettuare la verifica. Se non sono stati definiti utenti di test per un pool, sarà necessario includere i parametri SenderSipAddress e ReceiverSipAddress, nonché le credenziali corrispondenti degli utenti coinvolti nello scambio di messaggi istantanei. Il cmdlet **Test-CsAVConference** effettuerà quindi le verifiche utilizzando i due utenti specificati.

    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se due utenti (litwareinc\\pilar e litwareinc\\kenmyer) sono in grado di accedere a Lync Server e quindi partecipare a una conferenza A/V. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali di Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché il nome di accesso litwareinc\\pilar è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà solo immettere la password dell'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1. Il secondo comando effettua la stessa operazione, questa volta restituendo un oggetto credenziali per l'account di Ken Myer.

Disponendo dei due oggetti credenziali, il terzo comando dell'esempio stabilisce se i due utenti sono o meno in grado di accedere a Lync Server e quindi di partecipare a una conferenza A/V. A tale scopo, viene chiamato il cmdlet **Test-CsAVConference** con i parametri seguenti: TargetFqdn (FQDN del pool di registrazione), SenderSipAddress (indirizzo SIP del primo utente di test), SenderCredential (oggetto di Windows PowerShell contenente le credenziali di questo stesso utente), ReceiverSipAddress (indirizzo SIP dell'altro utente di test) e ReceiverCredential (oggetto di Windows PowerShell contenente le credenziali dell'altro utente).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAVConference -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsAVConference** è un esempio di "transazione sintetica". Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite manualmente da un amministratore oppure automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Le transazioni sintetiche vengono in genere condotte in due modi distinti. Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascun pool di registrazione. Questi utenti di test sono una coppia di utenti preconfigurati per l'utilizzo con le transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti effettivi. Dopo aver configurato gli utenti di test per un pool, gli amministratori possono eseguire una transazione sintetica sul pool senza dover specificare le identità e fornire le credenziali degli account utente coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando account utente effettivi. Se ad esempio due utenti non sono in grado di scambiare messaggi istantanei, un amministratore può eseguire una transazione sintetica utilizzando i due account utente (anziché una coppia di account di test) e provare quindi a diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando account utente effettivi, sarà necessario fornire i nomi e le password di accesso di ogni utente.

Il cmdlet **Test-CsAVConference** verifica se i due utenti di test sono in grado di eseguire una conferenza A/V. Quando viene eseguito il cmdlet, i due utenti vengono connessi al sistema. Dopo aver eseguito l'accesso, il primo utente crea una conferenza A/V e quindi attende che il secondo utente partecipi alla conferenza. Dopo un breve scambio di dati, la conferenza viene eliminata e i due utenti vengono disconnessi.

Il cmdlet **Test-CsAVConference** non esegue effettivamente una conferenza A/V tra i due utenti di test. Il cmdlet piuttosto verifica che i due utenti possano creare le connessioni necessarie per effettuare tale conferenza.

Utenti autorizzati a eseguire il cmdlet: per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAVConference"}

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
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore passato a ReceiverCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il seguente codice ad esempio restituisce un oggetto credenziali dell'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>È necessario fornire la password utente quando si esegue questo comando.</p>
<p>Le credenziali del destinatario non sono necessarie se si esegue il test con le impostazioni di configurazione per il monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore passato a SenderCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, con il codice seguente viene restituito un oggetto credenziale per l'utente litwareinc\davidegarghentini e tale oggetto viene archiviato in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\davidegarghentini&quot;</p>
<p>È necessario fornire la password utente quando si esegue questo comando.</p>
<p>Le credenziali del mittente non sono necessarie se si esegue il test con le impostazioni di configurazione per il monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da testare.</p></td>
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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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
<td><p>Indirizzo SIP del primo dei due account utente da testare. Ad esempio: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro ReceiverSipAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue il test con le impostazioni di configurazione per il monitoraggio dell'integrità del pool.</p></td>
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
<td><p>Indirizzo SIP del secondo dei due account utente da verificare. Ad esempio: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro SenderSIPAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue il test con le impostazioni di configurazione per il monitoraggio dell'integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se presente, verifica la possibilità di Join Launcher di partecipare a una conferenza A/V. Join Launcher viene utilizzato per facilitare la partecipazione degli utenti di dispositivi mobili, e di conseguenza degli utenti del servizio per dispositivi mobili, alle conferenze.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Test-CsAVConference** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)  
[Test-CsDialInConferencing](test-csdialinconferencing.md)

