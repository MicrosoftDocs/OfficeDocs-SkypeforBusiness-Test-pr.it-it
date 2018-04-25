---
title: Test-CsAVEdgeConnectivity
TOCTitle: Test-CsAVEdgeConnectivity
ms:assetid: 9f3b2c70-9239-4085-a108-43e0b7a308b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205138(v=OCS.15)
ms:contentKeyID: 49301485
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAVEdgeConnectivity

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la connettività all'A/V Edge Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Test-CsAVEdgeConnectivity -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-UserSipAddress <String>] <COMMON PARAMETERS>

    Test-CsAVEdgeConnectivity -UserCredential <PSCredential> -UserSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsAVEdgeConnectivity [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 verifica che un utente test preconfigurato sia in grado di connettersi all'A/V Edge Server configurato per il pool atl-cs-001.litwareinc.com. Si noti che questo comando avrà esito negativo se non è stato definito almeno un utente test di monitoraggio dello stato per atl-cs-001.litwareinc.com.

    Test-CsAVEdgeConnectivity -TargetFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'esempio 2 il cmdlet **Test-CsAVEdgeConnectivity** verifica che l'utente con indirizzo SIP sip:kenmyer@litwareinc.com sia in grado di connettersi all'A/V Edge Server. A tale scopo, il primo comando dell'esempio utilizza il cmdlet Get-Credential per recuperare un oggetto credenziali di Windows PowerShell per l'utente litwareinc\\kenmyer. Si noti che è necessario specificare la password di questo account per ottenere questo oggetto. Dopo aver ottenuto l'oggetto credenziali, il secondo comando utilizza il cmdlet **Test-CsAVEdgeConnectivity** per verificare che l'utente sia in grado di connettersi all'A/V Edge Server.

    $cred = Get-Credential "litwareinc\kenmyer"
    
    Test-CsAVEdgeConnectivity -TargetFqdn "atl-cs-001.litwareinc.com" -UserSipAddress "sip:kenmyer@litwareinc.com" -UserCredential $cred

## Descrizione dettagliata

Il cmdlet **Test-CsAVEdgeConnectivity** verifica che un utente sia in grado di connettersi all'A/V Edge Server assegnato a un pool di registrazione.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsAVEdgeConnectivity"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Test-CsAVEdgeConnectivity** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo (FQDN) del pool da sottoporre a test.</p></td>
</tr>
<tr class="even">
<td><p><em>UserCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Oggetto credenziali utente dell'account da verificare. Il valore passato a UserCredential deve essere un riferimento all'oggetto ottenuto tramite il cmdlet <strong>Get-Credential</strong>. Ad esempio, questo codice restituisce un oggetto credenziali per l'utente litwareinc\kenmyer e lo archivia in una variabile denominata</p>
<p>$x: $x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>È necessario immettere la password utente quando si esegue questo comando. Questo parametro non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato del pool.</p></td>
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
<p>Non anteporre il carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è necessario se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP dell'account utente da sottoporre a test, ad esempio -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro UserSipAddress deve fare riferimento allo stesso account utente di UserCredential. Questo parametro non è necessario se si sta eseguendo il test nell'ambito delle impostazioni di configurazione per il monitoraggio dello stato del pool.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsAVEdgeConnectivity** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Test-CsAVEdgeConnectivity** restituisce istanze dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

