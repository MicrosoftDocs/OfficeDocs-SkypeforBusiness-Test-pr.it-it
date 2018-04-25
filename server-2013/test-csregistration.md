---
title: Test-CsRegistration
TOCTitle: Test-CsRegistration
ms:assetid: 9e38cb36-c97a-43f2-97fe-64759f663be2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412737(v=OCS.15)
ms:contentKeyID: 49301476
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsRegistration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se un utente è in grado di accedere a Lync Server. Il cmdlet **Test-CsRegistration** è una "transazione sintetica", ovvero una simulazione delle normali attività di Lync Server per monitorare le prestazioni e lo stato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsRegistration -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsRegistration -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsRegistration [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene verificato il servizio di registrazione per il pool atl-cs-001.litwareinc.com. ‎Questo comando potrà essere eseguito correttamente solo se sono stati definiti utenti di test per il pool atl-cs-001.litwareinc.com. In questo caso, il comando consente di stabilire se il primo utente di test è in grado di accedere a Lync Server.

Se gli utenti di test non sono stati definiti, il comando avrà esito negativo in quanto non sarà in grado di stabilire con quale account utente tentare di accedere al sistema. Se non sono stati definiti gli utenti di test per un pool, è necessario includere il parametro UserSipAddress e le credenziali dell'utente che il comando dovrà utilizzare quando tenta di eseguire l'accesso.

    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

I comandi riportati nell'esempio 2 consentono di verificare se un utente specifico (litwareinc\\pilar) è in grado di accedere a Lync Server. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Get-Credential** per creare un oggetto credenziali di Windows PowerShell contenente nome e password dell'utente Pilar Ackerman. Dal momento che il nome di accesso litwareinc\\pilar è stato incluso come parametro, nella finestra di dialogo per la richiesta delle credenziali di Windows PowerShell l'amministratore dovrà solo immettere la password per l'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1.

Il secondo comando consente di verificare se questo utente può accedere al pool atl-cs-001.litwareinc.com. A tale scopo, viene chiamato il cmdlet **Test-CsRegistration** con tre parametri: TargetFqdn (il nome di dominio completo del pool di registrazione), UserCredential (l'oggetto Windows PowerShell contenente le credenziali utente di Pilar Ackerman) e UserSipAddress (l'indirizzo SIP corrispondente alle credenziali utente fornite).

    $cred1 = Get-Credential "litwareinc\pilar"
    
    Test-CsRegistration -TargetFqdn atl-cs-001.litwareinc.com -UserCredential $cred1 -UserSipAddress "sip:pilar@litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Test-CsRegistration** è un esempio di "transazione sintetica" di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite manualmente da un amministratore oppure automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Per eseguire le transazioni sintetiche è possibile procedere in due modi. Alcuni amministratori utilizzano i cmdlet CsHealthMonitoringConfiguration per configurare utenti di test per ciascun pool di registrazione. Si tratta di un certo numero di utenti che sono stati appositamente preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test che non appartengono a utenti reali. Dopo aver configurato gli utenti di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su quel pool senza dover specificare le identità o fornire le credenziali degli account utente coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando degli account utente reali. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (piuttosto che degli account utente di test) per cercare di diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando degli account utente reali sarà necessario fornire i nomi e le password di accesso di tutti gli utenti coinvolti.

Il cmdlet **Test-CsRegistration** consente di verificare che gli utenti dell'organizzazione possano accedere a Lync Server. Per eseguire questa verifica, il cmdlet **Test-CsRegistration** necessita di un singolo account di test. Se sono già stati configurati gli utenti di test per il pool su cui verrà eseguito il test, non sarà necessario specificare un account, poiché il cmdlet **Test-CsRegistration** utilizzerà automaticamente il primo account di test assegnato al pool. Per informazioni dettagliate, vedere l'argomento relativo al cmdlet [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md) nella Guida. In alternativa, è possibile eseguire la verifica utilizzando un account che non è stato assegnato al pool. In questo modo è possibile eseguire verifiche anche nel caso in cui non siano stati configurati utenti di test. Questa soluzione inoltre consente di testare la capacità di uno specifico utente di accedere a Lync Server. Se si sceglie questo metodo, sarà necessario fornire nome utente e password dell'account da verificare.

Quando viene eseguito, il cmdlet **Test-CsRegistration** tenta di eseguire l'accesso a Lync Server con l'account utente di test e, se l'operazione riesce, disconnette l'utente di test dal sistema. Tutta la procedura viene eseguita senza alcuna interazione da parte degli utenti e senza che questi vengano coinvolti. Si supponga ad esempio che l'account di test sip:kenmyer@litwareinc.com corrisponda a un utente reale con un account Lync Server reale. In questo caso, il test verrà eseguito senza coinvolgere Ken Myer. Quando l'account di test di Ken Myer si disconnette, il vero Ken Myer resterà connesso al sistema.

Se si aggiunge il parametro Verbose, è possibile ottenere una descrizione dettagliata di tutte le azioni eseguite dal cmdlet **Test-CsRegistration** per completare il test.

Utenti autorizzati a utilizzare questo cmdlet: Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsRegistration"}

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
<td><p>Oggetto credenziali utente dell'account da verificare. Il valore passato a UserCredential deve essere un riferimento all'oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e lo archivia in una variabile denominata</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando. Questo parametro non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato nella verifica. I valori consentiti sono:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
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
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'account utente da sottoporre a test, ad esempio, -UserSipAddress &quot;sip:davidegarghentini@litwareinc.com&quot;. Il parametro UserSipAddress deve fare riferimento allo stesso account utente di UserCredential. Questo parametro non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsRegistration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsRegistration** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

