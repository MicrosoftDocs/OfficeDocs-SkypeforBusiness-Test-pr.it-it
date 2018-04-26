---
title: Get-CsClientPinInfo
TOCTitle: Get-CsClientPinInfo
ms:assetid: 45feaa2c-f284-4374-a8a6-d3ff3c87d660
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425947(v=OCS.15)
ms:contentKeyID: 49300389
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientPinInfo

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera informazioni sul PIN assegnato a un utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsClientPinInfo -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni sul PIN di tutti gli utenti abilitati per Lync Server. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** per restituire tutti gli utenti abilitati per Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Get-CsClientPinInfo**, che visualizza le informazioni sul PIN di ogni utente della raccolta.

    Get-CsUser | Get-CsClientPinInfo

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il cmdlet **Get-CsClientPinInfo** per visualizzare le informazioni sul PIN di un singolo utente, ovvero l'utente con identità litwareinc\\kenmyer.

    Get-CsClientPinInfo -Identity "litwareinc\kenmyer"

## ESEMPIO 3

Nell'esempio 3 vengono restituite informazioni sul PIN per tutti gli utenti con un account nell'unità organizzativa Finance. A tale scopo, vengono utilizzati il cmdlet **Get-CsUser** e il parametro OU per restituire una raccolta di tutti gli utenti nell'unità organizzativa Finance. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Get-CsClientPinInfo**, che visualizza informazioni sul PIN per ogni utente della raccolta.

    Get-CsUser -OU "OU=Finance,DC=litwareinc,DC=com" | Get-CsClientPinInfo

## ESEMPIO 4

Il comando riportato nell'esempio 4 visualizza informazioni sul PIN per tutti i responsabili dell'organizzazione. Per recuperare una raccolta di tutti i responsabili, il comando utilizza il cmdlet **Get-CsUser** e il parametro LdapFilter. Il valore di filtro "Title=Manager" restituisce solo i dati relativi agli utenti la cui qualifica è "Manager". Viene quindi utilizzato il cmdlet **Get-CsClientPinInfo** per visualizzare le informazioni sul PIN di ognuno di questi utenti.

    Get-CsUser -LdapFilter "Title=Manager" | Get-CsClientPinInfo

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite un telefono. L'accesso al sistema o la partecipazione a una conferenza in genere richiede l'immissione del nome utente e della password. Tale operazione può tuttavia rappresentare un problema se si utilizza un telefono privo di tastierino alfanumerico. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono accedere al sistema o partecipare a una conferenza immettendo il PIN anziché il nome utente e la password.

Gli amministratori possono recuperare le impostazioni PIN di un utente o di un gruppo di utenti eseguendo il cmdlet **Get-CsClientPinInfo**. Si noti che un amministratore non può recuperare il PIN assegnato a un utente. Se un utente dimentica il proprio PIN, non sarà più in grado di usare l'autenticazione tramite PIN per accedere al sistema fino a quando un amministratore non gli assegnerà un nuovo PIN o fino a quando l'utente non otterrà un nuovo PIN dalla pagina Web relativa alla conferenza telefonica con accesso esterno.

Per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Non sarà possibile pertanto eseguire il cmdlet **Get-CsClientPinInfo** da un'istanza remota di Windows PowerShell perché il comando non è in grado di attraversare il firewall e accedere al database di SQL Server Express. È comunque possibile eseguire il cmdlet localmente nel server Standard Edition. Per eseguire il cmdlet **Get-CsClientPinInfo** in remoto nel server Standard Edition, è necessario abilitare manualmente le eccezioni del firewall per SQL Server Express.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsClientPinInfo** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientPinInfo"}

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
<td><p>Indica l'identità dell'account utente il cui PIN deve essere bloccato. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). È anche possibile fare riferimento a un account utente utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con il valore di stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Get-CsClientPinInfo** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Il cmdlet **Get-CsClientPinInfo** restituisce una o più istanze dell'oggetto Microsoft.Rtc.Management.UserPinService.PinInfoDetails.

## Vedere anche

#### Ulteriori risorse

[Get-CsPinPolicy](get-cspinpolicy.md)  
[Lock-CsClientPin](lock-csclientpin.md)  
[Set-CsClientPin](set-csclientpin.md)  
[Unlock-CsClientPin](unlock-csclientpin.md)

