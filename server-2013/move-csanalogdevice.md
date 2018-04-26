---
title: Move-CsAnalogDevice
TOCTitle: Move-CsAnalogDevice
ms:assetid: c629c5f8-93e7-4fe4-ad51-52bc0ae99a46
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398816(v=OCS.15)
ms:contentKeyID: 49301944
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsAnalogDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sposta uno o più dispositivi analogici in un nuovo pool di registrazione. Un dispositivo analogico è un telefono o un altro dispositivo connesso alla rete PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsAnalogDevice -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Con il comando riportato nell'esempio 1 il dispositivo analogico con valore Identity CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com viene spostato nel pool di registrazione atl-cs-001.litwareinc.com.

    Move-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -Target atl-cs-001.litwareinc.com

## Esempio 2

Nell'esempio 2 il dispositivo analogico con nome visualizzato Active Directory "Building 14, Room 142" viene spostato nel pool di registrazione atl-cs-001.litwareinc.com. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsAnalogDevice** senza alcun parametro per restituire una raccolta di tutti i dispositivi analogici attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti i dispositivi con nome visualizzato "Building 14, Room 142". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Move-CsAnalogDevice**, che sposta tutti i dispositivi della raccolta nel pool di registrazione atl-cs-001.litwareinc.com.

    Get-CsAnalogDevice | Where-Object {$_.DisplayName -eq "Building 14, Room 142"} | Move-CsAnalogDevice -Target atl-cs-001.litwareinc.com

## Esempio 3

Tramite il comando illustrato nell'esempio 3 vengono spostati tutti i dispositivi analogici con nome visualizzato che inizia con il valore stringa "Building 14". Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsAnalogDevice** per restituire una raccolta di tutti i dispositivi analogici attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti i dispositivi con nome visualizzato che inizia con il valore stringa "Building 14". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Move-CsAnalogDevice**, che sposta ciascun dispositivo della raccolta nel pool di registrazione atl-cs-001.litwareinc.com.

    Get-CsAnalogDevice | Where-Object {$_.DisplayName -like "Building 14*"} | Move-CsAnalogDevice -Target atl-cs-001.litwareinc.com

## Descrizione dettagliata

Tra i dispositivi analogici sono inclusi i telefoni, i fax, i modem e i dispositivi TTY/TTD (Teletype/Telecommunication Devices for the Deaf) connessi alla rete PSTN (Public Switched Telephone Network). Contrariamente ai dispositivi basati su VoIP aziendale, ovvero la soluzione VoIP (Voice over Internet Protocol) offerta da Microsoft, i dispositivi analogici non trasmettono informazioni utilizzando pacchetti digitali. Le informazioni invece vengono trasmesse tramite un segnale continuo. Questo segnale viene comunemente denominato segnale analogico, da cui l'espressione "dispositivi analogici".

Affinché gli amministratori possano gestire i dispositivi analogici, Lync Server consente di associare i dispositivi analogici agli oggetti contatto di Active Directory. Una volta associato un dispositivo a un oggetto contatto, è possibile gestire il dispositivo analogico assegnando criteri e dial plan al contatto.

Il cmdlet **Move-CsAnalogDevice** consente di spostare in un nuovo pool di registrazione un dispositivo analogico esistente.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Move-CsAnalogDevice** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Le autorizzazioni per l'esecuzione di questo cmdlet per siti o unità organizzative di Active Directory specifiche possono essere assegnate tramite il cmdlet **Grant-CsOUPermission**. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsAnalogDevice"}

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
<td><p>Identificatore univoco per il dispositivo analogico. I dispositivi analogici vengono identificati utilizzando il nome distinto Active Directory dell'oggetto contatto associato. Per impostazione predefinita, i dispositivi analogici utilizzano un identificatore univoco globale (GUID) come nome comune. Questo significa che in genere i dispositivi utilizzano un'identità simile alla seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN), ad esempio atl-cs-001.litwareinc.com, del pool di registrazione in cui deve essere spostato il dispositivo analogico. Oltre a un pool di registrazione, il parametro Target può anche indicare il nome FQDN di un provider di hosting.</p></td>
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
<td><p>Consente di connettersi al controller di dominio specificato per spostare il dispositivo analogico. Per la connessione a uno specifico controller di dominio, includere il parametro DomainController seguito dal nome computer (ad esempio atl-cs-001) o dal relativo nome FQDN (ad esempio atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, sposta il dispositivo analogico, ma elimina gli eventuali dati associati, ad esempio i criteri assegnati al dispositivo. Se non è presente, il dispositivo viene spostato insieme agli eventuali dati associati.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, indica al computer di ignorare eventuali errori che potrebbero verificarsi con il database back-end e tenta di spostare il telefono area comune malgrado questi errori.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare un oggetto utente attraverso la pipeline che rappresenta l'account utente spostato. Per impostazione predefinita, il cmdlet <strong>Move-CsAnalogDevice</strong> non passa oggetti tramite la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro viene utilizzato solo per Microsoft Lync Online 2010. Non deve essere utilizzato con un'implementazione locale di Lync Server.</p></td>
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

Stringa. Il cmdlet **Move-CsAnalogDevice** accetta un valore stringa da pipeline che rappresenta l'identità del dispositivo analogico.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Move-CsAnalogDevice** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituirà le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

