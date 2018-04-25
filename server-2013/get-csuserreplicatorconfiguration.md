---
title: Get-CsUserReplicatorConfiguration
TOCTitle: Get-CsUserReplicatorConfiguration
ms:assetid: 7318ae92-e07b-4817-9ec1-be9c7f35aa26
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398548(v=OCS.15)
ms:contentKeyID: 49300968
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserReplicatorConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione di User Replicator attualmente in uso nell'organizzazione. User Replicator recupera periodicamente le informazioni aggiornate sugli account utente da Active Directory. Queste nuove informazioni vengono quindi sincronizzate con i dati utente correnti, archiviati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUserReplicatorConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUserReplicatorConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono restituite le informazioni su tutte le impostazioni di configurazione di User Replicator attualmente in uso nell'organizzazione.

    Get-CsUserReplicatorConfiguration

## Descrizione dettagliata

Sebbene Lync Server utilizzi un proprio database degli account utente e dei relativi dati, Lync Server si basa ancora su Active Directory come origine definitiva delle informazioni sugli utenti. Ad esempio, quando viene creato un nuovo account utente di Active Directory, è necessario fornire le informazioni di base a esso relative, ad esempio il nome visualizzato di Active Directory. Se però un utente è abilitato per Lync Server, non è necessario specificare un nuovo nome visualizzato per l'utente perché Lync Server utilizza il nome visualizzato già archiviato in Servizi di dominio Active Directory.

Naturalmente, le informazioni sull'account utente (incluso il nome visualizzato in Active Directory) sono soggette a modifiche nel tempo. Ad esempio, un utente di sesso femminile dopo il matrimonio potrebbe cambiare cognome e quindi anche il nome visualizzato. Per garantire che il database di Lync Server e Active Directory rimangano sincronizzati, Lync Server deve comunicare regolarmente con Active Directory, recuperare gli aggiornamenti più recenti degli account utente e modificare di conseguenza il proprio database degli utenti. La sincronizzazione tra Active Directory e Lync Server viene effettuata dal componente User Replicator.

Durante l'installazione di Lync Server viene automaticamente creato un set globale di impostazioni di configurazione per User Replicator. Per impostazione predefinita, tali impostazioni vengono utilizzate per la gestione di User Replicator a livello di organizzazione. La gestione di User Replicator consiste nell'identificazione dei domini con cui Lync Server deve eseguire la sincronizzazione, nonché nell'indicazione della frequenza in base alla quale User Replicator verifica la disponibilità degli aggiornamenti per gli account utente in Active Directory. Per impostazione predefinita, User Replicator individua tutti i domini disponibili ed effettua la sincronizzazione con essi. Tuttavia, utilizzando la proprietà AdDomainNamingContextList è possibile limitare la sincronizzazione a un set specifico di domini, quelli contenuti nella proprietà AdDomainNamingContextList.

Se si utilizza Lync Server, è inoltre possibile utilizzare i cmdlet CsUserReplicatorConfiguration per creare e gestire le impostazioni di configurazione nell'ambito del servizio. Con la versione locale di Lync Server, è tuttavia necessario limitarsi a una singola raccolta di impostazioni di configurazione assegnate all'ambito globale.

Il cmdlet **Get-CsUserReplicatorConfiguration** consente agli amministratori di restituire informazioni su tutte le impostazioni di User Replicator attualmente in uso nella loro organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsUserReplicatorConfiguration** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserReplicatorConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare la raccolta (o le raccolte) di impostazioni di configurazione di User Replicator da restituire. Ad esempio, questo comando restituisce tutte le impostazioni configurate nell'ambito del servizio: -Filter &quot;service:*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione di User Replicator da restituire. Per restituire le impostazioni nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;. Si noti che le impostazioni nell'ambito del servizio sono disponibili solo se si esegue Lync Online. Per restituire le impostazioni globali, utilizzare la sintassi seguente: -Identity global. Se questo parametro non viene specificato, vengono restituite tutte le impostazioni di configurazione di User Replicator attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione di User Replicator dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsUserReplicatorConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsUserReplicatorConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserReplicator.UserReplicatorConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)  
[Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)  
[Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

