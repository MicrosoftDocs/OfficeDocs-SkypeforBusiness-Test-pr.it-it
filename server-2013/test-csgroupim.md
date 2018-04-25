---
title: Test-CsGroupIM
TOCTitle: Test-CsGroupIM
ms:assetid: 1e73fd7a-5727-4688-8d4c-a3107c3985e9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398273(v=OCS.15)
ms:contentKeyID: 49299876
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsGroupIM

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di due utenti di condurre una conferenza di messaggistica istantanea. Il cmdlet **Test-CsGroupIM** è una "transazione sintetica", ovvero una simulazione delle normali attività di Lync Server per monitorare l'integrità e le prestazioni. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsGroupIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsGroupIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsGroupIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-TestJoinLauncher <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene effettuato un controllo per verificare se due utenti test preconfigurati sono in grado di accedere al pool atl-cs-001.litwareinc.com e quindi prendere parte a una conferenza di messaggistica istantanea. ‎Questo comando potrà essere eseguito correttamente solo se sono stati definiti utenti test per il pool atl-cs-001.litwareinc.com. In caso affermativo, il comando determina se i due utenti test possono accedere al sistema e se sono in grado di partecipare a una conferenza di messaggistica istantanea.

Se non sono stati definiti utenti di test, il comando avrà esito negativo in quanto non sarà in grado di stabilire con quali utenti effettuare il test. Se non è stato definito alcun utente di test per un pool, è necessario includere i parametri SenderSipAddress e ReceiverSipAddress e le credenziali corrispondenti per gli utenti coinvolti nella sessione di messaggistica istantanea. Le verifiche verranno quindi eseguite dal cmdlet **Test-CsGroupIM** utilizzando i due utenti specificati.

    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se due utenti (litwareinc\\pilar e litwareinc\\kenmyer) sono in grado di accedere a Lync Server e quindi partecipare a una conferenza di messaggistica istantanea. Per ottenere questo risultato, il primo comando nell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali Windows PowerShell contenente nome e password dell'utente Pilar Ackerman. Dal momento che il nome di accesso (litwareinc\\pilar) è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà solo immettere la password per l'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato nella variabile denominata $cred1. Il secondo comando esegue la stessa operazione, ma questa volta restituisce un oggetto credenziali per l'account Ken Myer.

Con i due oggetti credenziali disponibili, il terzo comando dell'esempio determina se i due utenti sono o meno in grado di eseguire l'accesso a Lync Server e quindi di partecipare a una conferenza di messaggistica istantanea. A tale scopo, viene chiamato il cmdlet **Test-CsGroupIM** con i parametri seguenti: TargetFqdn (nome di dominio completo del pool di registrazione), SenderSipAddress (indirizzo SIP del primo utente), SenderCredential (credenziali del primo utente), ReceiverSipAddress (indirizzo SIP del secondo utente) e ReceiverCredential (credenziali del secondo utente).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsGroupIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsGroupIM** è un esempio di transazione sintetica di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di completare correttamente normali attività, quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono sulla rete PSTN (Public Switched Telephone Network). Questi test possono essere eseguiti manualmente da un amministratore oppure automaticamente da un'applicazione, ad esempio Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Per eseguire le transazioni sintetiche è possibile procedere in due modi. Alcuni amministratori utilizzano i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascun pool di registrazione. Si tratta di un certo numero di utenti che sono stati appositamente preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test che non appartengono a utenti reali. Dopo aver configurato gli utenti di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su quel pool senza dover specificare le identità o fornire le credenziali degli account utente coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando degli account utente reali. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (piuttosto che degli account utente di test) per cercare di diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando degli account utente reali, ricordare che sarà necessario fornire le credenziali di tutti gli utenti coinvolti.

Il cmdlet **Test-CsGroupIM** consente di verificare che gli utenti dell'organizzazione possano condurre conferenze. Per eseguire i test, il cmdlet **Test-CsGroupIM** richiede due account utente. Se sono già stati configurati gli utenti di test per il pool su cui verrà eseguito il test, non sarà necessario specificare questi account, in quanto il cmdlet **Test-CsGroupIM** utilizzerà automaticamente gli account di test assegnati al pool. Per informazioni dettagliate, vedere l'argomento relativo al cmdlet [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md) nella Guida. In alternativa, è possibile eseguire il test utilizzando account diversi da quelli assegnati alla funzione di registrazione. Ciò consente di eseguire i test anche nel caso in cui non siano stati configurati utenti di test per il pool. Questa soluzione consente inoltre di testare la capacità di due utenti specifici di condurre una conferenza. Se si sceglie questo metodo, sarà necessario specificare nome utente e password per entrambi gli utenti.

Quando si utilizza il cmdlet **Test-CsGroupIM**, il cmdlet tenta di eseguire l'accesso a Lync Server per entrambi gli utenti. Se l'accesso riesce, il cmdlet **Test-CsGroupIM** crea una nuova conferenza utilizzando il primo utente di test, quindi invita il secondo utente a parteciparvi. Dopo uno scambio di messaggi, entrambi gli utenti vengono disconnessi dal sistema. Tutta la procedura viene eseguita senza alcuna interazione da parte degli utenti e senza coinvolgere alcun utente effettivo. Ad esempio, si supponga che l'account di test sip:kenmyer@litwareinc.com corrisponda a un utente reale con un account di Lync Server reale. In questo caso, il test verrà eseguito senza interrompere l'attività del vero Ken Myer. Ad esempio, anche quando l'account di test di Ken Myer si disconnette, il vero Ken Myer resterà connesso al sistema. Allo stesso modo, il vero Ken Myer non riceverà l'invito a partecipare alla conferenza. L'invio verrà inviato all'account di test e accettato da quest'ultimo.

Se si aggiunge il parametro Verbose, è possibile ottenere una descrizione dettagliata di tutte le azioni eseguite dal cmdlet **Test-CsGroupIM** per completare il test.

Utenti autorizzati a utilizzare questo cmdlet: Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsGroupIM"}

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
<td><p>L'oggetto credenziali utente per il primo dei due account utente da sottoporre a test. Il valore specificato per il parametro ReceiverCredential deve essere un riferimento oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\pilar e lo memorizza nella variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando.</p>
<p>Le credenziali del destinatario non sono necessarie se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>L'oggetto credenziali utente per il secondo dei due account utente da sottoporre a test. Il valore specificato per il parametro SenderCredential deve essere un riferimento oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e lo memorizza nella variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando.</p>
<p>Le credenziali del mittente non sono necessarie se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
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
<td><p>SipSyntheticTransaction + AuthenticationMechanism</p></td>
<td><p>Tipo di autenticazione utilizzato nel test. I valori consentiti sono:</p>
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
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del primo dei due account utente da testare, ad esempio: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro ReceiverSipAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
<p>L'indirizzo SIP non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del secondo dei due account utente da testare, ad esempio: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro SenderSipAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestJoinLauncher</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se specificato, questo parametro verifica la capacità del componente Join Launcher di partecipare a una conferenza audio/video. Join Launcher viene utilizzato per consentire agli utenti di dispositivi mobili e di conseguenza agli utenti del servizio per dispositivi mobili di partecipare alle conferenze.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsGroupIM** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsGroupIM** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsIM](test-csim.md)

