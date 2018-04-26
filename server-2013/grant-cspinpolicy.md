---
title: Grant-CsPinPolicy
TOCTitle: Grant-CsPinPolicy
ms:assetid: ce5f610b-117b-46b3-ad06-0e93f5b7a4de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398871(v=OCS.15)
ms:contentKeyID: 49302022
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsPinPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio PIN client a un utente o a un gruppo di utenti. L'autenticazione tramite PIN consente agli utenti di accedere a Lync Server fornendo un PIN anziché un nome utente e una password. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsPinPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 consente di assegnare il criterio RedmondUsersPinPolicy all'utente davidegarghentini@litwareinc.com.

    Grant-CsPinPolicy -Identity "kenmyer@litwareinc.com" -PolicyName RedmondUsersPinPolicy

## ESEMPIO 2

Nell'esempio 2 viene annullata l'assegnazione degli eventuali criteri PIN per utente precedentemente assegnati all'utente kenmyer@litwareinc.com. Chiamando il cmdlet **Grant-CsPinPolicy** e impostando il nome dei criteri su un valore Null ($Null), verranno rimossi gli eventuali criteri per utente assegnati all'utente.

    Grant-CsPinPolicy -Identity kenmyer@litwareinc.com -PolicyName $Null 

## ESEMPIO 3

Nell'esempio 3 vengono assegnati i criteri RedmondUsersPinPolicy a tutti gli utenti che lavorano nella città di Redmond. A tale scopo, il cmdlet **Get-CsUser** recupera innanzitutto una raccolta di tutti gli utenti che lavorano a Redmond. Questa operazione viene eseguita includendo il parametro LdapFilter e utilizzando il valore di filtro "l=Redmond". Nei filtri LDAP la elle minuscola "l" rappresenta la località dell'utente. La raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsPinPolicy**, che assegna i criteri RedmondUsersPinPolicy a ogni utente.

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsPinPolicy -PolicyName RedmondUsersPinPolicy

## ESEMPIO 4

Nell'esempio 4 i criteri RedmondUsersPinPolicy vengono assegnati a tutti gli utenti a cui non sono stati assegnati criteri PIN per utente. Per individuare gli utenti a cui non sono stati assegnati criteri PIN, viene chiamato il cmdlet **Get-CsUser** insieme al parametro Filter. Il valore di filtro {ClientPinPolicy -eq $Null} restituisce solo gli utenti con proprietà ClientPinPolicy impostata su Null (ovvero a cui non sono stati assegnati criteri PIN per utente). La raccolta di utenti viene quindi inviata tramite pipe al cmdlet **Grant-CsPinPolicy**, che assegna i criteri RedmondUsersPinPolicy a ogni persona della raccolta.

    Get-CsUser -Filter {PinPolicy -eq $Null} | Grant-CsPinPolicy -PolicyName RedmondUsersPinPolicy

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite telefono. In genere, l'accesso al sistema o la partecipazione a una conferenza richiedono l'immissione del nome utente e della password. Tale operazione può rappresentare un problema se si utilizza un telefono privo di tastierino alfanumerico. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono quindi accedere al sistema o partecipare a una conferenza immettendo il codice PIN anziché un nome utente e una password.

In Lync Server vengono utilizzati criteri per il PIN per gestire le proprietà di autenticazione tramite PIN. È pertanto possibile specificare la lunghezza minima di un codice PIN, nonché stabilire se consentire codici PIN che utilizzano modelli comuni, ad esempio cifre ripetute (come nel caso del codice PIN 11223344). I criteri per il PIN possono essere configurati nell'ambito globale o nell'ambito del sito. Possono inoltre essere configurati nell'ambito per utente e assegnati quindi a un utente o a un insieme specifico di utenti. Per assegnare un criterio per utente, è necessario utilizzare il cmdlet **Grant-CsPinPolicy**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Grant-CsPinPolicy** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsPinPolicy"}

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
<td><p>Indica il valore Identity dell'account utente a cui assegnare il criterio PIN per utente. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nel foramto dominio\accesso (ad esempio, litwareinc\davidegarghentini), 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). È possibile specificare le identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name come parametro Identity dell'utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il &quot;Nome&quot; del criterio da assegnare. PolicyName corrisponde all'identità del criterio meno l'ambito del criterio (il prefisso &quot;tag:&quot;). Ad esempio, per un criterio con Identity tag:Redmond il parametro PolicyName corrisponde a Redmond, mentre per un criterio con Identity tag:RedmondUsersPinPolicy il parametro PolicyName corrisponde a RedmondUsersPinPolicy. Per annullare l'assegnazione di un criterio per utente precedentemente assegnato a un utente, impostare PolicyName su un valore Null ($Null).</p></td>
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
<td><p>Consente di specificare il nome di dominio completo (FQDN) di un controller di dominio da contattare durante l'assegnazione dei nuovi criteri. Se questo parametro non viene specificato, il cmdlet <strong>Grant-CsPinPolicy</strong> contatterà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare un oggetto utente attraverso la pipeline che rappresenta l'utente a cui viene assegnato il criterio. Per impostazione predefinita, il cmdlet <strong>Grant-CsPinPolicy</strong> non passa oggetti attraverso la pipeline.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.UserPinService.PinInfoDetails. Il cmdlet **Grant-CsPinPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsPinPolicy** non restituisce un oggetto o un valore. Se tuttavia si include il parametro PassThru, il cmdlet restituirà le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsPinPolicy](get-cspinpolicy.md)  
[New-CsPinPolicy](new-cspinpolicy.md)  
[Remove-CsPinPolicy](remove-cspinpolicy.md)  
[Set-CsPinPolicy](set-cspinpolicy.md)

