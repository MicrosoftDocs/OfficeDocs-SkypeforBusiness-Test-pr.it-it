---
title: Grant-CsArchivingPolicy
TOCTitle: Grant-CsArchivingPolicy
ms:assetid: 675f5d8d-d8f9-4d19-b11b-75df48b09467
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398475(v=OCS.15)
ms:contentKeyID: 49300823
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsArchivingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di assegnare criteri di archiviazione delle sessioni di messaggistica istantanea a utenti o a insiemi di utenti. Tali criteri consentono di archiviare tutte le sessioni di messaggistica istantanea eseguite tra utenti interni e/o di archiviare tutte le sessioni di messaggistica istantanea eseguite tra utenti interni e partner esterni. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsArchivingPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 il criterio di archiviazione RedmondArchivingPolicy viene assegnato all'utente con nome visualizzato "Ken Myer". Nel caso del cmdlet **Grant-CsArchivingPolicy**, la proprietà Identity fa riferimento all'identità dell'utente, non del criterio di archiviazione. Il criterio da assegnare invece deve essere specificato con il parametro PolicyName. Il valore del parametro è l'identità del criterio (ad esclusione del prefisso "tag:" ).

    Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName RedmondArchivingPolicy

## ESEMPIO 2

Nell'esempio 2 viene assegnato a tutti gli utenti con account nell'unità organizzativa (OU) Redmond il criterio di archiviazione RedmondArchivingPolicy. A tale scopo, vengono utilizzati il cmdlet **Get-CsUser** e il parametro OU per restituire una raccolta di tutti gli utenti che dispongono di account nell'unità organizzativa con nome distinto "OU=Redmond,dc=litwareinc,dc=com". La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsArchivingPolicy**, che assegna il criterio RedmondArchivingPolicy a ogni utente della raccolta.

    Get-CsUser -OU "OU=Redmond,dc=litwareinc,dc=com" | Grant-CsArchivingPolicy -PolicyName RedmondArchivingPolicy

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 viene assegnato il criterio RedmondArchivingPolicy a tutti gli utenti che lavorano a Redmond. A tale scopo, viene chiamato il cmdlet **Get-CsUser** con il parametro LdapFilter. Il valore del filtro LDAP "l=Redmond" restituisce una raccolta di tutti gli utenti che lavorano nella città di Redmond. Nel linguaggio di query LDAP, l (elle minuscola) è l'abbreviazione di "località" e corrisponde quindi alla città. La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsArchivingPolicy**, che assegna il criterio RedmondArchivingPolicy a ogni utente nella raccolta.

    Get-CsUser -LdapFilter "l=Redmond" | Grant-CsArchivingPolicy -PolicyName RedmondArchivingPolicy

## ESEMPIO 4

Con l'esempio 4 a tutti gli utenti residenti nel pool di registrazione atl-cs-001.litwareinc.com viene assegnato il criterio RedmondArchivingPolicy. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsUser** per restituire tutti gli utenti abilitati per Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli utenti con RegistrarPool uguale ad atl-cs-001-litwareinc.com. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Grant-CsArchivingPolicy**, che assegna il criterio RedmondArchivingPolicy a ogni utente nella raccolta.

    Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsArchivingPolicy -PolicyName RedmondArchivingPolicy

## ESEMPIO 5

Con l'esempio 5 vengono individuati tutti gli utenti a cui è stato assegnato il criterio RedmondArchivingPolicy, quindi a ognuno di questi utenti viene assegnato un criterio diverso, NorthAmericaArchivingPolicy. A tale scopo, viene utilizzato il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti abilitati per Lync Server. Il parametro Filter e il valore del filtro {ArchivingPolicy -eq "RedmondArchivingPolicy"} limitano i dati restituiti agli account in cui ArchivingPolicy è uguale a "RedmondArchivingPolicy". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Grant-CsArchivingPolicy**, che assegna il criterio NorthAmericaArchivingPolicy a ogni utente nella raccolta.

    Get-CsUser -Filter {ArchivingPolicy -eq "RedmondArchivingPolicy"} | Grant-CsArchivingPolicy -PolicyName "NorthAmericaArchivingPolicy"

## ESEMPIO 6

L'esempio 6 è una variante dell'esempio 5. Questa volta però il criterio RedmondArchivingPolicy viene rimosso dagli utenti a cui era stato assegnato in precedenza. Chiamando il cmdlet **Grant-CsArchivingPolicy** con PolicyName uguale a $Null, vengono rimossi tutti i criteri per utente assegnati in precedenza.

    Get-CsUser -Filter {ArchivingPolicy -eq "RedmondArchivingPolicy"} | Grant-CsArchivingPolicy -PolicyName $Null

