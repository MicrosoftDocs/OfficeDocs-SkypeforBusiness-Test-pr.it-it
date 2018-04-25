---
title: Enable-CsMeetingRoom
TOCTitle: Enable-CsMeetingRoom
ms:assetid: 88af3267-80c5-46c0-aaef-135843b42a04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205062(v=OCS.15)
ms:contentKeyID: 49301226
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsMeetingRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita una sala riunioni di Lync Server 2013. Per sala riunioni si intende un dispositivo per conferenze progettato per gestire scenari di collaborazione e videoconferenza in sale conferenze di piccole dimensioni. Per abilitare una sala riunioni, è necessario innanzitutto creare un account utente di Active Directory che rappresenterà tale sistema. Benché gli oggetti sala riunioni siano basati su account utente, non verranno visualizzati quando si esegue il cmdlet **Get-CsUser**. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Enable-CsMeetingRoom -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-HostingProviderProxyFqdn <Fqdn>] [-OriginatorSid <SecurityIdentifier>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-RegistrarPool <Fqdn>] [-SipAddress <String>] [-SipAddressType <FirstLastName | EmailAddress | UserPrincipalName | SAMAccountName | None>] [-SipDomain <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 abilita la sala riunioni con l'identità (in questo caso, il nome visualizzato di Active Directory) "Redmond Meeting room". La nuova sala riunioni viene inserita nel pool di registrazione arl-cs-001.litwareinc.com e le viene assegnato l'indirizzo SIP sip:RedmondMeetingRoom@litwareinc.com.

    Enable-CsMeetingRoom -Identity "Redmond Meeting room" -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddress "sip:RedmondMeetingRoom@litwareinc.com"

## Esempio 2

Nell'esempio 2 vengono abilitate tutte le sale riunioni trovate nell'unità organizzativa MeetingsRoom. In altri termini, questo comando abilita tutti gli account utente inclusi nell'unità organizzativa MeetingsRoom. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsAdUser** insieme al parametro OU. Il valore di parametro "OU=MeetingRooms,dc=litwareinc,dc=com" restituisce solo i dati relativi agli account utente trovati nell'unità organizzativa MeetingRooms. Tali account vengono quindi inviati tramite pipe al cmdlet **Enable-CsMeetingRoom**, che recupera ogni account della raccolta e lo abilita come sala riunioni. Ogni nuova sala riunioni verrà inserita nel pool di registrazione atl-cs-001.litwareinc.com e avrà un indirizzo SIP costituito dal parametro SamAccountName dell'account (ad esempio room14) e dal dominio SIP litwareinc.com.

    Get-CsAdUser -OU "OU=MeetingRooms,dc=litwareinc,dc=com" | Enable-CsMeetingRoom -RegistrarPool "atl-cs-001.litwareinc.com" -SipAddressType "SamAccountName" -SipDomain "litwareinc.com"

## Descrizione dettagliata

In Lync Server le sale riunioni sono accessori autonomi per computer che vengono installati nelle sale conferenze e offrono funzionalità avanzate per riunioni, ad esempio:

  - Accesso alle riunioni con un singolo tocco

  - Raccolta video multiview

  - Lavagne abilitate per il tocco sulla parte anteriore dello schermo della sala riunioni

  - Integrazione del calendario per l'accesso alle riunioni pianificate

  - Condivisione e scambio di contenuto

Per gestire questi nuovi dispositivi endpoint, è necessario inoltre creare e abilitare un account di cassetta postale per la risorsa Microsoft Exchange Server 2013 per il dispositivo e quindi abilitarlo per Lync Server 2013. Si noti che per Lync Server non sono disponibili cmdlet per la creazione o la rimozione di sale riunioni. È necessario invece utilizzare il cmdlet **Enable-CsMeetingRoom** per abilitare le sale riunioni e il cmdlet [Disable-CsMeetingRoom](disable-csmeetingroom.md) per disabilitarle. Per poter abilitare la sala riunioni, l'account per la risorsa deve essere già presente. Disabilitando una sala riunioni viene solo rimossa la sala riunioni dalla raccolta di sale riunioni, non viene eliminato l'account di cassetta postale per la risorsa.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Enable-CsMeetingRoom"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Enable-CsMeetingRoom** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indica l'identità dell'account utente da configurare come sala riunioni. Le identità in genere vengono specificate utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente come dominio\accesso (ad esempio, litwareinc\room14) e 4) il nome visualizzato di Active Directory dell'utente (ad esempio, Room 14).</p>
<p>È inoltre possibile fare riferimento a un account utente utilizzando il nome distinto di Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con il valore di stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per abilitare una sala riunioni. Per connettersi a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-dc-001) o dal nome di dominio completo (FQDN) (ad esempio, atl-dc-001.litwareinc.com).</p></td>
</tr>
<tr class="even">
<td><p><em>HostingProviderProxyFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del server proxy provider di hosting. Questo parametro viene utilizzato solo con Microsoft Lync Online.</p></td>
</tr>
<tr class="odd">
<td><p><em>OriginatorSid</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Security.Principal.SecurityIdentifier</p></td>
<td><p>Valore dell'attributo msRTCSIP-OriginatorSID. Questo attributo di Active Directory viene utilizzato per abilitare Single Sign-On. Questo parametro viene utilizzato solo con Microsoft Lync Online.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite pipeline un oggetto sala riunioni che rappresenta la sala riunioni che si sta abilitando per Lync Server. Per impostazione predefinita, il cmdlet <strong>Enable-CsMeetingRoom</strong> non passa alcun oggetto tramite pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome del pool di proxy. Questo parametro viene utilizzato solo con Microsoft Lync Online.</p></td>
</tr>
<tr class="even">
<td><p><em>RegistrarPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Indica il pool di registrazione in cui verrà inserito l'account di Lync Server della sala riunioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di assegnare alla sala riunioni uno specifico indirizzo SIP. Quando si specifica l'indirizzo SIP, è necessario farlo precedere da &quot;sip:&quot;. In pratica, il valore fornito al parametro SipAddress deve essere simile al seguente:</p>
<p>sip:room14@litwareinc.com</p>
<p>Il parametro SipAddress non deve essere utilizzato se si utilizza il parametro SipAddressType per fare in modo che Lync Server generi automaticamente un indirizzo SIP per la sala riunioni.</p>
<p>Il parametro SipAddress non può essere utilizzato se si tenta di abilitare più sale riunioni contemporaneamente. È invece possibile generare automaticamente gli indirizzi SIP per tali sale utilizzando il parametro SipAddressType.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddressType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.Cmdlets.AddressType</p></td>
<td><p>Indica a Lync Server di generare automaticamente un indirizzo SIP per la nuova sala riunioni. Affinché Lync Server generi automaticamente l'indirizzo SIP, è necessario includere il parametro SipAddressType e utilizzare uno dei valori seguenti:</p>
<p>* FirstLastName. L'indirizzo SIP corrisponde al nome dell'utente, seguito da un punto, dal cognome dell'utente e dal dominio SIP. Ad esempio, per la sala 14 l'indirizzo SIP diventa: Room.14@litwareinc.com. Se si utilizza questo tipo di indirizzo, è necessario includere anche il parametro SipDomain.</p>
<p>* EmailAddress. L'indirizzo di posta elettronica dell'utente (definito in Active Directory) viene utilizzato come indirizzo SIP.UserPrincipalName. Come indirizzo SIP viene utilizzato l'UPN dell'utente.</p>
<p></p>
<p>* SamAccountName. L'indirizzo SIP corrisponde al SamAccountName (nome di accesso) dell'utente seguito dal dominio SIP. Ad esempio, per l'utente con SamAccountName room 14 l'indirizzo SIP diventa: room14@litwareinc.com. Se si utilizza questo tipo di indirizzo, è necessario includere anche il parametro SipDomain.</p>
<p>Il parametro SipAddressType non è necessario se si utilizza il parametro SIPAddress e si assegna esplicitamente all'utente un indirizzo SIP.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipDomain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Dominio SIP per la sala riunioni da abilitare. Questo parametro è obbligatorio se si utilizza il parametro SIPAddressType per fare in modo che Lync Server generi automaticamente un indirizzo SIP per l'utente e se gli indirizzi SIP sono basati sul SamAccountName o sul nome e cognome dell'utente. Questo parametro non è necessario se l'indirizzo SIP è basato sull'indirizzo di posta elettronica dell'utente o sull'UPN perché il nome del dominio è già incluso nei valori di tali attributi.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Enable-CsMeetingRoom** accetta gli input tramite pipeline dei valori stringa che rappresentano l'identità di un account utente abilitato per Lync Server. Il cmdlet accetta anche istanze di oggetti utente di Active Directory inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Enable-CsMeetingRoom** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom.

## Vedere anche

#### Ulteriori risorse

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

