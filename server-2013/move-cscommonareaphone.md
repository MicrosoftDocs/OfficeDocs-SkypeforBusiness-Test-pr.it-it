---
title: Move-CsCommonAreaPhone
TOCTitle: Move-CsCommonAreaPhone
ms:assetid: af5f832c-1be9-4495-ba1a-c10ca50d7b29
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412837(v=OCS.15)
ms:contentKeyID: 49301673
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsCommonAreaPhone

 

_**Ultima modifica dell'argomento:** 2015-04-02_

Sposta uno o più telefoni di area comune in un nuovo pool di registrazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsCommonAreaPhone -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'Esempio 1 sposta il telefono dell'area comune con identità CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com nel pool di registrazione atl-cs-001.litwareinc.com.

    Move-CsCommonAreaPhone -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## ESEMPIO 2

Nell'esempio 2 il telefono di area comune il cui nome visualizzato in Active Directory è "Building 31 Cafeteria" viene spostato nel pool di registrazione atl-cs-001.litwareinc.com. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsCommonAreaPhone** senza alcun parametro aggiuntivo in modo da restituire una raccolta di tutti i telefoni di area comune attualmente in uso nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i telefoni in cui l'attributo DisplayName è uguale a "Building 31 Cafeteria". Questa raccolta filtrata viene inviata tramite pipe al cmdlet **Move-CsCommonAreaPhone**, che sposta ogni telefono della raccolta in atl-cs-001.litwareinc.com.

    Get-CsCommonAreaPhone | Where-Object {$_.DisplayName -eq "Building 31 Cafeteria"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## ESEMPIO 3

Nell'esempio 3 tutti i telefoni di area comune che attualmente si trovano nel pool di registrazione dublin-cs-001.litwareinc.com vengono spostati nel pool di registrazione atl-cs-001.litwareinc.com. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsCommonAreaPhone** senza alcun parametro per restituire una raccolta di tutti i telefoni di area comune configurati per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti i telefoni di area comune in cui il pool di registrazione è uguale a dublin-cs-001.litwareinc.com. Questa raccolta viene inviata tramite pipe al cmdlet **Move-CsCommonAreaPhone**, che sposta ogni telefono della raccolta nel nuovo pool di registrazione atl-cs-001.litwareinc.com.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com

## ESEMPIO 4

L'esempio 4 è una variante del comando riportato nell'esempio 3. In questo caso tuttavia i telefoni di area comune non vengono solo spostati in un nuovo pool di registrazione, ma vengono anche assegnati a un nuovo criterio vocale per utente. A tale scopo, viene incluso il parametro PassThru quando si chiama il cmdlet **Move-CsCommonAreaPhone**. Questa operazione è necessaria per inviare gli oggetti telefono di area comune tramite la pipeline. Per impostazione predefinita, il cmdlet **Move-CsCommonAreaPhone** non passa alcun oggetto attraverso la pipeline. Dopo che i telefoni sono stati spostati, gli oggetti telefono vengono inviati tramite pipe al cmdlet **Grant-CsVoicePolicy**, che assegna il criterio vocale AtlantaVoicePolicy a ognuno dei telefoni appena spostati.

    Get-CsCommonAreaPhone | Where-Object {$_.RegistrarPool -match "dublin-cs-001.litwareinc.com"} | Move-CsCommonAreaPhone -Target atl-cs-001.litwareinc.com -PassThru | Grant-CsVoicePolicy -PolicyName AtlantaVoicePolicy

## Descrizione dettagliata

I telefoni di area comune sono telefoni IP non associati a un singolo utente. Invece di essere installati in qualche ufficio, tali telefoni sono generalmente posizionati nelle sale d'attesa degli edifici, nelle mense, nelle aree riservate ai dipendenti, nelle sale riunioni e in altri luoghi in cui è probabile si ritrovino molte persone. Per gli amministratori questa è una sfida gestionale, in quanto l'utilizzo dei telefoni in Lync Server viene normalmente gestito mediante criteri vocali e dial plan assegnati a utenti singoli. Ai telefoni di area comune non viene assegnato un utente specifico.

La soluzione a questa sfida è rappresentata dalla creazione di oggetti contatto di Active Directory per tutti i telefoni nelle aree comuni. Questi oggetti contatto possono essere creati usando il cmdlet **New-CsCommonAreaPhone**. Come nel caso degli account utente, anche a questi oggetti contatto è possibile assegnare criteri e voice plan. Di conseguenza, sarà possibile mantenere il controllo dei telefoni nelle aree comuni anche se non sono associati a singoli utenti. Ad esempio, se si desidera evitare che le persone possano trasferire o parcheggiare le chiamate da un telefono in un'area comune, è possibile creare un criterio vocale che impedisca il trasferimento o il parcheggio delle chiamate e quindi assegnare questo criterio ai telefoni nelle aree comuni (oppure, più correttamente, all'oggetto contatto che rappresenta il telefono nell'area comune).

Il cmdlet **Move-CsCommonAreaPhone** consente di spostare un telefono delle aree comuni esistente in un altro pool di registrazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Move-CsCommonAreaPhone** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Il permesso di eseguire questo cmdlet per siti specifici o specifiche unità organizzative di Active Directory (OU) può essere assegnato utilizzando il cmdlet **Grant-CsOUPermission**. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsCommonAreaPhone"}

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
<td><p>Identificatore univoco per il telefono dell'area comune. I telefoni delle aree comuni vengono identificati tramite il nome distinto di Active Directory dell'oggetto contatto associato. Per impostazione predefinita, i telefoni delle aree comuni utilizzano un identificatore univoco globale (GUID) come nome comune; i telefoni avranno quindi un parametro Identity analogo al seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome completo di dominio (FQDN) del pool di registrazione dove deve essere spostato il telefono dell'area comune; ad esempio: atl-cs-001.litwareinc.com. In aggiunta al pool di registrazione il parametro Target può essere costituito dal FQDN di un provider di hosting.</p></td>
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
<td><p>Consente di connettersi al controller di dominio specificato per spostare un telefono dell'area comune. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-cs-001) o dal suo FQDN (ad esempio, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, consente di spostare il telefono dell'area comune e di eliminare eventuali dati associati (ad esempio, i criteri assegnati al dispositivo). Se non è presente, il telefono viene spostato insieme ai dati associati.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, indica al computer di ignorare gli eventuali errori che potrebbero verificarsi con il database back-end e di tentare di spostare il telefono di area comune nonostante tali errori.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di specificare attraverso la pipeline un oggetto utente che rappresenta l'account utente che si sta spostando. Per impostazione predefinita, il cmdlet <strong>Move-CsCommonAreaPhone</strong> non fornisce alcun oggetto attraverso la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro viene utilizzato solo per Lync Online. Non deve essere utilizzato con un'implementazione locale di Lync Server.</p></td>
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

Stringa. Il cmdlet **Move-CsCommonAreaPhone** accetta valori stringa che rappresentano l'identità del telefono di area comune inviati tramite pipeline.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Move-CsCommonAreaPhone** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituirà istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