## Descrizione dettagliata

Molte organizzazioni considerano utile conservare tutte le sessioni di messaggistica istantanea a cui prendono parte gli utenti. Altre organizzazioni invece sono tenute a mantenere queste sessioni come archivi. Per archiviare le sessioni di messaggistica istantanea con Lync Server, è necessario eseguire due passaggi. Abilitare innanzitutto l'archiviazione nell'ambito globale e/o del sito utilizzando il cmdlet **Set-CsArchivingConfiguration**. In questo modo viene fornita la possibilità di archiviare sessioni di messaggistica istantanea. L'archiviazione di tali sessioni tuttavia non inizia automaticamente.

Per salvare delle trascrizioni delle sessioni di messaggistica istantanea è necessario completare il secondo passaggio: creare uno o più criteri di archiviazione delle sessioni di messaggistica istantanea. Questi criteri determinano per quali utenti vengono registrate le sessioni di messaggistica istantanea e quali tipi di sessioni di messaggistica istantanea (interne e/o esterne) vengono archiviate. Le sessioni di messaggistica istantanea interne sono sessioni in cui tutti i partecipanti sono utenti autenticati che dispongono di account Active Directory nell'organizzazione. Le sessioni di messaggistica istantanea esterne, invece, sono sessioni in cui almeno uno dei partecipanti è un utente non autenticato che non dispone di un account Active Directory nell'organizzazione. È possibile scegliere di archiviare soltanto sessioni interne, soltanto sessioni esterne oppure entrambi i tipi.

I criteri di archiviazione possono essere assegnati nell'ambito globale o del sito. Tali criteri possono inoltre essere assegnati nell'ambito per utente e quindi essere applicati a un utente o a un gruppo di utenti specifico. Si supponga, ad esempio, che il criterio globale in uso consenta di archiviare solo le sessioni di messaggistica istantanea interne. In questo caso, si potrebbe creare un secondo criterio per archiviare sia le sessioni interne che quelle esterne e applicare il criterio solo al personale addetto alle vendite. Poiché i criteri per utente hanno la precedenza sui criteri globali e di sito, per i membri dello staff di vendita verranno archiviate tutte le sessioni di messaggistica istantanea. Per tutti gli altri utenti, ovvero gli utenti che non appartengono al reparto vendite e a cui non viene applicato il criterio relativo alle vendite, verranno archiviate solamente le sessioni di messaggistica istantanea interne.

Il cmdlet **Grant-CsArchivingPolicy** è utilizzato per assegnare i criteri di archiviazione per utente a un utente o a un set di utenti specificato.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Grant-CsArchivingPolicy** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsArchivingPolicy"}

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
<td><p>Indica l'identità dell'account utente a cui assegnare i criteri. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) L'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio dell'utente e il nome di accesso nel formato dominio\accesso (ad esempio litwareinc\kenmyer); 4) il nome visualizzato in Servizi di dominio Active Directory dell'utente (ad esempio, Ken Myer). Le identità utente possono essere referenziate anche utilizzando il nome distinto dell'utente in Active Directory.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come valore Identity dell'utente. L'identità &quot;* Smith&quot; restituisce ad esempio tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il &quot;Nome&quot; del criterio da assegnare. PolicyName corrisponde all'identità del criterio meno il designatore di ambito &quot;tag:&quot;. Ad esempio, un criterio con Identity tag:Redmond dispone di un PolicyName uguale a Redmond; un criterio con Identity tag:RedmondArchivingPolicy dispone di un PolicyName uguale a RedmondArchivingPolicy.</p>
<p>Per rimuovere un criterio per utente assegnato a un utente, impostare PolicyName su un valore null:</p>
<p>-PolicyName $Null</p></td>
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
<td><p>Se presente, il cmdlet passa l'oggetto (o gli oggetti) utente attraverso la pipeline di Windows PowerShell. Per impostazione predefinita, il cmdlet <strong>Grant-CsArchivingPolicy</strong> non passa alcun oggetto attraverso la pipeline.</p></td>
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

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Grant-CsArchivingPolicy** accetta l'input da pipeline di valori stringa che rappresentano l'identità (Identity) di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Il cmdlet **Grant-CsArchivingPolicy** non restituisce alcun oggetto o valore. In realtà il cmdlet assegna istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.IM.ImArchivingPolicy a utenti o a gruppi di utenti. Se tuttavia si include il parametro PassThru, il cmdlet restituisce istanze di Microsoft.Rtc.Management.ADConnect.Schema.OCSUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)

