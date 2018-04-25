---
title: Test-CsXmppIM
TOCTitle: Test-CsXmppIM
ms:assetid: ffeb05a7-141d-46dc-936f-1f7218521ff8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205423(v=OCS.15)
ms:contentKeyID: 49302592
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsXmppIM

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica se è possibile inviare un messaggio istantaneo attraverso un gateway XMPP. I gateway XMPP consentono agli utenti di Lync Server 2013 di scambiare messaggi istantanei e informazioni sulla presenza con utenti appartenenti a provider di servizi di messaggistica istantanea e presenza che utilizzano il protocollo XMPP (Extensible Messaging and Presence Protocol). Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsXmppIM -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsXmppIM -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsXmppIM [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Receiver <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## Esempio 1

Nell'esempio precedente vengono verificate le funzionalità di messaggistica istantanea XMPP per il pool atl-cs-001.litwareinc.com. Questo comando funziona esclusivamente se sono stati definiti utenti di prova per il pool atl-cs-001.litwareinc.com. In questo caso, il comando determinerà se il primo utente di prova può inviare un messaggio istantaneo XMPP a un utente con l'indirizzo SIP adelaney@contoso.com.

Se non sono stati definiti utenti di prova, il comando avrà esito negativo perché non conoscerà l'utente tramite cui accedere. Se non si sono definiti utenti per un pool, è necessario includere il parametro UserSipAddress e le credenziali dell'utente che il comando deve utilizzare quando tenta di accedere.

    Test-CsXmppIM -TargetFqdn "atl-cs-001.litwareinc.com" -Receiver "adelany@contoso.com"

## Esempio 2

I comandi riportati nell'esempio 2 testano se un utente specifico (litwareinc\\pilar) è in grado di accedere per inviare un messaggio istantaneo XMPP all'utente adelaney@contoso.com. A tale scopo, il primo comando nell'esempio utilizza il cmdlet Get-Credential per creare un oggetto credenziali dell'interfaccia della riga di comando Windows PowerShell contenente il nome e la password dell'utente Luisa Cazzaniga. Dal momento che il nome di accesso litwareinc\\pilar è stato incluso come parametro, la finestra di dialogo Richiesta credenziali di Windows PowerShell richiede all'amministratore solo di immettere la password per l'account di Luisa Cazzaniga. L'oggetto credenziali risultante viene quindi archiviato in una variabile denominata $cred1.

Il secondo comando controlla quindi se questo utente può accedere al pool atl-cs-001.litwareinc.com e inviare il messaggio istantaneo XMPP. Per eseguire questa attività, viene chiamato il cmdlet **Test-CsXmppIm** insieme a quattro parametri: TargetFqdn (nome di dominio completo del pool di registrazione), Receiver (indirizzo SIP dell'utente a cui il messaggio è indirizzato), UserCredential (oggetto Windows PowerShell contenente le credenziali dell'utente Luisa Cazzaniga) e UserSipAddress (indirizzo SIP corrispondente alle credenziali utente fornite).

    $credential = Get-Credential "litwareinc\kenmyer"
    
    Test-CsXmppIM -TargetFqdn "atl-cs-001.litwareinc.com" -Receiver "adelany@contoso.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $credential

## Descrizione dettagliata

Extensible Messaging and Presence Protocol (XMPP) è un protocollo di comunicazioni standard (basato su XML) utilizzato per l'invio di messaggi su Internet. XMPP è stato denominato in origine Jabber ed è supportato da numerose applicazioni di messaggistica e comunicazioni Internet, tra cui Google Talk e Facebook Chat. Il cmdlet **Test-CsXmppIM** verifica la capacità di un utente di scambiare messaggi istantanei con un utente su una rete XMPP. Affinché questo test abbia esito positivo, è necessario disporre di un indirizzo SIP valido per l'utente XMPP e appartenente a una rete configurata come partner XMPP consentito.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsXmppIM"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsXmppIM** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Receiver</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP dell'utente a cui è indirizzato il messaggio di prova.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Nome di dominio completo del pool da testare.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PSCredential</p></td>
<td><p>Oggetto credenziali utente per l'account utente da testare. Il valore passato a UserCredential deve essere un riferimento all'oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata $x:$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario fornire la password dell'utente quando si esegue questo comando.</p>
<p>Questo parametro non è richiesto se si sta eseguendo il test utilizzando le impostazioni di configurazione di monitoraggio dello stato.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Oggetto credenziali utente per l'account da testare. Il valore passato a UserCredential deve essere un riferimento all'oggetto ottenuto utilizzando il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e archivia tale oggetto in una variabile denominata</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario fornire la password dell'utente quando si esegue questo comando. Questo parametro non è richiesto se si sta eseguendo il test con le impostazioni di configurazione di monitoraggio dello stato per il pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato risultante dall'esecuzione del cmdlet verrà archiviato nella variabile specificata. Questa variabile include una coppia di metodi, ToHTML e ToXML, da utilizzare per salvare l'output su un file HTML o XML.</p>
<p>Per archiviare l'output in una variabile del logger denominata $TestOutput utilizzare la sintassi seguente:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Nota: non anteporre un carattere $ quando si specifica il nome della variabile.</p>
<p>Per salvare le informazioni archiviate nella variabile del logger su un file HTML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>Per salvare le informazioni archiviate nella variabile del logger su un file XML, utilizzare un comando simile al seguente:</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Quando presente, l'output dettagliato risultante derivante dall'esecuzione del cmdlet verrà archiviato nella variabile specificata. Ad esempio, per archiviare l'output in una variabile denominata $TestOutput utilizzare la sintassi seguente</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è richiesto se la funzione di registrazione utilizza la porta predefinita 5061</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Indirizzo SIP per l'account utente da testare, ad esempio:</p>
<p>-UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>Il parametro UserSipAddress deve fare riferimento allo stesso account utente di UserCredential. Questo parametro non è richiesto se si sta eseguendo il test con le impostazioni di configurazione di monitoraggio dello stato per il pool.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsXmppIM** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsXmppIM** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Set-CsXmppGatewayConfiguration](set-csxmppgatewayconfiguration.md)

