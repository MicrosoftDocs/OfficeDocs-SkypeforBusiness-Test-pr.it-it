---
title: Test-CsPresence
TOCTitle: Test-CsPresence
ms:assetid: 09a5faf6-4e80-4a3b-ac84-aec9778ee9b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398148(v=OCS.15)
ms:contentKeyID: 49299620
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPresence

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di un utente di accedere a Lync Server, pubblicare le proprie informazioni sulla presenza e sottoscrivere le informazioni sulla presenza pubblicate da un secondo utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsPresence -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-PublisherSipAddress <String>] [-RegistrarPort <Int32>] [-SubscriberSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPresence -PublisherCredential <PSCredential> -PublisherSipAddress <String> -SubscriberCredential <PSCredential> -SubscriberSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPresence [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-SubscriberSipAddress <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene effettuato un controllo per stabilire se una coppia di utenti di test preconfigurati è in grado di accedere al pool atl-cs-001.litwareinc.com. Dopo l'accesso degli utenti di test, il cmdlet **Test-CsPresence** verifica se i due utenti sono in grado di scambiare le informazioni sulla presenza. ‎Questo comando potrà essere eseguito correttamente solo se sono stati definiti utenti di test per il pool atl-cs-001.litwareinc.com. In caso affermativo, il comando determinerà se il primo utente di test è in grado di accedere al sistema, quindi verificherà se è in grado di scambiare informazioni sulla presenza con il secondo utente di test definito per il pool.

Se non è stata definita una funzione di registrazione, il comando avrà esito negativo in quanto non sarà in grado di stabilire quali utenti utilizzare durante il test. Se non sono stati definiti utenti di test per un pool, è necessario includere i parametri SubscriberSipAddress e PublisherSipAddress oltre alle credenziali corrispondenti per gli utenti che fungono da sottoscrittore della presenza e da entità di pubblicazione della presenza. I controlli verranno quindi eseguiti dal cmdlet **Test-CsPresence** utilizzando i due utenti specificati.

    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com 

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se due utenti (litwareinc\\pilar e litwareinc\\kenmyer) sono in grado di accedere a Lync Server e quindi di scambiarsi informazioni sulla presenza. Per ottenere questo risultato, il primo comando nell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali Windows PowerShell contenente nome e password dell'utente Pilar Ackerman. Dal momento che il nome di accesso (litwareinc\\pilar) è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà solo immettere la password per l'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato nella variabile denominata $cred1. Il secondo comando esegue la stessa operazione, ma questa volta restituisce un oggetto credenziali per l'account Ken Myer.

Con i due oggetti credenziali disponibili, il terzo comando dell'esempio stabilisce se i due utenti sono o meno in grado di accedere a Lync Server e di scambiarsi le informazioni sulla presenza. A tale scopo, viene chiamato il cmdlet **Test-CsPresence** con i parametri seguenti: TargetFqdn (l'FQDN del pool di registrazione), SubscriberSipAddress (l'indirizzo SIP del primo utente di test), SubscriberCredential (l'oggetto di Windows PowerShell contenente le credenziali di questo stesso utente), PublisherSipAddress (l'indirizzo SIP dell'altro utente di test) e PublisherCredential (l'oggetto di Windows PowerShell contenente le credenziali dell'altro utente).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPresence -TargetFqdn atl-cs-001.litwareinc.com -SubscriberSipAddress "sip:pilar@litwareinc.com" -SubscriberCredential $cred1 -PublisherSipAddress "sip:kenmyer@litwareinc.com" -PublisherCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsPresence** è un esempio di transazione sintetica di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di completare correttamente normali attività, quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono sulla rete PSTN (Public Switched Telephone Network). Questi test possono essere eseguiti manualmente da un amministratore oppure automaticamente da un'applicazione, ad esempio Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Per eseguire le transazioni sintetiche è possibile procedere in due modi. Alcuni amministratori utilizzano i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascun pool di registrazione. Generalmente, si tratta di account di test che non appartengono a utenti reali. Dopo aver configurato questi account utente per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su quel pool senza dover specificare le identità e fornire le credenziali degli account utente coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando degli account utente reali. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (piuttosto che degli account utente di test) per cercare di diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando degli account utente reali sarà necessario fornire i nomi e le password di accesso di tutti gli utenti coinvolti.

Il cmdlet **Test-CsPresence** viene utilizzato per determinare se una coppia di utenti di test è in grado di accedere a Lync Server e quindi di scambiarsi informazioni sulla presenza. A tale scopo, il cmdlet innanzitutto fa accedere i due utenti al sistema. Se entrambi gli accessi riescono, il primo utente di test chiede di ricevere le informazioni sulla presenza dal secondo utente. Il secondo utente pubblica queste informazioni e il cmdlet **Test-CsPresence** verifica che le informazioni vengano trasmesse correttamente al primo utente. Dopo lo scambio delle informazioni sulla presenza, i due utenti di test vengono disconnessi da Lync Server.

Utenti autorizzati a utilizzare questo cmdlet: Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPresence"}

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
<td><p><em>PublisherCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>L'oggetto credenziali utente per il primo dei due account utente da testare. Il valore specificato per il parametro PublisherCredential deve essere un riferimento oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e lo memorizza nella variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando.</p>
<p>Le credenziali di pubblicazione non sono necessarie se si sta eseguendo il test con le impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>L'oggetto credenziali utente per il secondo dei due account utente da testare. Il valore specificato per il parametro SubscriberCredential deve essere un riferimento oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\pilar e lo memorizza nella variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando.</p>
<p>Le credenziali di sottoscrittore non sono necessarie se si sta eseguendo il test con le impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
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
<td><p><em>PublisherSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP per il primo dei due account utente da testare. Ad esempio: -PublisherSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro PublisherSipAddress deve fare riferimento allo stesso account utente di PublisherCredential.</p>
<p>L'indirizzo SIP non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SubscriberSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP del secondo dei due account utente da testare. Ad esempio: -SubscriberSipAddress &quot;sip:pilar@litwareinc.com&quot;. Il parametro SubscriberSipAddress deve fare riferimento allo stesso account utente di SubscriberCredential.</p>
<p>L'indirizzo SIP non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsPresence** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsPresence** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsRegistration](test-csregistration.md)

