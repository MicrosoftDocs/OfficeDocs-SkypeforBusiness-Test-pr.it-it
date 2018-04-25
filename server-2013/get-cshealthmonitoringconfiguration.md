---
title: Get-CsHealthMonitoringConfiguration
TOCTitle: Get-CsHealthMonitoringConfiguration
ms:assetid: 843876f1-8aa6-4324-a981-8eded4d3b16d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398667(v=OCS.15)
ms:contentKeyID: 49301186
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsHealthMonitoringConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle impostazioni di configurazione del monitoraggio dello stato attualmente in uso nell'organizzazione. Tali impostazioni consentono agli amministratori di eseguire test di controllo della qualità senza dover fornire i nomi utente e le password per gli account di test necessari. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsHealthMonitoringConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsHealthMonitoringConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite tutte le impostazioni di configurazione del monitoraggio dello stato attualmente in uso nell'organizzazione.

    Get-CsHealthMonitoringConfiguration

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce un'unica raccolta di impostazioni di configurazione per il monitoraggio dello stato di integrità: le impostazioni con Identity atl-cs-001.litwareinc.com.

    Get-CsHealthMonitoringConfiguration -Identity atl-cs-001.litwareinc.com

## ESEMPIO 3

Nell'esempio 3 vengono restituite tutte le impostazioni di configurazione per il monitoraggio dello stato create per il dominio litwareinc.com. A tale scopo, viene chiamato il cmdlet **Get-CsHealthMonitoringConfiguration** con il parametro Filter. Il valore di filtro "\*.litwareinc.com" assicura che vengano restituite solo le impostazioni con parametro Identity che termina con il valore stringa ".litwareinc.com".

    Get-CsHealthMonitoringConfiguration -Filter *.litwareinc.com

## ESEMPIO 4

Il comando mostrato nell'esempio 4 restituisce tutte le impostazioni di configurazione per il monitoraggio dello stato in cui è incluso l'utente con indirizzo SIP sip:kenmyer@litwareinc.com come uno degli utenti di test. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsHealthMonitoringConfiguration** senza ulteriori parametri. Viene restituita una raccolta di tutte le impostazioni di configurazione per il monitoraggio dello stato attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni con proprietà FirstTestUserSipUri uguale a "sip:kenmyer@litwareinc.com" oppure con proprietà SecondTestUserSipUri uguale a "sip:kenmyer@litwareinc.com". Verranno restituite tutte le raccolte di impostazioni in cui viene utilizzato l'indirizzo SIP di Ken Myer come primo o secondo utente di test.

    Get-CsHealthMonitoringConfiguration | Where-Object {$_.FirstTestUserSipUri -eq "sip:kenmyer@litwareinc.com" -or $_.SecondTestUserSipUri -eq " sip:kenmyer@litwareinc.com"}

## Descrizione dettagliata

Le transazioni sintetiche vengono utilizzate in Lync Server per verificare che gli utenti siano in grado di effettuare correttamente attività comuni quali l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono appartenente alla rete PSTN (Public Switched Telephone Network). Tali verifiche possono essere eseguite "manualmente" da un amministratore oppure possono essere eseguite automaticamente da un'applicazione come Microsoft System Center Operations Manager (in precedenza Microsoft Operations Manager).

È possibile condurre le transazioni in due diversi modi. Molti amministratori utilizzeranno i cmdlet **CsHealthMonitoringConfiguration** per configurare account di test per ciascun pool di registrazione o di server Director. Questi account di test sono costituiti da una coppia di account utente preconfigurati per l'utilizzo con le transazioni sintetiche. Si tratta in genere di account di test e non di account appartenenti a utenti effettivi. Dopo aver configurato gli account di test per un pool, gli amministratori possono eseguire una transazione sintetica sul pool senza dover specificare le identità o fornire le credenziali degli account utente coinvolti nel test. In realtà, la transazione sintetica utilizza automaticamente gli account di test preconfigurati durante l'esecuzione dei controlli.

In alternativa, gli amministratori possono eseguire una transazione sintetica utilizzando account utente effettivi. Ad esempio, se due utenti non riescono a scambiarsi messaggi istantanei, l'amministratore può eseguire una transazione sintetica utilizzando i due account in questione, anziché la coppia di account di test. Se si decide di eseguire una transazione sintetica utilizzando account utente effettivi, sarà necessario specificare le credenziali di ciascun utente.

Il cmdlet **Get-CsHealthMonitoringConfiguration** consente di recuperare le informazioni sulle impostazioni di configurazione per il monitoraggio dello stato di integrità attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsHealthMonitoringConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsHealthMonitoringConfiguration"}

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
<td><p>Consente l'utilizzo di caratteri jolly per specificare le impostazioni di configurazione per il monitoraggio dello stato di integrità da recuperare. Ad esempio, la sintassi che segue restituisce tutte le impostazioni configurate per il dominio litwareinc.com: -Filter &quot;*.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del pool in cui sono state assegnate le impostazioni di configurazione per il monitoraggio dello stato di integrità. Ad esempio: -Identity atl-cs-001.litwareinc.com.</p>
<p>Se il parametro non viene incluso, il cmdlet <strong>Get-CsHealthMonitoringConfiguration</strong> restituirà le informazioni su tutte le impostazioni di configurazione per il monitoraggio dello stato attualmente in uso.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione del monitoraggio dello stato di integrità dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsHealthMonitoringConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsHealthMonitoringConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.HealthMonitoring.HealthMonitoringSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)  
[Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)  
[Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)

