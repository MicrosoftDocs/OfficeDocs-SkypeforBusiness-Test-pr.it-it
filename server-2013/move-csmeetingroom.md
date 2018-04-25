---
title: Move-CsMeetingRoom
TOCTitle: Move-CsMeetingRoom
ms:assetid: 4ea6b8bd-b134-4453-9ae4-6118330a62ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204889(v=OCS.15)
ms:contentKeyID: 49300513
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsMeetingRoom

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sposta un oggetto sala riunioni di Lync Server 2013 da un pool di registrazione a un altro. Una sala riunioni è un dispositivo per conferenze progettato per gestire scenari di collaborazione e videoconferenze in piccole sale conferenze. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Move-CsMeetingRoom -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando mostrato nell'esempio 1 sposta la sala riunioni con nome visualizzato "Room 14" nel pool atl-cs-001.litwareinc.com.

    Move-CsMeetingRoom -Target "atl-cs-001.litwareinc.com" -Identity "Room 14"

## Esempio 2

Nell'esempio 2 tutte le sale riunioni dell'organizzazione vengono spostate nel pool atl-cs-001.litwareinc.com. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsMeetingRoom** senza parametri, in modo da restituire una raccolta di tutte le sale riunioni configurate per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Move-CsMeetingRoom**, che sposta ogni sala riunioni della raccolta nel nuovo pool.

    Get-CsMeetingRoom | Move-CsMeetingRoom -Target "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

In Lync Server le sale riunioni sono accessori autonomi per computer che vengono installati nelle sale conferenze e offrono funzionalità avanzate per riunioni, ad esempio:

  - Accesso alle riunioni con un singolo tocco

  - Raccolta video multiview

  - Lavagne abilitate per il tocco sulla parte anteriore dello schermo della sala riunioni

  - Integrazione del calendario per l'accesso alle riunioni pianificate

  - Condivisione e scambio di contenuto

Per gestire questi nuovi dispositivi endpoint, è necessario inoltre creare e abilitare un account di cassetta postale per la risorsa Microsoft Exchange Server 2013 per il dispositivo e quindi abilitarlo per Lync Server 2013. Si noti che per Lync Server non sono disponibili cmdlet per la creazione o la rimozione di sale riunioni. È necessario invece utilizzare il cmdlet [Enable-CsMeetingRoom](enable-csmeetingroom.md) per abilitare le sale riunioni e il cmdlet [Disable-CsMeetingRoom](disable-csmeetingroom.md) per disabilitarle. Per poter abilitare la sala riunioni, l'account per la risorsa deve essere già presente. Disabilitando una sala riunioni viene solo rimossa la sala riunioni dalla raccolta di sale riunioni, non viene eliminato l'account di cassetta postale per la risorsa.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsMeetingRoom"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Move-CsMeetingRoom** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Indica l'identità della sala riunioni da spostare. Le sale riunioni possono essere specificate utilizzando uno dei seguenti quattro formati: 1) l'indirizzo SIP della sala, 2) il nome dell'entità utente (UPN) della sala, 3) il nome del dominio e il nome di accesso della sala nel formato dominio\accesso (ad esempio litwareinc\kenmyer) e 4) il nome visualizzato di Active Directory della sala (ad esempio Sala riunioni principale). Alle identità utente è anche possibile fare riferimento utilizzando il nome distinto Active Directory della sala.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (ad esempio atl-cs-001.litwareinc.com) del pool di registrazione in cui deve essere spostata la sala riunioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specifico per spostare una sala riunioni. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome del computer, ad esempio atl-dc-001, oppure dal relativo nome di dominio completo (FQDN), ad esempio atl-dc-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro indica al cmdlet <strong>Move-CsMeetingRoom</strong> di ignorare tutti gli errori che possono verificarsi durante l'operazione di spostamento. Come regola generale, è consigliabile evitare di utilizzare il parametro Force, a meno che non sia assolutamente necessario.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro indica al computer di ignorare gli eventuali errori che possono verificarsi con il database back-end e di tentare comunque di spostare la sala riunioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare tramite la pipeline un oggetto sala riunioni che rappresenta la sala riunioni da spostare. Per impostazione predefinita, il cmdlet <strong>Move-CsMeetingRoom</strong> non passa oggetti tramite pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro non viene utilizzato con la versione locale di Lync Server 2013.</p></td>
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

Il cmdlet Moves-CsMeetingRoom accetta le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADMeetingRoom inviate tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Disable-CsMeetingRoom](disable-csmeetingroom.md)  
[Enable-CsMeetingRoom](enable-csmeetingroom.md)  
[Get-CsMeetingRoom](get-csmeetingroom.md)  
[Set-CsMeetingRoom](set-csmeetingroom.md)

