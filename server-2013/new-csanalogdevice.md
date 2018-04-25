---
title: New-CsAnalogDevice
TOCTitle: New-CsAnalogDevice
ms:assetid: c02755d6-b651-4385-91a0-5b594dc67751
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412937(v=OCS.15)
ms:contentKeyID: 49301869
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAnalogDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo dispositivo analogico che può essere gestito tramite Lync Server. Un dispositivo analogico è un telefono o un altro dispositivo connesso alla rete PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsAnalogDevice -DN <ADObjectId> <COMMON PARAMETERS>

    New-CsAnalogDevice -OU <OUIdParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: -AnalogFax <$true | $false> -Gateway <Fqdn> -LineUri <String> -RegistrarPool <Fqdn> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando riportato nell'esempio 1 viene creato un nuovo dispositivo analogico con numero di telefono (LineUri) 1-425-555-6001. Per specificare il numero di telefono è stato utilizzato il formato E.164. Oltre al parametro LineUri, gli altri parametri utilizzati in questo comando sono DisplayName (per impostare il nome visualizzato Active Directory del dispositivo), RegistrarPool (per specificare il pool di registrazione), AnalogFax (impostato su $False per indicare che si tratta di un telefono e non di un apparecchio fax), Gateway (impostato sull'indirizzo IP del gateway) e OU (nome distinto dell'unità organizzativa di Active Directory in cui deve essere creato l'oggetto contatto del dispositivo).

    New-CsAnalogDevice -LineUri tel:+14255556001 -DisplayName "Building 14 Receptionist" -RegistrarPool redmond-Cs-001.litwareinc.com -AnalogFax $False -Gateway 192.168.0.240 -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## Descrizione dettagliata

Tra i dispositivi analogici sono inclusi i telefoni, i fax, i modem e i dispositivi TTY/TTD (Teletype/Telecommunication Devices for the Deaf) connessi alla rete PSTN (Public Switched Telephone Network). Contrariamente ai dispositivi basati su VoIP aziendale, ovvero la soluzione VoIP (Voice over Internet Protocol) offerta da Microsoft, i dispositivi analogici non trasmettono informazioni utilizzando pacchetti digitali. Le informazioni invece vengono trasmesse tramite un segnale continuo. Questo segnale viene comunemente denominato segnale analogico, da cui l'espressione "dispositivi analogici".

Affinché gli amministratori possano gestire i dispositivi analogici, Lync Server consente di associare i dispositivi analogici agli oggetti contatto di Active Directory. Una volta associato un dispositivo a un oggetto contatto, è possibile gestire il dispositivo analogico assegnando criteri e dial plan al contatto.

I nuovi dispositivi analogici vengono creati mediante il cmdlet **New-CsAnalogDevice**. Il cmdlet è in grado di creare nuovi oggetti contatto da utilizzare con i dispositivi analogici o di associare oggetti contatto esistenti a un nuovo dispositivo. Per informazioni dettagliate, vedere le descrizioni relative ai parametri OU e DN in questo argomento.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsAnalogDevice** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Le autorizzazioni per l'esecuzione di questo cmdlet per siti o unità organizzative di Active Directory specifiche possono essere assegnate tramite il cmdlet **Grant-CsOUPermission**. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAnalogDevice"}

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
<td><p><em>AnalogFax</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare su True ($True) se il dispositivo analogico è un apparecchio fax. Impostare su False ($False) se il dispositivo non è un apparecchio fax.</p></td>
</tr>
<tr class="even">
<td><p><em>DN</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.ADObjectId</p></td>
<td><p>Consente di associare un oggetto contatto di Active Directory esistente al dispositivo analogico. Se si dispone di un oggetto contatto da associare a un dispositivo analogico, utilizzare il parametro DN seguito dal nome distinto del contatto, ad esempio -DN &quot;cn=Building 14 Lobby,dc=litwareinc,dc=com&quot;. Il comando avrà esito negativo se il contatto specificato non esiste.</p>
<p>Non è possibile utilizzare i parametri OU e DN nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Gateway</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Indirizzo IP del gateway PSTN che deve essere utilizzato dal dispositivo analogico.</p></td>
</tr>
<tr class="even">
<td><p><em>LineUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono del dispositivo analogico. L'URI (Uniform Resource Identifier) della linea deve essere specificato utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;, ad esempio TEL:+14255551297. L'eventuale numero di interno deve essere aggiunto alla fine dell'URI della linea, ad esempio: &quot;TEL:+14255551297;ext=51297&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>OU</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Nome distinto dell'unità organizzativa (OU) di Active Directory in cui deve essere posizionato l'oggetto contatto, ad esempio -OU &quot;ou=Redmond,dc=litwareinc,dc=com”.</p>
<p>Se si include il parametro OU, verrà creato un nuovo contatto nell'unità organizzativa specificata e al contatto verrà assegnato automaticamente un identificatore univoco globale (GUID) come nome comune. Di conseguenza, il nome dell'oggetto contatto sarà simile al seguente: {ce84964a-c4da-4622-ad34-c54ff3ed361f}.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del pool di registrazione in cui deve essere inserito l'oggetto contatto, ad esempio -RegistrarPool &quot;atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di configurare il nome visualizzato Active Directory del dispositivo analogico.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono visualizzato in Lync. La proprietà DisplayNumber può essere formattata nella modalità che si preferisce, ad esempio 1-800-555-1234; 1-(800)-555-1234; 1.800.555.1234 e così via.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce un oggetto che rappresenta il telefono delle aree comuni.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco (simile a un indirizzo di posta elettronica) che consente al dispositivo analogico di comunicare con dispositivi SIP come Lync. L'indirizzo SIP deve essere preceduto dal prefisso &quot;sip:&quot;, ad esempio sip:bldg14lobby@litwareinc.com.</p></td>
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

Nessuno. Il cmdlet **New-CsAnalogDevice** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsAnalogDevice** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsAnalogDevice](get-csanalogdevice.md)  
[Move-CsAnalogDevice](move-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

