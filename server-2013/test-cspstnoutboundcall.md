---
title: Test-CsPstnOutboundCall
TOCTitle: Test-CsPstnOutboundCall
ms:assetid: 12d940c3-8526-4c8f-8dc1-3fe65a3211bc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398207(v=OCS.15)
ms:contentKeyID: 49299749
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPstnOutboundCall

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la capacità di un utente di effettuare una chiamata a un numero di telefono sulla rete PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsPstnOutboundCall -TargetPstnPhoneNumber <String> -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall -TargetFqdn <String> -TargetPstnPhoneNumber <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsPstnOutboundCall [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene effettuato un controllo per verificare se un utente test preconfigurato è in grado di accedere al pool atl-cs-001.litwareinc.com e quindi viene effettuata una chiamata sul gateway PSTN. ‎Questo comando potrà essere eseguito correttamente solo se sono stati definiti gli utenti test per il pool atl-cs-001.litwareinc.com. In caso affermativo, il comando stabilisce se il primo utente test può accedere al sistema e, in tal caso, chiamare un telefono sulla rete PSTN.

Se gli utenti di test non sono stati definiti, il comando avrà esito negativo in quanto non sarà in grado di stabilire con quale utente effettuare il test. Se non è stato definito alcun utente di test per un pool, sarà necessario includere il parametro UserSipAddress e le credenziali corrispondenti per l'account utente coinvolto nel test. Il cmdlet **Test-CsPstnOutboundCall** quindi eseguirà le verifiche utilizzando l'utente specificato.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" 

## ESEMPIO 2

I comandi riportati nell'esempio 2 verificano se un utente test (litwareinc\\kenmyer) è in grado di accedere aLync Server e di effettuare una chiamata telefonica sul gateway PSTN. Per ottenere questo risultato, il primo comando nell'esempio utilizza il cmdlet **Get-Credential** per creare un oggetto credenziali Windows PowerShell contenente nome e password dell'utente Ken Myer. Dal momento che il nome di accesso litwareinc\\kenmyer è stato incluso come parametro, nella risultante finestra di dialogo Richiesta credenziali di Windows PowerShell, l'amministratore dovrà solo immettere la password per l'account di Ken Myer. L'oggetto credenziali risultante viene quindi archiviato nella variabile denominata $cred1.

Con l'oggetto credenziali disponibile, il secondo comando dell'esempio determina se l'utente di test è in grado di eseguire l'accesso a Lync Server e quindi di effettuare una chiamata al numero telefonico di destinazione (+15551234567). A tale scopo, viene chiamato il cmdlet **Test-CsPstnOutboundCall** con i parametri seguenti: TargetFqdn (FQDN del pool di registrazione), UserSipAddress (indirizzo SIP dell'utente che deve effettuare la chiamata), UserCredential (oggetto di Windows PowerShell contenente le credenziali dell'utente di test) e TargetPstnPhoneNumber (numero di telefono da chiamare).

    $cred1 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -TargetPstnPhoneNumber "+15551234567" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred1

## ESEMPIO 3

Nell'esempio 3 viene illustrato come utilizzare il cmdlet **Test-CsPstnOutboundCall** in modalità piattaforma server. In questa modalità viene specificato l'indirizzo SIP dell'utente, ma non vengono incluse le relative credenziali. Se viene eseguito in questa modalità, Lync Server utilizza i certificati per autenticare l'utente di test.

    Test-CsPstnOutboundCall -TargetFqdn atl-cs-001.litwareinc.com -UserSipAddress sip:kenmyer@litwareinc.com -TargetPstnPhoneNumber "+15551234567"

## Descrizione dettagliata

Il cmdlet **Test-CsPstnOutboundCall** è un esempio di "transazione sintetica" di Lync Server. Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di completare correttamente normali attività, quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono sulla rete PSTN (Public Switched Telephone Network). Questi test possono essere eseguiti manualmente da un amministratore oppure automaticamente da un'applicazione, ad esempio Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

Per eseguire le transazioni sintetiche è possibile procedere in due modi. Alcuni amministratori utilizzano i cmdlet **CsHealthMonitoringConfiguration** per configurare utenti di test per ciascun pool di registrazione. Si tratta di un certo numero di utenti che sono stati appositamente preconfigurati per essere utilizzati nell'ambito delle transazioni sintetiche. Generalmente si tratta di account di test che non appartengono a utenti reali. Dopo aver configurato gli utenti di test per un pool, gli amministratori possono semplicemente eseguire una transazione sintetica su quel pool senza dover specificare le identità o fornire le credenziali degli account utente coinvolti nel test.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando degli account utente reali. Ad esempio, se due utenti non sono in grado di scambiare messaggi istantanei, un amministratore potrebbe eseguire una transazione sintetica utilizzando i due account utente in questione (piuttosto che degli account utente di test) per cercare di diagnosticare e risolvere il problema. Se si decide di eseguire una transazione sintetica utilizzando degli account utente reali sarà necessario fornire i nomi e le password di accesso di tutti gli utenti coinvolti.

Test-CsPstnOutboundCall può essere utilizzato anche in modalità piattaforma server. In quel caso è necessario solo specificare l'indirizzo SIP di un utente e Lync Server utilizzerà i certificati per autenticare l'utente.

Quando si esegue il cmdlet **Test-CsPstnOutboundCall**, il cmdlet tenta innanzitutto di eseguire l'accesso a Lync Server per l'utente di test. Se l'accesso riesce, il cmdlet tenterà di effettuare una chiamata telefonica attraverso il gateway PSTN. Questa chiamata telefonica verrà effettuata utilizzando il dial plan, il criterio vocale e altri criteri e impostazioni assegnati all'account di test. Quando viene data risposta alla chiamata, il cmdlet invia codici DTMF sulla rete per verificare la connettività multimediale.

Nel corso del test il cmdlet **Test-CsPstnOutboundCall** effettuerà una vera chiamata telefonica, pertanto il telefono di destinazione squillerà e sarà necessario rispondere affinché il test possa considerarsi riuscito. Questa chiamata inoltre deve essere terminata manualmente dall'amministratore.

Utenti autorizzati a utilizzare questo cmdlet: Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsPstnOutboundCall"}

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
<td><p><em>TargetPstnPhoneNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Numero telefonico sulla rete PSTN da chiamare nel corso del test. Il numero telefonico di destinazione viene meglio specificato se si utilizza il formato E.164, ciò significa che il numero assomiglierà a questo &quot;+14255551298&quot;, un numero che contiene il segno più (+) seguito dal prefisso internazionale (1), dal prefisso locale (425) e dal numero telefonico (5551298). Non utilizzare trattini, parentesi o altri caratteri quando si specifica il numero telefonico.</p>
<p>Se non si utilizza il formato E.164, al numero telefonico verrà aggiunto il dial plan dell'utente test. Lync Server utilizzerà quindi questo dial plan per normalizzare il numero nel formato E.164. Se il numero non può essere normalizzato, non sarà possibile effettuare la chiamata e il test avrà esito negativo.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente dell'account da sottoporre a test. Il valore passato al parametro UserCredential deve essere un riferimento oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Il codice seguente ad esempio restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e lo archivia nella variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando.</p>
<p>Questo parametro non è necessario se il comando sta utilizzando gli utenti test configurati con i cmdlet CsHealthMonitoringConfiguration. Non è necessario specificare questo parametro anche se si sta eseguendo il test in modalità piattaforma server. In tal caso, Lync Server tenterà di autenticare l'utente utilizzando i certificati.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
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
<td><p>System.String</p></td>
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
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'account utente da sottoporre a test. Ad esempio: -SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro UserSipAddress deve fare riferimento allo stesso account utente di UserCredential.</p>
<p>Questo parametro non è necessario se il comando sta utilizzando gli utenti di test configurati con i cmdlet CsHealthMonitoringConfiguration.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsPstnOutboundCall** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsPstnOutboundCall** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsPstnPeerToPeerCall](test-cspstnpeertopeercall.md)

