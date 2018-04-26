---
title: Test-CsMcxP2PIM
TOCTitle: Test-CsMcxP2PIM
ms:assetid: 443a3b31-6f58-4570-9eaa-310e73c39e03
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690020(v=OCS.15)
ms:contentKeyID: 49300359
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsMcxP2PIM

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la possibilità per una coppia di utenti di scambiare messaggi istantanei utilizzando il servizio per dispositivi mobili Lync Server. Il servizio per dispositivi mobili consente agli utenti di cellulari come iPhone e Windows Phone di eseguire operazioni quali lo scambio di messaggi istantanei e di informazioni sulla presenza, l'archiviazione e il recupero dei messaggi in segreteria telefonica internamente anziché tramite il provider wireless e l'utilizzo di funzionalità di Lync Server come Chiamata tramite ufficio e le conferenze telefoniche con chiamata esterna. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Test-CsMcxP2PIM -ReceiverSipAddress <String> -SenderSipAddress <String> <COMMON PARAMETERS>

    Test-CsMcxP2PIM -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID> -TargetFqdn <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 verifica se una coppia di utenti, Ken Myer e Pilar Ackerman, può scambiare messaggi istantanei tramite il servizio per dispositivi mobili. Per ottenere questo risultato, i primi due comandi dell'esempio utilizzano il cmdlet **Get-Credential** per creare oggetti credenziali per i due utenti. Le credenziali per Ken Myer vengono archiviate in una variabile denominata $credential1 e quelle per Pilar Ackerman vengono archiviate in una variabile denominata $credential2.

Dopo la creazione degli oggetti credenziali, il comando finale chiama il cmdlet **Test-CsMcxP2PIM** specificando il pool di registrazione di destinazione (atl-cs-001.litwareinc.com), il tipo di autenticazione (Negotiate), nonché gli indirizzi SIP e le credenziali dei due utenti.

    $credential1 = Get-Credential "litwareinc\kenmyer"
    $credential2 = Get-Credential "litwareinc\pilar"
    
    Test-CsMcxP2PIM -TargetFqdn "atl-cs-001.litwareinc.com" -Authentication Negotiate -SenderSipAddres "sip:kenmyer@litwareinc.com" -SenderCredential $credential1 -ReceiverSipAddress "sip:packerman@litwareinc.com" -ReceiverCredential $credential2

## Descrizione dettagliata

Il servizio per dispositivi mobili Lync Server estende numerose funzionalità di Lync Server a dispositivi mobili come Apple iPhone, Windows Phone, telefoni Android e telefoni Nokia. Gli utenti possono tra l'altro utilizzare questi telefoni per scambiare messaggi istantanei e informazioni sulla presenza e per ricevere notifiche di nuovi messaggi in segreteria telefonica. Grazie al servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft), gli utenti con telefoni iPhone o Windows Phone possono ricevere queste notifiche anche se Lync Server è in esecuzione in background. Il servizio per dispositivi mobili consente inoltre alle organizzazioni di abilitare la funzionalità Chiamata tramite ufficio, con cui gli utenti possono effettuare una chiamata dal proprio cellulare e fare in modo che risulti provenire dal telefono dell'ufficio. Tramite i sistemi ID chiamante ad esempio viene visualizzato il numero dell'ufficio dell'utente anziché il numero del cellulare.

Il cmdlet **Test-CsMcxP2PIM** viene utilizzato per determinare se una coppia di utenti può scambiare messaggi istantanei utilizzando il servizio per dispositivi mobili. Si noti che l'esecuzione di questo cmdlet non richiede l'utilizzo di telefoni cellulari né comporta l'invio di messaggi istantanei. Il cmdlet verifica invece che i due utenti possano accedere a Lync Server e che tramite il servizio per dispositivi mobili possano essere stabilite le connessioni necessarie per lo scambio di messaggi istantanei tra i due utenti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Test-CsMcxP2PIM** può essere utilizzato localmente dai membri dei gruppi seguenti: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dei comandi di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsMcxP2PIM"}

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
<td><p><em>Authentication</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>I valori consentiti sono: TrustedServer, Negotiate, ClientCertificate e LiveID.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il primo dei due account utente da testare. Il valore passato a ReceiverCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\pilar e archivia tale oggetto in una variabile denominata $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del primo dei due account utente da testare. Ad esempio:</p>
<p>-ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;</p>
<p>Il parametro ReceiverSipAddress deve fare riferimento allo stesso account utente del parametro ReceiverCredential.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per il secondo dei due account utente da testare. Il valore passato a SenderCredential deve essere un riferimento a un oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Il codice seguente restituisce, ad esempio, un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>Quando si esegue questo comando, è necessario specificare la password utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP del secondo dei due account utente da testare. Ad esempio:</p>
<p>-SenderSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Il parametro SenderSipAddress deve fare riferimento allo stesso account utente del parametro SenderCredential.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da testare.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, che possono quindi essere utilizzati per salvare l'output in un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile logger denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre il carattere $ quando si specifica il nome della variabile.</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile logger in un file XML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre il carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è obbligatorio se il servizio di registrazione utilizza la porta 5061 predefinita.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsMcxP2PIM** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsMcxP2PIM** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

