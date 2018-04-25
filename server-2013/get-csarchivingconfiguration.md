---
title: Get-CsArchivingConfiguration
TOCTitle: Get-CsArchivingConfiguration
ms:assetid: e4951b81-2738-4cc2-87be-f8ee79da6c09
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399012(v=OCS.15)
ms:contentKeyID: 49302267
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsArchivingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su come (oppure se) le sessioni di messaggistica istantanea vengono archiviate nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsArchivingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsArchivingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituita una raccolta di tutte le impostazioni di configurazione di archiviazione in uso nell'organizzazione.

    Get-CsArchivingConfiguration

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il parametro Identity per limitare la raccolta restituita di impostazioni di configurazione dell'archiviazione alle impostazioni con valore Identity site:Redmond.

    Get-CsArchivingConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per limitare la raccolta restituita di impostazioni di configurazione dell'archiviazione alle impostazioni configurate nell'ambito del sito. Il valore site:\* del parametro limita gli elementi restituiti a quelli il cui valore Identity inizia con il valore stringa "site:".

    Get-CsArchivingConfiguration -Filter site:*

## ESEMPIO 4

In questo esempio viene utilizzato il cmdlet **Get-CsArchivingConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione di archiviazione abilitate per l'uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsArchivingConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione dell'archiviazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro per limitare i dati restituiti alle raccolte in cui la proprietà EnableArchiving non è uguale a "None". Se EnableArchiving è impostata su "None", l'archiviazione è stata disabilitata. Se la proprietà è impostata su qualsiasi altro valore ("IMOnly" o "ImAndWebConf"), l'archiviazione è stata abilitata.

    Get-CsArchivingConfiguration | Where-Object {$_.EnableArchiving -ne "None"}

## Descrizione dettagliata

Per molte organizzazioni è utile conservare una trascrizione di tutte le sessioni di messaggistica istantanea eseguite dai propri utenti (o da un sottoinsieme di utenti selezionati). Altre organizzazioni sono obbligate a detenere trascrizioni del genere. Ad esempio, molte organizzazioni che operano nel settore finanziario sono obbligate per legge a detenere copie di tutte le proprie comunicazioni elettroniche.

Lync Server offre grande flessibilità nell'archiviazione di sessioni di messaggistica istantanea e conferenze Web. Se è stato distribuito il server di archiviazione, sarà possibile utilizzare i diversi cmdlet **CsArchivingConfiguration** per abilitare e disabilitare l'archiviazione dei messaggi istantanei e per gestire il database di archiviazione. Se l'archiviazione non dovesse riuscire, è inoltre possibile sospendere la messaggistica istantanea. Questo consente di conservare un record di tutte le comunicazioni elettroniche.

Per archiviare sessioni di messaggistica istantanea, è necessario configurare almeno un server di archiviazione. Una volta configurato il server di archiviazione, è necessario eseguire due passaggi ulteriori. È innanzitutto necessario abilitare l'archiviazione nell'ambito appropriato. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet **Set-CsArchivingConfiguration**. L'ambito potrebbe essere globale. Tuttavia, è possibile configurare impostazioni di archiviazione personalizzate per siti diversi.

In secondo luogo, è necessario utilizzare i criteri di archiviazione per indicare gli utenti le cui sessioni di messaggistica istantanea verranno archiviate. Cosa succede se si abilita l'archiviazione ma non si assegna un criterio agli utenti che specifichi che le sessioni di messaggistica istantanea devono essere archiviate? Non succede niente: le sessioni di messaggistica istantanea non verranno archiviate se non è presente un criterio che richiede l'archiviazione di tali sessioni.

Con il cmdlet **Get-CsArchivingConfiguration** è possibile determinare come è stata configurata l'archiviazione delle sessioni di messaggistica istantanea nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsArchivingConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsArchivingConfiguration"}

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
<td><p>Consente l'utilizzo di caratteri jolly per restituire una raccolta o più raccolte di impostazioni di configurazione dell'archiviazione. Per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi seguente: -Filter site:*. Per restituire una raccolta di tutte le impostazioni con valore stringa &quot;Canada&quot; nella relativa proprietà Identity (l'unica proprietà cui è possibile applicare un filtro), utilizzare la sintassi seguente: -Filter &quot;*Canada*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Consente di indicare l'identificatore univoco per la raccolta delle impostazioni di archiviazione che si desidera restituire. Per far riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per restituire informazioni sulle impostazioni assegnate a un singolo pool di registrazione, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;</p>
<p>Le impostazioni a livello di pool sono disponibili solo in Lync Server 2013.</p>
<p>Si noti che non è possibile utilizzare caratteri jolly quando si specifica un parametro Identity. Se tuttavia è necessario utilizzare caratteri jolly, includere il parametro Filter.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsArchivingConfiguration</strong> restituirà una raccolta di tutte le impostazioni di configurazione dell'archiviazione in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione dell'archiviazione dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsArchivingConfiguration** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsArchivingConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Archiving.ArchivingSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsArchivingConfiguration](new-csarchivingconfiguration.md)  
[Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)  
[Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)  
[Set-CsArchivingServer](set-csarchivingserver.md)

