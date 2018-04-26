---
title: Test-CsPhoneBootstrap
TOCTitle: Test-CsPhoneBootstrap
ms:assetid: b132446b-f264-405e-8e3a-971ab1c37694
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412852(v=OCS.15)
ms:contentKeyID: 49301692
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsPhoneBootstrap

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che un utente possa accedere a Lync Server utilizzando un dispositivo compatibile con Lync Phone Edition. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsPhoneBootstrap -PhoneOrExt <String> -PIN <String> [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] [-TargetUri <String>] [-UserSipAddress <String>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 verifica che l'utente con il numero di telefono e il PIN specificati possa connettersi a Lync Server utilizzando un dispositivo compatibile con Lync Phone Edition. Per eseguire la verifica, è necessario fornire il numero di telefono (+14255551219) e il PIN (0712) dell'utente.

    Test-CsPhoneBootstrap -PhoneOrExt "+14255551219" -Pin "0712"

## ESEMPIO 2

Nell'esempio 2 viene verificato se l'utente con il numero di telefono e il PIN specificati è in grado di connettersi a Lync Server utilizzando un dispositivo compatibile con Lync Phone Edition. In questo esempio il parametro UserSipAddress viene incluso come verifica aggiuntiva. La verifica avrà esito negativo se l'utente con l'indirizzo SIP non corrisponde all'utente con il numero di telefono e il PIN specificati.

    Test-CsPhoneBootstrap -PhoneOrExt "+14255551219" -Pin "0712" -UserSipAddress "sip:kenmyer@litwareinc.com"

## Descrizione dettagliata

Per poter effettuare la connessione a Lync Server, i dispositivi compatibili con Lync Phone Edition devono utilizzare il protocollo DHCP (Dynamic Host Configuration Protocol) per recuperare l'indirizzo di un pool di registrazione di Lync Server. Questi dispositivi inoltre devono fornire un numero di telefono e un PIN associato validi per poter essere autenticati dal sistema. Questo processo è noto come "bootstrap" o avvio automatico. Il cmdlet **Test-CsPhoneBootstrap** consente agli amministratori di verificare che un determinato utente che utilizza il numero di telefono e il PIN che gli sono stati assegnati sia in grado di accedere al sistema da un dispositivo compatibile con Lync Phone Edition. Per eseguire la verifica non è in realtà necessario alcun dispositivo.

Per consentire al cmdlet **Test-CsPhoneBootstrap** di effettuare il controllo, il pool di registrazione che ospita l'account utente su cui viene eseguito il test deve risultare individuabile mediante protocollo DHCP. Per stabilire se è possibile individuare in questo modo un pool di registrazione, utilizzare il cmdlet [Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md) e controllare il valore della proprietà EnableDHCPServer. Se la proprietà è impostata su False, sarà necessario utilizzare il cmdlet [Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md) per impostare il valore su True in modo che il pool di registrazione risulti individuabile mediante protocollo DHCP. Questa operazione può essere eseguita anche utilizzando un server DHCP versione Enterprise e configurando le opzioni specifiche di Lync Server.

Utenti autorizzati a eseguire il cmdlet: per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets \\endash match "Test-CsPhoneBootstrap"}

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
<td><p><em>PhoneOrExt</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono o interno dell'account utente di cui viene eseguito il test. Ad esempio: -PhoneOrExt &quot;+14255551219&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PIN</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Codice PIN dell'account utente su cui viene eseguito il test.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando presente, l'output dettagliato relativo all'esecuzione del cmdlet verrà archiviato nella variabile specificata. Per archiviare, ad esempio, l'output in una variabile denominata $TestOutput, utilizzare la sintassi seguente:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Non anteporre un carattere $ quando si specifica il nome della variabile.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Porta SIP utilizzata dal servizio di registrazione. Questo parametro non è necessario se il servizio di registrazione utilizza la porta predefinita 5061.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione che ospita l'account utente su cui eseguire il test. Se non viene specificato, verrà utilizzata l'individuazione tramite DHCP per trovare il pool di registrazione.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio di provisioning del certificato. Se questo parametro non viene incluso, verrà utilizzata l'individuazione tramite DHCP per trovare l'URI di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserSipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP dell'account utente utilizzato nella verifica, ad esempio: -UserSipAddress &quot;sip:kenmyer@litwareinc.com&quot;. Il parametro UserSipAddress deve fare riferimento al numero di telefono e al PIN specificati. La verifica avrà esito negativo se il numero di telefono e il PIN inclusi non appartengono all'utente specificato dal parametro UserSipAddress. Si noti che l'indirizzo SIP deve includere il prefisso &quot;sip:&quot;.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsPhoneBootstrap** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Test-CsPhoneBootstrap** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Test-CsRegistration](test-csregistration.md)

