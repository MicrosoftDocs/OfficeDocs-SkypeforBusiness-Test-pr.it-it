---
title: Grant-CsClientPolicy
TOCTitle: Grant-CsClientPolicy
ms:assetid: c09d743d-cf2c-4622-b00c-cc815852e4a6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412942(v=OCS.15)
ms:contentKeyID: 49301872
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsClientPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio client a un utente o a un gruppo di utenti. I criteri client consentono di stabilire, tra l'altro, le funzionalità di Lync Server disponibili per gli utenti. È ad esempio possibile decidere di consentire solo ad alcuni utenti di trasferire i file, negando questo diritto ad altri utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsClientPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, i criteri client SalesPolicy vengono assegnati all'utente con identità Davide Garghentini.

    Grant-CsClientPolicy -Identity "Ken Myer" -PolicyName SalesPolicy

## ESEMPIO 2

Nell'esempio 2, a tutti gli utenti che appartengono al reparto Sales vengono assegnati i criteri client SalesPolicy. Nel comando vengono utilizzati innanzitutto il cmdlet **Get-CsUser** e il parametro LdapFilter per restituire una raccolta di tutti gli utenti membri del reparto Sales. La raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsClientPolicy**, che assegna i criteri SalesPolicy a ogni utente nella raccolta.

    Get-CsUser -LDAPFilter "Department=Sales" | Grant-CsClientPolicy -PolicyName SalesPolicy

## ESEMPIO 3

Nell'esempio 3, i criteri client RedmondAccountingPolicy vengono assegnati a tutti gli utenti che soddisfano due requisiti: 1) l'utente deve avere la qualifica di Accountant e 2) lavorare nella città di Redmond. A tale scopo, nel comando vengono utilizzati innanzitutto il cmdlet **Get-CsUser** e il parametro LdapFilter per restituire una raccolta di tutti gli utenti che lavorano a Redmond e che sono in possesso della qualifica di Accountant. Il valore di filtro "(&(Title=Accountant)(l=Redmond))" limita i dati restituiti agli utenti con la qualifica di Accountant (Title=Accountant) e (&) che lavorano a Redmond (l=Redmond). La elle minuscola "l" rappresenta la località dell'utente.

La raccolta che si ottiene viene quindi inviata tramite pipe al cmdlet **Grant-CsClientPolicy**, che assegna il criterio RedmondAccountingPolicy a ogni utente nella raccolta.

    Get-CsUser -LDAPFilter "(&(Title=Accountant)(l=Redmond))" | Grant-CsClientPolicy -PolicyName RedmondAccountingPolicy

## ESEMPIO 4

Nell'esempio 4 i criteri AccountingPolicy vengono assegnati a tutti gli utenti che soddisfano uno di questi due requisiti: o l'utente ha la qualifica di Accountant o di Senior Accountant. Per eseguire questa attività, vengono utilizzati il cmdlet **Get-CsUser** e il parametro LdapFilter per restituire una raccolta di utenti con la qualifica di Accountant o di Senior Accountant. Il valore di filtro "(|(Title=Accountant)(Title=Senior Accountant))" limita i dati restituiti agli utenti con la qualifica di Accountant (Title=Accountant) o (|) di Senior Accountant (Title=Senior Accountant). La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Grant-CsClientPolicy**, che assegna il criterio client AccountingPolicy a ogni utente nella raccolta.

    Get-CsUser -LdapFilter "(|(Title=Accountant)(Title=Senior Accountant))" | Grant-CsClientPolicy -PolicyName AccountingPolicy

## ESEMPIO 5

Nell'esempio 5 a tutti gli utenti con account nel pool di registrazione atl-cs-001.litwareinc.com viene assegnato il criterio client AtlantaBranchPolicy. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsUser** per restituire gli account utente appropriati. Il parametro Filter e il valore di filtro {RegistrarPool -eq "atl-cs-001.litwareinc.com"} assicurano che vengano restituiti solo gli account utente ospitati nel pool di registrazione atl-cs-001.litwareinc.com. La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsClientPolicy**, che assegna a ogni utente il criterio client AtlantaBranchPolicy.

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsClientPolicy -PolicyName AtlantaBranchPolicy

