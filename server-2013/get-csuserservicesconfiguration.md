---
title: Get-CsUserServicesConfiguration
TOCTitle: Get-CsUserServicesConfiguration
ms:assetid: 07884f7a-d9f7-4a3f-a5ef-7f4ba71c2769
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398133(v=OCS.15)
ms:contentKeyID: 49299581
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserServicesConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle impostazioni di configurazione dei servizi utente in uso nell'organizzazione. Il servizio Servizi utente consente di conservare le informazioni sulla presenza e gestire le conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUserServicesConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUserServicesConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce una raccolta di tutte le impostazioni di configurazione di Servizi utente attualmente in uso nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsUserServicesConfiguration** senza alcun parametro aggiuntivo.

    Get-CsUserServicesConfiguration

## ESEMPIO 2

Con l'esempio 2 viene restituita una sola raccolta di impostazioni di configurazione di Servizi utente, quella con identità site:Redmond. Poiché le identità devono essere univoche, il comando non restituirà mai più di un elemento.

    Get-CsUserServicesConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene restituita una raccolta di tutte le impostazioni di configurazione di Servizi utente applicate nell'ambito del servizio. A tale scopo, viene chiamato il cmdlet **Get-CsUserServicesConfiguration** con il parametro -Filter. Con il valore di filtro "service:\*" vengono restituite solo le impostazioni in cui l'identità inizia con i caratteri "service:". Per definizione, si tratta delle impostazioni configurate nell'ambito del servizio.

    Get-CsUserServicesConfiguration -Filter "service:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le impostazioni di configurazione di Servizi utente che consentono agli utenti di disporre di più di 250 contatti. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUserServicesConfiguration** senza parametri aggiuntivi per restituire una raccolta di tutte le impostazioni di configurazione di Servizi utente attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà MaxContacts è maggiore di 250.

    Get-CsUserServicesConfiguration | Where-Object {$_.MaxContacts -gt 250}

## ESEMPIO 5

Nell'esempio 5 vengono riportate informazioni per le impostazioni di configurazione di Servizi utente in cui il periodo di tolleranza per gli utenti anonimi è superiore a 10 minuti. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsUserServicesConfiguration** senza parametri aggiuntivi per restituire una raccolta di tutte le impostazioni di configurazione di Servizi utente in uso nell'organizzazione. La raccolta restituita viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà AnonymousUserGracePeriod è maggiore di 10 minuti (00 ore: 10 minuti: 00 secondi).

    Get-CsUserServicesConfiguration | Where-Object {$_.AnonymousUserGracePeriod -gt "00:10:00"}

## Descrizione dettagliata

Lync Server si basa sul servizio Servizi utente per gestire le informazioni sulla presenza degli utenti, le riunioni e le conferenze. I cmdlet **CsUserServicesConfiguration** vengono a loro volta utilizzati per gestire le impostazioni di Servizi utente nell'ambito del servizio, del sito e globale. L'unico servizio che può ospitare le impostazioni di configurazione di Servizi utente è il servizio Servizi utente stesso. Queste impostazioni consentono ad esempio di determinare il numero di contatti massimo per un utente, il numero di riunioni che un utente può pianificare in un determinato momento e la durata del periodo di attività di una riunione.

Il cmdlet **Get-CsUserServicesConfiguration** offre agli amministratori un mezzo per recuperare informazioni su una o su tutte le impostazioni di configurazione del servizio Servizi utente attualmente in uso.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsUserServicesConfiguration** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserServicesConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per il recupero di una o più raccolte di impostazioni di configurazione di Servizi utente. Ad esempio, per restituire tutte le impostazioni configurate nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per restituire tutte le impostazioni configurate nell'ambito del servizio, utilizzare la seguente sintassi: -Filter &quot;service:*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per le impostazioni di configurazione di Servizi utente da restituire. Per restituire le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per restituire le impostazioni configurate nell'ambito del sito, utilizzare la sintassi: -Identity site:Redmond. Per restituire le impostazioni a livello del servizio, utilizzare una sintassi simile alla seguente: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>Se questo parametro viene omesso, il cmdlet <strong>Get-CsUserServicesConfiguration</strong> restituisce tutte le impostazioni di configurazione di Servizi utente attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione di Servizi utente dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsUserServicesConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsUserServicesConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsUserServicesConfiguration](new-csuserservicesconfiguration.md)  
[Remove-CsUserServicesConfiguration](remove-csuserservicesconfiguration.md)  
[Set-CsUserServicesConfiguration](set-csuserservicesconfiguration.md)

