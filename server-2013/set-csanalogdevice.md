---
title: Set-CsAnalogDevice
TOCTitle: Set-CsAnalogDevice
ms:assetid: b05e729e-cdef-4c78-8ce7-b183c3208a93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412843(v=OCS.15)
ms:contentKeyID: 49301675
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAnalogDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un dispositivo esistente nella raccolta di dispositivi analogici che è possibile gestire tramite Lync Server. Un dispositivo analogico è un telefono o un altro dispositivo connesso alla rete PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAnalogDevice -Identity <UserIdParameter> [-AnalogFax <$true | $false>] [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-Gateway <Fqdn>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene modificato il valore della proprietà LineUri del dispositivo analogico con l'identità CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.

    Set-CsAnalogDevice -Identity "CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com" -LineUri "TEL:+14255551298"

## ESEMPIO 2

Il comando riportato nell'esempio 2 consente di cambiare il gateway di ogni dispositivo analogico che attualmente utilizza il gateway 192.168.0.240. A tale scopo, viene chiamato il cmdlet **Get-CsAnalogDevice** con il parametro Filter. Il valore di filtro {Gateway -eq "192.168.0.240"} restituisce solo i dispositivi con Gateway uguale a (-eq) 192.168.0.240. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsAnalogDevice**, che imposta la proprietà Gateway su 192.168.1.100 per ogni elemento della raccolta.

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"} | Set-CsAnalogDevice -Gateway "192.168.1.100"

## Descrizione dettagliata

I dispositivi analogici includono telefoni, apparecchi fax, modem e dispositivi TTY/TTD (Teletype/Telecommunication Devices for the Deaf) connessi alla rete PSTN (Public Switched Telephone Network). A differenza dei dispositivi che traggono vantaggio da VoIP aziendale, la soluzione VoIP offerta da Microsoft, i dispositivi analogici non trasmettono informazioni utilizzando pacchetti digitali. Le informazioni, invece, vengono trasmesse utilizzando un segnale continuo. Questo segnale viene comunemente denominato segnale analogico; da qui l'espressione "dispositivi analogici".

Per consentire agli amministratori di gestire i dispositivi analogici, Lync Server offre la possibilità di associare tali dispositivi agli oggetti contatto di Active Directory. Dopo aver associato un dispositivo a un oggetto contatto, è possibile gestire il dispositivo analogico assegnando criteri e dial plan al contatto.

Il cmdlet **Set-CsAnalogDevice** consente di modificare le proprietà degli oggetti contatto associati ai dispositivi analogici. Ad esempio, è possibile cambiare il nome visualizzato del contatto di Active Directory e anche l'URI linea associato al dispositivo.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsAnalogDevice** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Il permesso di eseguire questo cmdlet per siti specifici o specifiche unità organizzative di Active Directory (OU) può essere assegnato utilizzando il cmdlet **Grant-CsOUPermission**. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAnalogDevice"}

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
<td><p>UserIdParameter</p></td>
<td><p>Identificatore univoco per il dispositivo analogico che viene modificato. I dispositivi analogici vengono identificati utilizzando il nome distinto Active Directory (DN) dell'oggetto contatto associato. Per impostazione predefinita, nei dispositivi analogici viene utilizzato un GUID (identificatore univoco globale) come nome comune, pertanto in genere l'identità dei dispositivi è simile alla seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Per questo motivo, potrebbe risultare più semplice modificare i dispositivi analogici utilizzando il cmdlet <strong>Get-CsAnalogDevice</strong> per restituire gli oggetti dispositivi analogici e quindi inviando tramite pipe tali oggetti al cmdlet <strong>Set-CsAnalogDevice</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AnalogFax</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Impostare su True ($True) se il dispositivo analogico è un apparecchio fax. Impostare su False($False) se il dispositivo analogico non è un apparecchio fax.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Consente di configurare il nome visualizzato in Active Directory del dispositivo analogico.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Numero di telefono come viene visualizzato in Lync. La proprietà DisplayNumber può essere formattata in qualsiasi modo. Ad esempio, 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234 e così via.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specificato per modificare le informazioni sul contatto. Per la connessione a uno specifico controller di dominio, includere il parametro -DomainController seguito dal nome computer (ad esempio atl-mcs-001) o dal suo nome di dominio completo (FQDN) (ad esempio atl-mcs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Quando il valore è True ($True), il dispositivo analogico può essere utilizzato con Lync.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'oggetto contatto per il dispositivo analogico è stato abilitato per VoIP aziendale, la soluzione VoIP offerta da Microsoft. Con VoIP aziendale, è possibile effettuare chiamate via Internet anziché utilizzare la rete telefonica standard.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica la posizione in cui vengono archiviate le sessioni di messaggistica istantanea del contatto. I valori consentiti sono:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>Gateway</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Fqdn</p></td>
<td><p>Indirizzo IP del gateway PSTN utilizzato dal dispositivo analogico.</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Numero di telefono del dispositivo analogico. L'URI di linea deve essere specificato utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;. Ad esempio: TEL:+14255551297. Qualsiasi numero di interno deve essere aggiunto alla fine dell'URI di linea, ad esempio: TEL:+14255551297;ext=51297.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>witchParameter</p></td>
<td><p>Restituisce un oggetto che rappresenta il telefono nell'area comune.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identificatore univoco che consente al dispositivo analogico di comunicare con i dispositivi SIP, ad esempio Lync 2013. L'indirizzo SIP deve essere preceduto dal prefisso &quot;sip:&quot;, ad esempio sip:bldg14lobby@litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact. Il cmdlet **Set-CsAnalogDevice** accetta le istanze da pipeline dell'oggetto dispositivo analogico.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Set-CsAnalogDevice** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituirà istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)

