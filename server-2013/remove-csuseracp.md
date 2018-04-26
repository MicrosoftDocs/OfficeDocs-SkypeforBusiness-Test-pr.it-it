---
title: Remove-CsUserAcp
TOCTitle: Remove-CsUserAcp
ms:assetid: dec450bb-d523-468d-aee4-07fdc3d567c4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398982(v=OCS.15)
ms:contentKeyID: 49302213
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserAcp

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove uno o più provider di servizi di audioconferenza assegnati a un utente oppure a un gruppo di utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsUserAcp -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Name <String>] [-ParticipantPasscode <String>] [-PassThru <SwitchParameter>] [-TollNumber <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 rimuove tutti i provider di servizi di audioconferenza che sono stati assegnati all'utente Davide Garghentini.

    Remove-CsUserAcp -Identity "Ken Myer"

## ESEMPIO 2

Nell'esempio 2 viene mostrato come rimuovere tutti i provider di servizi di audioconferenza che sono stati assegnati a tutti gli utenti abilitati per Lync Server. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsUser** per recuperare una raccolta di tutti gli utenti che sono stati abilitati per Lync Server. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsUserAcp**, che rimuove tutti i provider di servizi di audioconferenza che sono stati assegnati ai singoli utenti presenti nella raccolta.

    Get-CsUser | Remove-CsUserAcp

## ESEMPIO 3

Nell'esempio 3 tutti i provider di servizi di audioconferenza che hanno il nome "Fabrikam ACP" vengono rimossi dall'account utente di Davide Garghentini.

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Fabrikam ACP"

## ESEMPIO 4

Nell'esempio 4 viene rimosso il provider di servizi di audioconferenza con numero a pagamento "14255551298" da tutti gli account utente a cui è stato assegnato un provider di servizi di audioconferenza. Per eseguire questa attività, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsUserAcp** per restituire informazioni su tutti i provider di servizi di audioconferenza assegnati a tutti gli utenti. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che seleziona solo gli account in cui la proprietà AcpInfo include (-match) il numero di telefono "14255551298". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsUserAcp**, che rimuove il corrispondente provider di servizi di audioconferenza da ciascun account presente nella raccolta filtrata.

    Get-CsUserAcp | Where-Object {$_.AcpInfo -match "14255551298"} | Remove-CsUserAcp

## Descrizione dettagliata

Un provider di servizi di audioconferenza è una società terza che fornisce servizi di conferenza alle organizzazioni. Tra l'altro, i provider di servizi di audioconferenza consentono agli utenti in trasferta non connessi alla rete aziendale o a Internet di accedere ai contenuti audio di una conferenza o di una riunione. Tali provider offrono spesso servizi di qualità elevata quali traduzione immediata, trascrizione e assistenza diretta di un operatore durante la conferenza.

Lync Server non consente l'integrazione completa con i provider di servizi di audioconferenza. I cmdlet **CsUserAcp** consentono agli amministratori di impostare un numero telefonico e un passcode, nonché di configurare altre informazioni utilizzabili per l'integrazione dei provider di servizi di audioconferenza ogni volta che un utente pianifica una riunione. Poiché tuttavia tali cmdlet non sono specifici per la versione locale di Lync Server ma devono essere utilizzati principalmente con Lync Online, non verrà garantita ulteriore integrazione con i provider di servizi di audioconferenza oltre all'assegnazione dei valori delle proprietà.

Un qualsiasi provider di servizi di audioconferenza assegnato a un utente può essere successivamente rimosso utilizzando il cmdlet **Remove-CsUserAcp**. Chiamando il cmdlet **Remove-CsUserAcp** senza alcun parametro (ad eccezione del parametro Identity che indica l'account utente da modificare), si rimuovono tutti i provider di servizi di audioconferenza assegnati a un utente. In alternativa, è possibile utilizzare i parametri facoltativi inclusi con il cmdlet **Remove-CsUserAcp** per rimuovere determinati provider da un account utente. Ad esempio, questo comando trova l'account utente Davide Garghentini e rimuove tutti i provider di servizi di audioconferenza il cui nome è "Fabrikam ACP":

Remove-CsUserAcp –Identity "Davide Garghentini" –Name "Fabrikam ACP"

Per una rimozione più mirata dei provider di servizi di audioconferenza, è sufficiente includere ulteriori parametri. Ad esempio, il seguente comando rimuove tutti i provider di servizi di audioconferenza il cui nome è "Fabrikam ACP" e per i quali il valore TollNumber è uguale a "14255551298":

Remove-CsUserAcp –Identity "Davide Garghentini" –Name "Fabrikam ACP" –TollNumber "14255551298"

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsUserAcp** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserAcp"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente da cui rimuovere il provider di servizi di audioconferenza. l'identità di un utente può essere specificata con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nella forma dominio\accesso (ad esempio litwareinc\davidegarghentini), 4) il nome visualizzato Servizi di dominio Active Directory dell'utente (ad esempio Davide Garghentini). È possibile fare riferimento alle identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il valore Identity &quot;* Smith&quot; restituisce tutti gli utenti con un nome visualizzato che termina con il valore stringa &quot; Smith&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome del provider di servizi di audioconferenza. Ad esempio: -Name &quot;Fabrikam Conference Services&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipantPasscode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Passcode necessario quando ci si connette a una conferenza mediante il provider di servizi di audioconferenza. Ad esempio: -PassCode &quot;0712&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite la pipeline un oggetto utente che rappresenta l'utente per cui si rimuove il provider di servizi di audioconferenza. Per impostazione predefinita, il cmdlet <strong>Remove-CsUserAcp</strong> non passa oggetti tramite la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>TollNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero telefonico a pagamento utilizzato per le audioconferenze. Ad esempio: -TollNumber &quot;14255551298&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa o oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Remove-CsUserAcp** accetta un valore stringa da pipeline che rappresenta l'identità di un account utente abilitato per Lync Server. Il cmdlet accetta inoltre istanze da pipeline dell'oggetto utente di Active Directory.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserAcp](get-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

