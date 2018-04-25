---
title: Test-CsVoiceRoute
TOCTitle: Test-CsVoiceRoute
ms:assetid: 39d5012d-7beb-41c6-ac94-51011da04872
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425873(v=OCS.15)
ms:contentKeyID: 49300237
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica un numero di telefono rispetto a un formato numero di route vocale e restituisce un valore booleano (true/false) che indica se il numero fornito corrisponde al formato numero della route. Il formato numero è solo una delle proprietà utilizzate dalle route vocali per comunicare a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale a numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsVoiceRoute -Route <Route> -TargetNumber <PhoneNumber> [-Force <SwitchParameter>]

## Esempi

## ESEMPIO 1

Questo comando determina se un dato numero corrisponde al formato di una specifica route. Innanzitutto viene utilizzato il cmdlet **Get-CsVoiceRoute** per recuperare il testroute della route vocale. Quella route viene utilizzata come valore per il parametro Route del cmdlet **Test-CsVoiceRoute**. Viene anche incluso il numero da testare nel parametro TargetNumber. L'output è un valore booleano che indica se il numero corrisponde al formato di quella route.

    $vr = Get-CsVoiceRoute -Identity testroute
    Test-CsVoiceRoute -TargetNumber "+14255551212" -Route $vr

## ESEMPIO 2

Nell'esempio 2 viene eseguita la stessa azione dell'esempio 1. In questo esempio l'azione viene tuttavia compiuta con un singolo comando. Viene innanzitutto chiamato il cmdlet **Get-CsVoiceRoute** per recuperare la route vocale con identità testroute. Quella route vocale viene quindi inviata tramite pipe al cmdlet **Test-CsVoiceRoute** e testata rispetto al numero specificato nel parametro TargetNumber. Si noti che non è necessario specificare il parametro Route perché la route è stata inviata al cmdlet tramite pipe.

    Get-CsVoiceRoute -Identity testroute | Test-CsVoiceRoute -TargetNumber "+14255551212"

## ESEMPIO 3

In questo esempio viene recuperata una raccolta di tutte le route vocali definite in una distribuzione di Lync Server e viene verificato il formato numero di ogni route rispetto al valore TargetNumber specificato nel cmdlet **Test-CsVoiceRoute**. L'output può essere un valore True o False per ogni route verificata.

    Get-CsVoiceRoute | Test-CsVoiceRoute -TargetNumber "+14255551212"

## ESEMPIO 4

Questo esempio è simile all'Esempio 3 in cui si recuperano i risultati di un test di route vocale eseguito su più route. Tuttavia, l'output dell'Esempio 3 sarà un semplice elenco di valori True/False, privi di una chiara indicazione a quale route si riferisce il test. Questo esempio risolve il problema. Esistono altre azioni che possono essere intraprese per abbellire l'output ma questo breve esempio, se non altro, raggiunge lo scopo.

Viene innanzitutto chiamato il cmdlet **Get-CsVoiceRoute** per recuperare tutte le route vocali e assegnare la raccolta alla variabile $z. Nella riga successiva si avvia un ciclo Foreach. Questo ciclo prende ogni membro della raccolta uno alla volta e lo assegna alla variabile $x. Tale variabile, che include un riferimento a una singola route vocale, viene utilizzata innanzitutto per visualizzare l'identità di quella route: $x.Identity. La parte successiva del comando è una chiamata al cmdlet **Test-CsVoiceRoute**, dove la route $x viene testata rispetto al numero di destinazione. L'output finale sarà un elenco (non formattato perfettamente) di identità di route vocali seguite da un indicatore true/false che segnala se il numero di destinazione corrisponde o meno al formato numero della route con quella identità.

    $z = Get-CsVoiceRoute
    foreach ($x in $z){$x.Identity; Test-CsVoiceRoute -TargetNumber "+14255551212" -Route $x}

## Descrizione dettagliata

Una route vocale include un'espressione regolare che identifica quali numeri di telefono saranno instradati attraverso una route vocale specifica: i numeri di telefono corrispondenti all'espressione regolare saranno instradati attraverso questa route. Questo cmdlet verifica se un determinato numero di telefono verrà instradato su una route vocale specifica in base al formato del numero della route (la proprietà NumberPattern). Questo cmdlet può essere utilizzato per la risoluzione dei problemi di routing o semplicemente per testare numeri di telefono rispetto a route specifiche per essere certi di ottenere i risultati desiderati.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Test-CsVoiceRoute** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceRoute"}

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
<td><p><em>Route</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route</p></td>
<td><p>Un oggetto contenente un riferimento alla route vocale su cui si desidera testare il numero specificato nel parametro DialedNumber. Per recuperare un oggetto route vocale, utilizzare il cmdlet <strong>Get-CsVoiceRoute</strong>.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route</p></td>
</tr>
<tr class="even">
<td><p><em>TargetNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>Il numero di telefono su cui si desidera testare la route vocale specificata nel parametro Route. Questo numero deve essere nel formato E.164 (come +14255551212).</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route. Accetta l'input tramite pipeline di un oggetto route vocale.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.VoiceRouteTestResult.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

