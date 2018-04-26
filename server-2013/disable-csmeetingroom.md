---
title: Disable-CsMeetingRoom
TOCTitle: Disable-CsMeetingRoom
ms:assetid: 1bce6b58-484f-4e59-a259-aa315d37d9b0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204723(v=OCS.15)
ms:contentKeyID: 49299848
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsMeetingRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Disabilita una sala riunioni di Lync Server 2013. Una sala riunioni è un dispositivo per conferenze progettato per gestire scenari di collaborazione e videoconferenze in piccole sale conferenze. Quando si disabilita un oggetto sala riunione, si rimuovono tutti gli attributi di Active Directory specifici di Lync Server assegnati all'account utente che rappresenta la sala riunioni. L'account utente di Active Directory tuttavia non viene eliminato. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Disable-CsMeetingRoom -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 disabilita la sala riunioni sip:RedmondMeetingRoom@litwareinc.com.

    Disable-CsMeetingRoom -Identity "sip:RedmondMeetingRoom@litwareinc.com"

## Esempio 2

Nell'esempio 2 vengono disabilitate tutte le sale riunioni attualmente in uso nell'organizzazione. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsMeetingRoom** per recuperare una raccolta di tutte le sale riunioni. La raccolta viene quindi inviata tramite pipe al cmdlet **Disable-CsMeetingRoom**, che disabilita ogni sala riunioni della raccolta.

    Get-CsMeetingRoom | Disable-CsMeetingRoom

## Descrizione dettagliata

In Lync Server le sale riunioni sono accessori autonomi per computer che vengono installati nelle sale conferenze e offrono funzionalità avanzate per riunioni, ad esempio:

  - Accesso alle riunioni con un singolo tocco

  - Raccolta video multiview

  - Lavagne abilitate per il tocco sulla parte anteriore dello schermo della sala riunioni

  - Integrazione del calendario per l'accesso alle riunioni pianificate

  - Condivisione e scambio di contenuto

Per gestire questi nuovi dispositivi endpoint, è necessario tra l'altro creare e abilitare un account di cassetta postale per la risorsa di Microsoft Exchange Server 2013 per il dispositivo e quindi abilitare tale account per Lync Server 2013. Si noti che per Lync Server non sono disponibili cmdlet per la creazione o la rimozione di sale riunioni. È necessario invece utilizzare il cmdlet [Enable-CsMeetingRoom](enable-csmeetingroom.md) per abilitare le sale riunioni e il cmdlet **Disable-CsMeetingRoom** per disabilitarle. Per poter abilitare la sala riunioni, l'account per la risorsa deve essere già presente. Disabilitando una sala riunioni viene solo rimossa la sala riunioni dalla raccolta di sale riunioni, non viene eliminato l'account di cassetta postale per la risorsa.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Disable-CsMeetingRoom"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Disable-CsMeetingRoom** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indica l'identità dell'account utente da configurare come sala riunioni. Le identità utente vengono in genere specificate utilizzando uno dei quattro formati seguenti: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio litwareinc\kenmyer) e 4) il nome visualizzato di Active Directory dell'utente (ad esempio Ken Myer).</p>
<p>È inoltre possibile fare riferimento all'account utente utilizzando il nome distinto dell'utente in Active Directory.</p>
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
<td><p>Consente la connessione al controller di dominio specifico per disabilitare una sala riunioni. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome del computer, ad esempio atl-dc-001, oppure dal relativo nome di dominio completo (FQDN), ad esempio atl-dc-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare attraverso la pipeline un oggetto sala riunioni che rappresenta la sala riunioni da disabilitare. Per impostazione predefinita, il cmdlet <strong>Disable-CsMeetingRoom</strong> non passa oggetti attraverso la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Disable-CsMeetingRoom** accetta le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Disable-CsMeetingRoom** invece elimina l'istanza dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom.

## Vedere anche

#### Ulteriori risorse

[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Move-CsMeetingRoom](move-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