## Descrizione dettagliata

In Lync Server i criteri client sostituiscono le impostazioni di Criteri di gruppo in uso nelle versioni precedenti del prodotto. In Microsoft Office Communicator 2007 e Microsoft Office Communicator 2007 R2 la funzionalità Criteri di gruppo viene utilizzata per definire le azioni consentite agli utenti in Communicator e in altri client. Alcune impostazioni di Criteri di gruppo ad esempio stabiliscono se gli utenti possono o meno salvare una trascrizione delle rispettive sessioni di messaggistica istantanea, se possono o meno inserire emoticon o testo formattato nei messaggi istantanei e se nelle informazioni sulla presenza vengono incorporate le informazioni di Microsoft Outlook.

Nonostante l'utilità di Criteri di gruppo, questa tecnologia presenta tuttavia alcuni limiti se applicata a Lync Server. Da un lato la funzionalità Criteri di gruppo è progettata per essere applicata in base al dominio o all'unità organizzativa e rende pertanto difficile assegnare i criteri a un gruppo di utenti più selezionato, ad esempio a tutti gli utenti che lavorano in un reparto specifico o a tutti quelli in possesso di una qualifica particolare. Dall'altro la funzionalità Criteri di gruppo viene applicata solo agli utenti che accedono al dominio e che effettuano l'accesso tramite un computer. Non viene applicata invece agli utenti che accedono a Lync Server su Internet o che accedono al sistema utilizzando un telefono cellulare. Ciò significa che lo stesso utente può avere esperienze diverse a seconda del dispositivo e della postazione utilizzati per l'accesso.

Per risolvere queste incongruenze, in Lync Server vengono utilizzati i criteri client anziché Criteri di gruppo. I criteri client vengono applicati ogni volta che un utente accede al sistema, indipendentemente dalla postazione e dal tipo di dispositivo utilizzati per l'accesso. I criteri client, analogamente ad altri criteri di Lync Server, possono inoltre essere facilmente assegnati a gruppi selezionati di utenti. È anche possibile creare criteri personalizzati da assegnare a un singolo utente.

I criteri client possono essere configurati in ambito globale, di sito e per utente. Per assegnare criteri per utente, è necessario utilizzare il cmdlet **Grant-CsClientPolicy**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Grant-CsClientPolicy** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsClientPolicy"}

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
<td><p>Indica l'identità dell'account utente a cui assegnare i criteri. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini), 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). È possibile fare riferimento alle identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>Inoltre, è possibile utilizzare il carattere jolly asterisco (*) quando si utilizza Display Name come valore Identity dell'utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il &quot;Nome&quot; del criterio da assegnare. PolicyName corrisponde all'identità del criterio meno l'ambito del criterio (il prefisso &quot;tag:&quot;). Un criterio con valore Identity tag:Redmond ad esempio dispone di una proprietà PolicyName uguale a Redmond, mentre un criterio con valore Identity tag:RedmondConferencingPolicy dispone di una proprietà PolicyName uguale a RedmondConferencingPolicy.</p>
<p>Se si imposta PolicyName su un valore Null, il comando annullerà le assegnazioni dei criteri per utente assegnati all'utente. Ad esempio:</p>
<p>Grant-CsClientPolicy –Identity &quot;Davide Garghentini&quot; –PolicyName $Null</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare un controller di dominio a cui connettersi durante l'assegnazione dei criteri. Se il parametro non è incluso, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, il cmdlet passa l'oggetto (o gli oggetti) utente attraverso la pipeline di Windows PowerShell. Per impostazione predefinita, il cmdlet <strong>Grant-CsClientPolicy</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Grant-CsClientPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsClientPolicy** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituirà le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientPolicy](get-csclientpolicy.md)  
[New-CsClientPolicy](new-csclientpolicy.md)  
[Remove-CsClientPolicy](remove-csclientpolicy.md)  
[Set-CsClientPolicy](set-csclientpolicy.md)

