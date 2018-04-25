---
title: Grant-CsClientVersionPolicy
TOCTitle: Grant-CsClientVersionPolicy
ms:assetid: b94d9473-db5f-4350-a7b4-991d0e26e525
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412903(v=OCS.15)
ms:contentKeyID: 49301782
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsClientVersionPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio di versione client all'ambito globale, del sito, del servizio o per utente. I criteri di versione client consentono di specificare quali client, ad esempio Microsoft Office Communicator 2007 R2, saranno in grado di accedere al sistema Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsClientVersionPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, i criteri di versione client RedmondClientVersionPolicy sono assegnati all'utente Davide Garghentini.

    Grant-CsClientVersionPolicy -Identity "Ken Myer" -PolicyName "RedmondClientVersionPolicy"

## ESEMPIO 2

Il comando mostrato nell'esempio 2 assegna i criteri di versione client RedmondClientVersionPolicy a tutti gli utenti che lavorano nella città di Redmond. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsUser** e il parametro LdapFilter per recuperare la raccolta di account utente appropriata. Il valore di filtro "l=Redmond" (dove la lettera elle minuscola "l" corrisponde al nome dell'attributo LDAP che indica la "località") limita il recupero dei dati agli utenti che lavorano nella città di Redmond. La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsClientVersionPolicy**, che assegna il criterio specificato a ogni utente della raccolta.

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## ESEMPIO 3

Nell'esempio 3 il criterio di versione client RedmondClientVersionPolicy viene assegnato a tutti gli utenti di un'unità organizzativa (OU) specifica. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** e il parametro OU. Il valore del parametro rappresenta il nome distinto dell'unità organizzativa ai cui utenti deve essere assegnato il criterio di versione client (ou=Redmond,ou=North America,dc=litwareinc,dc=com). Dopo che sono stati recuperati gli account utente, la raccolta viene inviata tramite pipe al cmdlet **Grant-CsClientVersionPolicy**, che assegna RedmondClientVersionPolicy a ognuno degli utenti.

    Get-CsUser -OU "ou=Redmond,ou=North America,dc=litwareinc,dc=com" | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## ESEMPIO 4

Nell'esempio 4 il criterio di versione client RedmondClientVersionPolicy viene assegnato a tutti gli utenti a cui era stato precedentemente assegnato il criterio vocale RedmondVoicePolicy. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsUser** insieme al parametro Filter. Il valore di filtro {VoicePolicy -eq "RedmondVoicePolicy"} assicura che vengano restituiti solo gli account utente in cui la proprietà VoicePolicy è uguale a "RedmondVoicePolicy". Gli account utente risultanti vengono quindi inviati tramite pipe al cmdlet **Grant-CsClientVersionPolicy** e viene loro assegnato il criterio di versione client RedmondClientVersionPolicy.

    Get-CsUser -Filter {VoicePolicy -eq "RedmondVoicePolicy"} | Grant-CsClientVersionPolicy -PolicyName "RedmondClientVersionPolicy"

## ESEMPIO 5

Nell'esempio 5 per tutti gli utenti dell'organizzazione viene annullata l'assegnazione dei criteri di versione client per utente precedentemente assegnati. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti dell'organizzazione che sono stati abilitati per Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsClientVersionPolicy**, che rimuove tutti i criteri di versione client per utente assegnati a tali utenti. Questa operazione viene eseguita impostando il valore di parametro PolicyName su $null.

    Get-CsUser | Grant-CsClientVersionPolicy -PolicyName $Null

## Descrizione dettagliata

I criteri di versione client rappresentano una raccolta di regole di versione client. Tali regole, a loro volta, vengono utilizzate per stabilire a quali applicazioni client è consentito accedere a Lync Server. Quando un utente tenta di accedere a Lync Server, la relativa applicazione client invia un'intestazione SIP al server. In questa intestazione sono incluse informazioni dettagliate sull'applicazione, tra cui la versione principale, la versione secondaria e il numero di build del software. Le informazioni sulla versione incluse nell'intestazione SIP vengono quindi verificate a fronte di una raccolta di regole di versione client per stabilire se alcune di queste regole si applicano a quella particolare applicazione. Se tale regola esiste, in Lync Server verrà eseguita l'azione specificata dalla regola. La regola ad esempio potrebbe indicare a Lync Server di consentire l'accesso, di bloccarlo oppure di autorizzarlo aggiornando però automaticamente l'applicazione client all'ultima versione, ad esempio da Office Communicator 2007 R2 a Lync 2013.

I criteri di versione client possono essere applicati nell'ambito globale, del sito, del servizio (solo servizio di registrazione) o del singolo utente e offrono una notevole flessibilità nello stabilire quali applicazioni client possono essere utilizzate per accedere al sistema. È ad esempio possibile decidere di impedire agli utenti di accedere a Lync Server utilizzando Communicator 2007 R2 perché questa versione precedente dell'applicazione client non supporta le stesse caratteristiche e funzionalità di Lync. A causa di conflitti hardware o software, può tuttavia accadere che anche un determinato gruppo di utenti non possa eseguire l'aggiornamento a Lync. In questo caso, è possibile creare una regola separata e un criterio di versione client distinto per consentire a tali utenti di effettuare l'accesso da Communicator 2007 R2.

Il cmdlet **Grant-CsClientVersionPolicy** consente di assegnare criteri di versione client a singoli utenti. Quando si crea un criterio per utente, questo non viene automaticamente assegnato. L'assegnazione non viene effettuata finché non si chiama il cmdlet **Grant-CsClientVersionPolicy** per assegnare esplicitamente il criterio a un utente o a un insieme di utenti.

È importante notare che i criteri di versione client non si applicano agli utenti federati, i quali invece sono vincolati dai criteri di versione client utilizzati nella propria organizzazione. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Finché tale organizzazione federata consentirà l'utilizzo del client A, l'utente sarà in grado di comunicare con l'organizzazione avvalendosi del client in questione. Lo stesso avverrà anche se il criterio di versione client blocca l'utilizzo del client A. I criteri di versione client applicati nella propria organizzazione non hanno la priorità sui criteri di versione client utilizzati in un'organizzazione federata.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Grant-CsClientVersionPolicy** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsClientVersionPolicy"}

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
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come valore Identity dell'utente. L'identità &quot;* Smith&quot; restituisce, ad esempio, tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il &quot;Nome&quot; del criterio da assegnare. PolicyName corrisponde all'identità del criterio meno l'ambito del criterio (il prefisso &quot;tag:&quot;). Un criterio con valore Identity tag:Redmond ad esempio dispone di un valore PolicyName uguale a Redmond, mentre un criterio con valore Identity tag:RedmondClientVersionPolic dispone di un valore PolicyName uguale a RedmondClientVersionPolicy. Per annullare l'assegnazione di un criterio per utente precedentemente assegnato a un utente, impostare PolicyName su un valore Null ($Null).</p></td>
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
<td><p>Se presente, il cmdlet passa l'oggetto (o gli oggetti) utente attraverso la pipeline di Windows PowerShell. Per impostazione predefinita, il cmdlet <strong>Grant-CsClientVersionPolicy</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Grant-CsClientVersionPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità (Identity) di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Grant-CsClientVersionPolicy** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituirà istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

