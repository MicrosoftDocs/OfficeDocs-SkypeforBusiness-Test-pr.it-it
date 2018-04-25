---
title: New-CsUserReplicatorConfiguration
TOCTitle: New-CsUserReplicatorConfiguration
ms:assetid: eb4dee9e-9ba4-4726-8f7c-b355433ed594
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399059(v=OCS.15)
ms:contentKeyID: 49302382
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUserReplicatorConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione per User Replicator. Tale componente recupera periodicamente informazioni aggiornate sugli account utente da Attive Directory e quindi sincronizza le nuove informazioni con i dati degli utenti correnti archiviati da Lync Server. Questo cmdlet è specifico per l'utilizzo con Lync Online e non funzionerà con la versione locale di Lync Server.

## Sintassi

    New-CsUserReplicatorConfiguration -Identity <XdsIdentity> [-ADDomainNamingContextList <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-ReplicationCycleInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 crea una nuova raccolta di impostazioni di configurazione di User Replicator per il servizio Registrar:atl-cs-001.litwareinc.com. Poiché non sono specificati ulteriori parametri, la nuova raccolta utilizzerà i valori di User Replicator predefiniti.

    New-CsUserReplicatorConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com"

## ESEMPIO 2

Nell'esempio 2 viene anche creata una nuova raccolta di impostazioni di configurazione del componente User Replicator per il servizio Registrar:atl-cs-001.litwareinc.com. In questo caso, viene però aggiunto AdDomainNamingContextList insieme ai nomi distinti dei due domini con cui effettuare la sincronizzazione, ovvero fabrikam.com e contoso.com. Tale nuova raccolta di impostazioni di configurazione di User Replicator verrà configurata solo con questi due domini, anche se ve ne sono altri disponibili.

    New-CsUserReplicatorConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com" -ADDomaiNamingContextList @{Add="dc=fabrikam,dc=com","dc=contoso.com"}

## Descrizione dettagliata

Sebbene Lync Server gestisca il proprio database di account utente e i dati di tali account, Lync Server si basa comunque su Attive Directory come origine definitiva delle informazioni sugli utenti. Ad esempio, quando viene creato un nuovo account utente di Attive Directory, è necessario fornire le informazioni di base sull'account utente, ad esempio il nome visualizzato di Attive Directory. Quando un utente è abilitato per Lync Server, non è tuttavia necessario specificare un nuovo nome visualizzato, in quanto Lync Server utilizza il nome visualizzato già archiviato in Attive Directory.

Le informazioni relative agli account utente, incluso il nome visualizzato di Active Directory, sono soggette a cambiamenti nel tempo. Ad esempio, un utente di sesso femminile che si sposa cambia cognome e quindi può avere necessità di cambiare anche il proprio nome visualizzato. Per assicurarsi che il database di Lync Server e Active Directory rimangano sincronizzati, Lync Server deve comunicare regolarmente con Active Directory, recuperare gli aggiornamenti più recenti relativi agli account utente e modificare di conseguenza il proprio database degli utenti. Tale sincronizzazione tra Active Directory e Lync Server viene effettuata dal componente User Replicator.

Durante l'installazione di Lync Server, viene creato automaticamente un insieme globale di impostazioni di configurazione per User Replicator. Per impostazione predefinita, tali impostazioni vengono utilizzate per gestire User Replicator per l'intera organizzazione. La gestione di User Replicator consiste nell'identificare i domini con cui Lync Server deve eseguire la sincronizzazione, nonché nell'indicare la frequenza con cui User Replicator deve verificare la disponibilità di aggiornamenti degli account utente in Attive Directory. È inoltre possibile creare ulteriori raccolte nell'ambito del servizio, ma solo se si utilizza Lync Online.

Le nuove impostazioni di configurazione per User Replicator vengono create utilizzando il cmdlet **New-CsUserReplicatorConfiguration**. Tali impostazioni possono essere create solo nell'ambito del servizio ed esclusivamente per Lync Online. Non è possibile creare nuove impostazioni di User Replicator per la versione locale di Lync Server.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsUserReplicatorConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUserReplicatorConfiguration"}

``` 
```

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione di User Replicator da creare. È possibile creare impostazioni solo con ambito servizio e unicamente per il servizio Registrar. Di conseguenza, le nuove impostazioni dovranno disporre di un parametro Identity analogo al seguente: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;.</p>
<p>Notare che questo si applica solo a Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>ADDomainNamingContextList</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Nomi distinti dei domini di Active Directory con cui User Replicator deve effettuare la sincronizzazione. Ad esempio, per aggiungere un dominio all'elenco, utilizzare una sintassi analoga alla seguente:</p>
<p>-ADDomainNamingContextList @{Add=&quot;dc=fabrikam,dc=com&quot;}</p>
<p>È possibile aggiungere più di un nome di dominio quando viene chiamato il cmdlet <strong>New-CsUserReplicatorConfiguration</strong>. A tale scopo, è sufficiente separare i nomi dei domini con una virgola:</p>
<p>-ADDomainNamingContextList @{Add=&quot;dc=fabrikam,dc=com&quot;,&quot;dc=contoso,dc=com&quot;}</p>
<p></p>
<p>Se la proprietà viene impostata su un valore null, User Replicator individuerà ed effettuerà la sincronizzazione con tutti i domini disponibili. Se la proprietà non è impostata su null, User Replicator effettuerà la sincronizzazione solo con i domini specificati in ADDomainNamingContextList.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>ReplicationCycleInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica per quanto tempo User Replicator deve attendere prima di verificare la disponibilità di eventuali aggiornamenti degli account utente in Active Directory. Come intervallo per il ciclo di replica è possibile specificare qualsiasi valore compreso tra 1 secondo e 23 ore, 59 minuti e 59 secondi. Il valore predefinito è 1 minuto. L'intervallo deve essere espresso utilizzando il formato hh:mm:ss (ore, minuti, secondi). Ad esempio, la seguente sintassi consente di impostare l'intervallo di tempo su 1 ora e 15 minuti: -ReplicationCycleInterval 01:15:00.</p></td>
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

Nessuno. Il cmdlet **New-CsUserReplicatorConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsUserReplicatorConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)  
[Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)  
[Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

