---
title: Set-CsUserReplicatorConfiguration
TOCTitle: Set-CsUserReplicatorConfiguration
ms:assetid: 7164960f-8e88-4c8d-9a12-1814aa2b9047
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398540(v=OCS.15)
ms:contentKeyID: 49300943
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserReplicatorConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione di User Replicator. User Replicator recupera periodicamente informazioni aggiornate sugli account utente da Servizi di dominio Active Directory e quindi le sincronizza con i dati utente correnti archiviati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUserReplicatorConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUserReplicatorConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ADDomainNamingContextList <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReplicationCycleInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il valore di ReplicationCycleInterval delle impostazioni globali di User Replicator viene impostato su cinque minuti (00 ore: 05 minuti: 00 secondi).

    Set-CsUserReplicatorConfiguration -Identity global -ReplicationCycleInterval "00:05:00"

## ESEMPIO 2

Il comando mostrato nell'esempio 2 annulla il valore della proprietà ADDomainNamingContextList. L'attività viene eseguita aggiungendo il parametro ADDomainNamingContextList e impostando il valore del parametro su null. Impostando questo valore su null, User Replicator automaticamente individuerà tutti i domini disponibili ed effettuerà la sincronizzazione in base a essi.

    Set-CsUserReplicatorConfiguration -Identity global -ADDomainNamingContextList $Null

## ESEMPIO 3

Nell'esempio 3 viene aggiunto un ulteriore nome alla proprietà ADDomainNamingContextList delle impostazioni globali di User Replicator. A questo scopo, viene utilizzata la sintassi @{Add=} insieme al nome distinto del dominio da aggiungere. Quando il comando viene eseguito, fabrikam.com viene aggiunto all'elenco di nomi di dominio. Per configurare le impostazioni globali in modo tale che nell'elenco sia presente solo fabrikam.com, utilizzare la sintassi seguente:

\-ADDomainNamingContextList @{Replace="dc=fabrikam,dc=com"}

Se la proprietà AdDomainNamingContextList è impostata su un valore diverso da null, User Replicator effettuerà la sincronizzazione solo con i domini elencati nel valore della proprietà. Questo comportamento sarà valido anche se sono presenti altri domini nella distribuzione.

    Set-CsUserReplicatorConfiguration -Identity global -ADDomainNamingContextList @{Add="dc=fabrikam,dc=com"}

## ESEMPIO 4

Nell'esempio 4 il dominio fabrikam.com viene rimosso dalla proprietà ADDomainNamingContextList delle impostazioni di configurazione globali di User Replicator. A tale scopo, viene utilizzata la sintassi @{Remove=} insieme al nome distinto (DN) del dominio (dc=fabrikam,dc=com).

    Set-CsUserReplicatorConfiguration -Identity global -ADDomainNamingContextList @{Remove="dc=fabrikam,dc=com"}

## Descrizione dettagliata

Anche se Lync Server dispone di un proprio database degli account utente e dei relativi dati, Lync Server si basa comunque su Servizi di dominio Active Directory come origine definitiva delle informazioni utente. Quando ad esempio viene creato un nuovo account utente di Active Directory, è necessario fornire le informazioni di base a esso relative, tra cui il nome visualizzato di Active Directory. Se però un utente è abilitato per Lync Server, non è necessario specificare un nuovo nome visualizzato, in quanto in Lync Server viene utilizzato il nome visualizzato già archiviato in Servizi di dominio Active Directory.

Le informazioni relative agli account utente, incluso il nome visualizzato Active Directory, sono soggette a modifiche nel tempo. Un utente che contrae matrimonio ad esempio può cambiare cognome e dover pertanto cambiare anche il nome visualizzato. Affinché il database di Lync Server e Servizi di dominio Active Directory rimangano sincronizzati, Lync Server deve comunicare regolarmente con Servizi di dominio Active Directory, recuperare gli aggiornamenti più recenti degli account utente e quindi modificare di conseguenza il database degli utenti di Lync Server. La sincronizzazione tra Servizi di dominio Active Directory e Lync Server viene eseguita da User Replicator.

Quando si installa Lync Server, viene automaticamente creato un insieme globale di impostazioni di configurazione di User Replicator. Per impostazione predefinita, queste impostazioni vengono utilizzate per gestire User Replicator a livello di organizzazione. La gestione di User Replicator consiste nell'identificare i domini con cui deve sincronizzarsi Lync Server e nell'indicare la frequenza con cui User Replicator deve ricercare in Servizi di dominio Active Directory gli aggiornamenti degli account utente. Per impostazione predefinita, User Replicator individua tutti i domini disponibili ed esegue la sincronizzazione in base a essi. Utilizzando la proprietà AdDomainNamingContextList è tuttavia possibile limitare la sincronizzazione a un insieme specifico di domini, ovvero i domini specificati nella proprietà AdDomainNamingContextList.

È inoltre possibile creare ulteriori raccolte nell'ambito del servizio, ma solo se si utilizza Lync Online.

Il cmdlet **Set-CsUserReplicatorConfiguration** consente di modificare qualsiasi impostazione di User Replicator attualmente in uso nell'organizzazione. È possibile utilizzare questo cmdlet per aggiungere o rimuovere domini dall'elenco di domini con cui User Replicator deve eseguire la sincronizzazione, nonché per modificare l'intervallo di tempo tra i cicli di replica.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsUserReplicatorConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserReplicatorConfiguration"}

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
<td><p><em>ADDomainNamingContextList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Nomi distinti dei domini di Active Directory con cui User Replicator deve effettuare la sincronizzazione. Ad esempio, per aggiungere un dominio all'elenco, utilizzare una sintassi analoga alla seguente:</p>
<p>-ADDomainNamingContextList @{Add=&quot;dc=fabrikam,dc=com&quot;}</p>
<p>Se la proprietà viene impostata su un valore null, User Replicator individuerà ed effettuerà la sincronizzazione con tutti i domini disponibili. Se questa proprietà non è impostata su null, User Replicator effettuerà la sincronizzazione solo con i domini specificati in ADDomainNamingContextList.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione di User Replicator da modificare. Per modificare le impostazioni globali, utilizzare la sintassi seguente: -Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto UserReplicatorConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicationCycleInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Rappresenta il tempo di attesa di User Replicator prima di verificare la disponibilità di eventuali aggiornamenti degli account utente in Servizi di dominio Active Directory. L'intervallo del ciclo di replica può corrispondere a qualsiasi valore temporale compreso tra 1 secondo e 23 ore, 59 minuti e 59 secondi. Il valore predefinito è 1 minuto. L'intervallo deve essere espresso utilizzando il formato hh:mm:ss (ore, minuti, secondi). Ad esempio, la seguente sintassi consente di impostare l'intervallo di tempo su 1 ora e 15 minuti:</p>
<p>-ReplicationCycleInterval 01:15:00</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration. Il cmdlet **Set-CsUserReplicatorConfiguration** accetta l'input da pipeline dell'oggetto di configurazione di User Replicator.

## Tipi restituiti

Il cmdlet **Set-CsUserReplicatorConfiguration** non restituisce alcun oggetto o valore. Modifica invece l'istanza globale (l'unica istanza di questo tipo) dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)  
[New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)  
[Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)

