---
title: Set-CsClientPin
TOCTitle: Set-CsClientPin
ms:assetid: d587c69c-9cf7-4cd8-81d4-26869524654b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398929(v=OCS.15)
ms:contentKeyID: 49302116
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientPin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un nuovo PIN all'utente specificato. Questo cmdlet è stato introdotto in Lync Server 2010. Si noti che la versione Lync Server 2013 di questo cmdlet può assegnare numeri PIN solo agli utenti presenti in Lync Server 2013. Per assegnare numeri PIN agli utenti presenti in Lync Server 2010, utilizzare invece la versione Lync Server 2010 di Set-CsClientPin.

## Sintassi

    Set-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Pin <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 all'utente litwareinc\\kenmyer viene assegnato un nuovo codice PIN generato automaticamente. Per assegnare un codice PIN generato automaticamente, è sufficiente omettere il parametro Pin quando si chiama il cmdlet **Set-CsClientPin**. Al termine dell'esecuzione del comando, il nuovo codice PIN assegnato a Ken Myer verrà visualizzato e tali informazioni potranno quindi essere inoltrate all'utente.

    Set-CsClientPin -Identity "litwareinc\kenmyer"

## ESEMPIO 2

Il comando nell'esempio 2 assegna il PIN 18723834 all'utente litwareinc\\davidegarghentini. Per assegnare un codice PIN specifico, è possibile utilizzare il parametro Pin seguito dal codice da assegnare.

    Set-CsClientPin -Identity "litwareinc\kenmyer" -Pin 18723834

## ESEMPIO 3

Nell'esempio 3 viene mostrato come assegnare automaticamente nuovi codici PIN a tutti gli utenti di una determinata unità organizzativa di Active Directory. A tale scopo, viene utilizzato il cmdlet **Get-CsUser** con il parametro OU per restituire una raccolta di tutti gli utenti con account nell'unità organizzativa Finance. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsClientPin**, che genera un nuovo codice PIN per ogni utente presente nella raccolta.

    Get-CsUser -OU "OU=Finance,DC=litwareinc,DC=com" | Set-CsClientPin

## ESEMPIO 4

Il comando riportato nell'esempio 4 assegna un nuovo codice PIN a tutti gli utenti che attualmente ne sono privi. A tale scopo, viene utilizzato il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti che sono stati abilitati per Lync Server. Questa raccolta viene quindi inviata tramite pipe ai cmdlet **Get-CsClientPin** e **Where-Object**. Questi due cmdlet consentono di selezionare solo gli utenti la cui proprietà IsPinSet è uguale a False. La raccolta risultante, che contiene solo gli utenti che non hanno un codice PIN, viene quindi inviata tramite pipe al cmdlet **Set-CsClientPin**, che genera automaticamente un codice PIN per ciascun utente presente nella raccolta.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $False} | Set-CsClientPin

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite telefono. Per accedere al sistema o partecipare a una conferenza, l'utente in genere deve immettere un nome utente o una password. L'immissione del nome utente e della password può tuttavia costituire un problema se il telefono in uso non dispone di una tastiera alfanumerica. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono quindi accedere al sistema o partecipare a una conferenza immettendo il codice PIN anziché il nome utente e la password.

Quando gli utenti sono abilitati per Lync Server, non viene loro assegnato un codice PIN. Questo significa che, per impostazione predefinita, gli utenti non possono accedere al sistema utilizzando l'autenticazione tramite PIN. Gli utenti possono ottenere un codice PIN dalla pagina Web Conferenza telefonica con accesso esterno. In alternativa, gli amministratori possono assegnare a ciascun utente un codice PIN utilizzando il cmdlet **Set-CsClientPin**. Con il cmdlet **Set-CsClientPin** è possibile assegnare a un utente un codice PIN specifico o lasciare che sia Lync Server a generarne uno automaticamente. Per generare automaticamente un codice PIN, è sufficiente omettere il parametro PIN quando si chiama il cmdlet **Set-CsClientPin**. In tal modo, verrà generato un nuovo codice PIN che verrà visualizzato insieme all'identità dell'utente al termine dell'esecuzione del comando.

I codici PIN assegnati esplicitamente devono soddisfare le condizioni specificate nel criterio di autenticazione tramite PIN che si applica all'utente in questione. Il codice PIN ad esempio deve contenere almeno tante cifre quante ne sono previste dalla proprietà MinPasswordLength. I codici PIN inoltre possono contenere solo caratteri numerici. Le lettere e qualsiasi altro carattere non numerico non sono consentiti.

Quando si imposta un codice PIN client utilizzando il cmdlet **Set-CsClientPin**, il conteggio della cronologia PIN non viene applicato. Si supponga ad esempio che un utente disponga del codice PIN 12345 e che il criterio PIN client impedisca il riutilizzo immediato dello stesso codice. Se l'utente tenta di rinnovare il proprio codice PIN client tramite la pagina Web Conferenza telefonica con accesso esterno, qualsiasi tentativo di riutilizzare lo stesso codice (12345) verrà rifiutato. Utilizzando il cmdlet **Set-CsClientPin**, un amministratore può tuttavia assegnare il codice PIN 12345 allo stesso utente. Ciò è dovuto al fatto che il cmdlet **Set-CsClientPin** non è vincolato dal conteggio della cronologia del criterio PIN.

Per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Questo significa che non sarà possibile eseguire il cmdlet **Set-CsClientPin** da un'istanza remota di Windows PowerShell, dal momento che il comando non sarà in grado di attraversare il firewall e accedere al database di SQL Server Express. Sarà comunque possibile eseguire il cmdlet localmente sul server Standard Edition. Per poter eseguire il cmdlet **Set-CsClientPin** in remoto su un server Standard Edition, sarà necessario abilitare manualmente le eccezioni del firewall per SQL Server Express.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsClientPin** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientPin"}

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
<td><p>Identità dell'account utente per cui deve essere impostato il codice PIN. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini), 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). È possibile fare riferimento alle identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name come parametro Identity dell'utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Pin</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Codice PIN facoltativo da assegnare all'utente. Se non si include il parametro PIN, Lync Server genererà in modo casuale un codice PIN e lo assegnerà all'utente in questione. Il codice PIN deve rispettare le impostazioni relative alla lunghezza minima e ai modelli comuni specificate nel criterio PIN client assegnato all'utente.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Set-CsClientPin** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Il cmdlet **Set-CsClientPin** non restituisce un valore o un oggetto. Il cmdlet configura invece istanze dell'oggetto Microsoft.Rtc.Management.UserPinService.PinInfoDetails.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Lock-CsClientPin](lock-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

