---
title: Test-CsIM
TOCTitle: Test-CsIM
ms:assetid: 2fdab54c-5ec4-4db5-b29c-a3efaae68f66
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425802(v=OCS.15)
ms:contentKeyID: 49300071
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsIM

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di due utenti di scambiare messaggi istantanei. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-EmailHost <String>] [-Force <SwitchParameter>] [-IsSsl <$true | $false>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-Password <String>] [-Port <UInt16>] [-TestLegalIntercept <SwitchParameter>] [-Username <String>] [-WaitSeconds <Int16>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene effettuato un controllo per verificare se due utenti test preconfigurati sono in grado di accedere al pool atl-cs-001.litwareinc.com e quindi scambiare messaggi istantanei. ‎Questo comando potrà essere eseguito correttamente solo se sono stati definiti utenti test per il pool atl-cs-001.litwareinc.com. In caso affermativo, il comando stabilisce se i due utenti possono accedere al sistema e, in tal caso, scambiare messaggi istantanei.

Se non sono stati definiti utenti di test, il comando avrà esito negativo perché non sarà in grado di stabilire con quali utenti effettuare il test. Se non è stata definita una funzione di registrazione per un pool, sarà necessario includere i parametri SenderSipAddress e ReceiverSipAddress oltre alle credenziali corrispondenti per gli utenti coinvolti nella sessione di messaggistica istantanea. Le verifiche verranno quindi eseguite dal cmdlet **Test-CsIM** utilizzando i due utenti specificati.

    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se due utenti (litwareinc\\pilar e litwareinc\\kenmyer) sono in grado di accedere a Lync Server e quindi di scambiarsi messaggi istantanei. Per ottenere questo risultato, il primo comando nell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali Windows PowerShell contenente nome e password dell'utente Pilar Ackerman. Dal momento che il nome di accesso (litwareinc\\pilar) è stato incluso come parametro, nella finestra di dialogo Richiesta credenziali di Windows PowerShell l'amministratore dovrà solo immettere la password per l'account di Pilar Ackerman. L'oggetto credenziali risultante viene quindi archiviato nella variabile denominata $cred1. Il secondo comando esegue la stessa operazione, ma questa volta restituisce un oggetto credenziali per l'account Ken Myer.

Con i due oggetti credenziali disponibili, il terzo comando dell'esempio determina se i due utenti sono o meno in grado di eseguire l'accesso a Lync Server e quindi di scambiare messaggi istantanei. A tale scopo, viene chiamato il cmdlet **Test-CsIM** con i parametri seguenti: TargetFqdn (l'FQDN del pool di registrazione), SenderSipAddress (l'indirizzo SIP del primo utente di test), SenderCredential (l'oggetto di Windows PowerShell contenente le credenziali di questo utente), -ReceiverSipAddress (l'indirizzo SIP dell'altro utente di test) e ReceiverCredential (l'oggetto di Windows PowerShell contenente le credenziali dell'altro utente).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsIm -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

## Descrizione dettagliata

Il cmdlet **Test-CsIM** è un esempio di "transazione sintetica" di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di completare correttamente normali attività, quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono sulla rete PSTN (Public Switched Telephone Network). Questi test possono essere eseguiti manualmente da un amministratore oppure automaticamente da un'applicazione, ad esempio Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Per eseguire le transazioni sintetiche è possibile procedere in due modi. Alcuni amministratori utilizzano il cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascun pool di registrazione. Si tratta di un certo numero di utenti che sono stati appositamente preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test che non appartengono a utenti reali. Dopo aver configurato gli utenti di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su quel pool senza dover specificare le identità o fornire le credenziali degli account utente coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando degli account utente reali. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (piuttosto che degli account utente di test) per cercare di diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando degli account utente reali, ricordare che sarà necessario fornire le credenziali di tutti gli utenti coinvolti.

Il cmdlet **Test-CsIM** innanzitutto tenta di eseguire l'accesso a Lync Server per due utenti di test. Presupponendo che entrambi gli accessi abbiano esito positivo, il cmdlet avvia una sessione di messaggistica istantanea tra i due utenti di test. L'utente 1 invita l'utente 2 a partecipare a una sessione di messaggistica istantanea e l'utente 2 accetta l'invito. Dopo avere verificato che i due utenti possono scambiarsi messaggi, il cmdlet **Test-CsIM** termina la sessione di messaggistica istantanea e disconnette entrambi gli utenti dal sistema.

Utenti autorizzati a utilizzare questo cmdlet: Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsIM"}

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
<td><p><em>EmailHost</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Host di posta elettronica dell'utente utilizzato nel test Legal Intercept, ad esempio:</p>
<p>-EmailHost &quot;litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>IsSsl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, specifica che il test viene eseguito utilizzando il protocollo SSL (Secure Socket Layer).</p></td>
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
<td><p><em>Password</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Password dell'utente utilizzato per il test Legal Intercept.</p></td>
</tr>
<tr class="odd">
<td><p><em>Port</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>UInt16</p></td>
<td><p>Porta utilizzata per il servizio Legal Intercept.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP per il primo dei due account utente da sottoporre a test. Ad esempio: -ReceiverSipAddress &quot;sip:jhaas@litwareinc.com&quot;. Il parametro ReceiverSipAddress deve fare riferimento allo stesso account utente di ReceiverCredential.</p>
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
<td><p>L'indirizzo SIP del secondo dei due account utente da sottoporre a test. Ad esempio: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro SenderSipAddress deve fare riferimento allo stesso account utente di SenderCredential.</p>
<p>L'indirizzo SIP non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato di integrità del pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TestLegalIntercept</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Se utilizzato, questo parametro indica a Test-CsIM di testare il servizio Legal Intercept per l'utente specificato.</p></td>
</tr>
<tr class="even">
<td><p><em>Username</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Nome dell'utente utilizzato nel test Legal Intercept.</p></td>
</tr>
<tr class="odd">
<td><p><em>WaitSeconds</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int16</p></td>
<td><p>Specifica per quanti secondi il sistema deve attendere una risposta dal servizio Legal Intercept.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsIM** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsIM** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsGroupIM](test-csgroupim.md)

