---
title: Lock-CsClientPin
TOCTitle: Lock-CsClientPin
ms:assetid: 81a9895f-96e3-43c9-9dac-8129358e446a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398650(v=OCS.15)
ms:contentKeyID: 49301157
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lock-CsClientPin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente a un amministratore di impedire a un utente di utilizzare l'autenticazione basata su PIN. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Lock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Lock-CsClientPin** per bloccare il PIN appartenente all'utente kenmyer@litwareinc.com.

    Lock-CsClientPin -Identity "kenmyer@litwareinc.com"

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il cmdlet **Lock-CsClientPin** per bloccare i PIN per tutti gli utenti a cui è attualmente assegnato un PIN. A tale scopo, viene utilizzato il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti abilitati per Lync Server. Tale raccolta viene inviata tramite pipe al cmdlet **Get-CsClientPinInfo**, utilizzato insieme al cmdlet **Where-Object** per restituire una raccolta degli utenti per cui la proprietà IsPinSet è uguale a True. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Lock-CsClientPin**, che blocca il PIN per ogni utente della raccolta.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsPinSet -eq $True} | Lock-CsClientPin

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il cmdlet **Lock-CsClientPin** per bloccare i PIN di tutti gli utenti con PIN scaduti. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti abilitati per Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Get-CsClientPinInfo**, utilizzato insieme al cmdlet **Where-Object** per restituire una raccolta solo degli utenti i cui PIN sono scaduti. Per determinare gli utenti con PIN scaduti, il cmdlet **Where-Object** ricerca gli account in cui la proprietà PinExpirationTime (che indica la data di scadenza del PIN) ha un valore antecedente alla data corrente. La data corrente viene recuperata mediante il cmdlet **Get-Date**. Se la data di scadenza (ad esempio 1° settembre 2010) è antecedente alla data corrente (ad esempio 2 settembre 2010), il PIN è scaduto. Viene infine utilizzato il cmdlet **Lock-CsClientPin** per bloccare tutti i PIN scaduti.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.PinExpirationTime -lt (Get-Date)} | Lock-CsClientPin

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite un telefono. L'accesso al sistema o la partecipazione a una conferenza in genere richiede l'immissione del nome utente e della password. Tale operazione può tuttavia rappresentare un problema se si utilizza un telefono privo di tastierino alfanumerico. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono accedere al sistema o partecipare a una conferenza immettendo il PIN anziché il nome utente e la password.

Come misura di sicurezza, Lync Server consente di bloccare il PIN di un utente. Quando un PIN è bloccato, l'utente non è più in grado di utilizzarlo per accedere al sistema o partecipare a una conferenza. L'utente potrà comunque accedere al sistema e partecipare alle conferenze utilizzando un'applicazione come Lync 2013 e specificando un nome utente e una password. Dopo il blocco di un PIN, l'unico modo per ripristinarlo, insieme ai privilegi di accesso dell'utente, consiste nel richiedere a un amministratore di sbloccare il PIN. Questa operazione può essere eseguita utilizzando il cmdlet **Unlock-CsClientPin**.

Il cmdlet **Lock-CsClientPin** consente agli amministratori di disabilitare temporaneamente la capacità di un utente di accedere al sistema utilizzando l'autenticazione PIN. I PIN possono anche essere bloccati dal sistema: se un utente non riesce ad accedere ripetutamente al sistema, il relativo PIN verrà automaticamente bloccato e anche in questo caso sarà necessario richiedere lo sblocco a un amministratore.

Per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Non sarà possibile pertanto eseguire il cmdlet **Lock-CsClientPin** da un'istanza remota di Windows PowerShell perché il comando non potrà attraversare il firewall e accedere al database di SQL Server Express. Sarà comunque possibile eseguire il cmdlet in locale nel server Standard Edition. Per eseguire il cmdlet **Lock-CsClientPin** in remoto, sarà necessario abilitare manualmente le eccezioni del firewall per SQL Server Express.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Lock-CsClientPin** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Lock-CsClientPin"}

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
<td><p>Identità dell'account utente per cui bloccare il PIN. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). Le identità utente possono essere referenziate anche utilizzando il nome distinto dell'utente in Active Directory.</p>
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
<td><p>Consente di ignorare la visualizzazione di messaggi di errore non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Lock-CsClientPin** accetta l'input da pipeline di valori stringa che rappresentano l'identità (Identity) di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Il cmdlet **Lock-CsClientPin** non restituisce alcun oggetto o valore. Configura invece una o più istanze dell'oggetto Microsoft.Rtc.Management.UserPinService.PinInfoDetails.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

