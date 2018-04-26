---
title: Remove-CsAnalogDevice
TOCTitle: Remove-CsAnalogDevice
ms:assetid: 61250894-fde6-476d-aaa2-ec5692af02b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398433(v=OCS.15)
ms:contentKeyID: 49300738
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAnalogDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un dispositivo esistente dalla raccolta di dispositivi analogici che è possibile gestire tramite Lync Server. Un dispositivo analogico è un telefono o un altro dispositivo connesso alla rete PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsAnalogDevice -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene eliminato il dispositivo analogico con Identity CN={e5e7daba-394e-46ec-95a1-1f2a9947aad2},CN=Users,DC=litwareinc,DC=com.

    Remove-CsAnalogDevice -Identity "CN={e5e7daba-394e-46ec-95a1-1f2a9947aad2},CN=Users,DC=litwareinc,DC=com"

## ESEMPIO 2

Il comando mostrato nell'esempio 2 elimina tutti i dispositivi analogici a cui è stato assegnato il nome visualizzato "Building 14 Receptionist". A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsAnalogDevice** e il parametro Filter. Il valore di filtro {DisplayName -eq "Building 14 Receptionist"} limita gli oggetti restituiti ai dispositivi analogici con proprietà DisplayName uguale a "Building 14 Receptionist". Gli elementi restituiti vengono quindi inviati tramite pipe al cmdlet **Remove-CsAnalogDevice**, che li rimuove.

    Get-CsAnalogDevice -Filter {DisplayName -eq "Building 14 Receptionist"} | Remove-CsAnalogDevice

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i dispositivi analogici a cui è stato assegnato il criterio vocale RedmondVoicePolicy. A tale scopo, vengono utilizzati il cmdlet **Get-CsAnalogDevice** e il parametro Filter per recuperare tutti i dispositivi analogici con proprietà VoicePolicy uguale a RedmondVoicePolicy. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsAnalogDevice**, che elimina tutti gli elementi della raccolta.

    Get-CsAnalogDevice -Filter {VoicePolicy -eq "RedmondVoicePolicy"} | Remove-CsAnalogDevice

## ESEMPIO 4

Il comando mostrato nell'esempio 4 rimuove tutti i fax analogici attualmente in uso nell'organizzazione. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsAnalogDevice** insieme al parametro Filter. Il valore di filtro {AnalogFax –eq $True} seleziona solo i dispositivi con proprietà AnalogFax uguale a True. La raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsAnalogDevice**, che rimuove tutti gli elementi della raccolta.

    Get-CsAnalogDevice -Filter {AnalogFax -eq $True} | Remove-CsAnalogDevice

## Descrizione dettagliata

Tra i dispositivi analogici sono inclusi telefoni, fax, modem e dispositivi TTY/TTD (Teletype/Telecommunication Device for the Deaf) connessi alla rete PSTN (Public Switched Telephone Network). Contrariamente ai dispositivi basati su VoIP aziendale, ovvero la soluzione VoIP (Voice over Internet Protocol) offerta da Microsoft, i dispositivi analogici non trasmettono informazioni utilizzando pacchetti digitali. Le informazioni vengono invece trasmesse tramite un segnale continuo. Questo segnale viene comunemente definito segnale analogico e da qui deriva il termine "dispositivi analogici".

Per consentire agli amministratori di gestire i dispositivi analogici per le organizzazioni, Lync Server offre la possibilità di associare tali dispositivi agli oggetti contatto di Active Directory. Dopo aver associato un dispositivo a un oggetto contatto, è possibile gestire il dispositivo analogico assegnando criteri e dial plan al contatto.

Nel tempo potrebbe essere necessario eliminare un oggetto contatto associato a un dispositivo analogico. Se ad esempio si eliminano gradualmente tutti i fax, non sarà più necessario disporre dei dispositivi analogici e degli oggetti contatto associati a tali apparecchi. Il cmdlet **Remove-CsAnalogDevice** consente di eliminare i dispositivi analogici. Eseguendo questo cmdlet, il dispositivo viene eliminato dall'elenco dei dispositivi analogici restituiti dal cmdlet **Get-CsAnalogDevice**. Verrà eliminato da Servizi di dominio Active Directory anche l'oggetto contatto associato a tale dispositivo.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsAnalogDevice** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Le autorizzazioni per l'esecuzione di questo cmdlet per siti oppure unità organizzative di Active Directory specifiche possono essere assegnate tramite il cmdlet **Grant-CsOUPermission**. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAnalogDevice"}

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
<td><p>Identificatore univoco per il dispositivo analogico da rimuovere. I dispositivi analogici vengono identificati utilizzando il nome distinto (DN) Active Directory dell'oggetto contatto associato. Per impostazione predefinita, questi dispositivi utilizzano un identificatore univoco globale (GUID) come nome comune e pertanto presentano in genere una proprietà Identity simile alla seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Per questo motivo, è possibile che risulti più semplice recuperare i dispositivi analogici tramite il cmdlet <strong>Get-CsAnalogDevice</strong> e quindi inviare tramite pipe al cmdlet <strong>Remove-CsAnalogDevice</strong> gli oggetti restituiti.</p></td>
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

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact. Il cmdlet **Remove-CsAnalogDevice** accetta istanze dell'oggetto dispositivo analogico inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Remove-CsAnalogDevice** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

