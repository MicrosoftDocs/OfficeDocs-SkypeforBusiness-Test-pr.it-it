---
title: Test-CsP2PAV
TOCTitle: Test-CsP2PAV
ms:assetid: acb01fb7-4685-4f38-a724-8c2ae8e0219a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412821(v=OCS.15)
ms:contentKeyID: 49301636
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsP2PAV

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se due utenti sono in grado di effettuare una chiamata audio/video (A/V) peer-to-peer. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsP2PAV -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsP2PAV -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsP2PAV [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene verificato se una coppia di utenti di test preconfigurati può accedere al pool atl-cs-001.litwareinc.com e quindi effettuare una chiamata audio/video peer-to-peer. Il comando funzionerà soltanto se sono stati definiti utenti di test per il pool atl-cs-001.litwareinc.com. In questo caso, il comando determinerà se i due utenti possono eseguire l'accesso al sistema e, in caso affermativo, se possono conversare mediante una chiamata audio/video.

Se non sono stati definiti utenti di test, il comando avrà esito negativo in quanto non sarà in grado di stabilire l'account utente da utilizzare per effettuare la verifica. Se non sono stati definiti utenti di test per un pool, sarà necessario includere i parametri SenderSipAddress e ReceiverSipAddress, nonché le credenziali corrispondenti degli utenti coinvolti nello scambio di messaggi istantanei. Il cmdlet **Test-CsP2PAV** effettuerà quindi le verifiche utilizzando i due utenti specificati.

    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se una coppia di utenti (litwareinc\\pilar e litwareinc\\kenmyer) può accedere a Lync Server ed effettuare quindi una chiamata audio/video peer-to-peer. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali di Windows PowerShell contenente il nome e la password dell'utente Pilar Ackerman. Poiché il nome di accesso litwareinc\\pilar è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà esclusivamente immettere la password dell'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1. Il secondo comando effettua la stessa operazione, questa volta restituendo un oggetto credenziali per l'account di Ken Myer.

Con i due oggetti credenziali disponibili, il terzo comando dell'esempio determina se i due utenti possono accedere a Lync Server ed effettuare una chiamata audio/video peer-to-peer. A tale scopo, viene chiamato il cmdlet **Test-CsP2PAV** con i parametri seguenti: TargetFqdn (nome di dominio completo del pool di registrazione), SenderSipAddress (indirizzo SIP del primo utente di test), SenderCredential (oggetto di Windows PowerShell contenente le credenziali per lo stesso utente), ReceiverSipAddress (indirizzo SIP dell'altro utente di test) e ReceiverCredential (oggetto di Windows PowerShell contenente le credenziali dell'altro utente di test).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsP2PAV** è un esempio di "transazione sintetica" di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite manualmente da un amministratore oppure automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Le transazioni sintetiche vengono in genere condotte in due modi distinti. Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascun pool di registrazione. Questi utenti di test sono una coppia di utenti preconfigurati per l'utilizzo con le transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti effettivi. Dopo aver configurato gli utenti di test per un pool, gli amministratori possono limitarsi a eseguire una transazione sintetica sul pool senza dover specificare le identità e fornire le credenziali degli account utente coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando account utente effettivi. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (anziché una coppia di account di test) e provare a diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando account utente effettivi, sarà necessario fornire i nomi e le password di accesso di ogni utente.

Il cmdlet **Test-CsP2PAV** viene utilizzato per determinare se due utenti di test sono in grado di partecipare a una conversazione audio/video (A/V) peer-to-peer. Per verificare questo scenario, il cmdlet inizia connettendo i due utenti a Lync Server. Presupponendo che i due accessi abbiano esito positivo, il primo utente invita quindi il secondo utente a partecipare a una chiamata A/V. Dopo che il secondo utente ha accettato la chiamata, viene testata la connessione tra i due utenti e quindi la chiamata viene terminata e gli utenti di test vengono disconnessi dal sistema.

Il cmdlet **Test-CsP2PAV** non esegue effettivamente una chiamata A/V e non vengono scambiate informazioni multimediali tra gli utenti di test. Il cmdlet invece verifica semplicemente che sia possibile effettuare le connessioni appropriate e che i due utenti siano in grado di eseguire una chiamata di questo tipo.

Utenti autorizzati a eseguire il cmdlet: per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsP2PAV"}

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
<td><p>Indirizzo SIP del primo dei due account utente da verificare. Ad esempio: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro ReceiverSipAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
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
<td><p>Indirizzo SIP del secondo dei due account utente da testare. Ad esempio: -SenderSipAddress &quot;sip:davidegarghentini@litwareinc.com&quot;. Il parametro SenderSipAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si esegue il test con le impostazioni di configurazione per il monitoraggio dell'integrità del pool.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsP2PAV** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsP2PAV** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsAVConference](test-csavconference.md)

