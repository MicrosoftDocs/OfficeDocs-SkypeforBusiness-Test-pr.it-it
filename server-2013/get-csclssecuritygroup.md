---
title: Get-CsClsSecurityGroup
TOCTitle: Get-CsClsSecurityGroup
ms:assetid: ce7aa87a-2355-4025-bba8-d4debf2137d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205285(v=OCS.15)
ms:contentKeyID: 49302024
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsSecurityGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui gruppi di sicurezza di configurazione della registrazione centralizzata in uso nell'organizzazione. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare la traccia eventi in più computer contemporaneamente. I gruppi di sicurezza possono essere utilizzati solo con Skype for Business online.

Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsClsSecurityGroup [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsSecurityGroup [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando illustrato nell'esempio 1 consente di restituire informazioni su tutti i gruppi di sicurezza della registrazione centralizzata configurati per l'utilizzo nell'organizzazione.

    Get-CsClsSecurityGroup

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per un solo gruppo di sicurezza della registrazione centralizzata: il gruppo con valore Identity global/helpdesk.

    Get-CsClsSecurityGroup -Identity "global/HelpDesk"

## Esempio 3

Nell'esempio 3 vengono restituite le informazioni per tutti i gruppi di sicurezza della registrazione centralizzata configurati nell'ambito globale. A tale scopo, viene incluso il parametro Filter con il valore filtro "global/\*". Questo valore filtro limita i dati restituiti ai gruppi configurati nell'ambito globale.

    Get-CsClsSecurityGroup -Filter "global/*"

## Esempio 4

Il comando illustrato nell'esempio 4 restituisce tutti i gruppi di sicurezza della registrazione centralizzata per i quali il livello di accesso è stato impostato su RedmondSupport. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsClsSecurityGroup** senza parametri per restituire una raccolta di tutti i gruppi di sicurezza della registrazione centralizzata disponibili. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che sceglie solo i gruppi per i quali la proprietà AccessLevel è uguale a RedmondSupport.

    Get-CsClsSecurityGroup | Where-Object {$_.AccessLevel -eq "RedmondSupport"}

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata consente inoltre agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

Con Skype for Business online, i gruppi di sicurezza vengono utilizzati per determinare quali utenti hanno accesso alle informazioni che consentono l'identificazione personale dell'utente scritte nei file di log. I gruppi di sicurezza vengono creati utilizzando il cmdlet [New-CsClsSecurityGroup](new-csclssecuritygroup.md) e vengono quindi aggiunti a una raccolta di impostazioni di configurazione della registrazione centralizzata. È possibile restituire informazioni sui gruppi di sicurezza di registrazione centralizzata utilizzando il cmdlet **Get-CsClsSecurityGroup**.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsSecurityGroup"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsClsSecurityGroup** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare caratteri jolly per restituire uno o più gruppi di sicurezza della registrazione centralizzata. Ad esempio, per restituire una raccolta di tutti i gruppi configurati nell'ambito globale, utilizzare la seguente sintassi:</p>
<p>-Filter &quot;global/*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il gruppo di sicurezza della registrazione centralizzata da restituire. L'identità di un gruppo di sicurezza è data dall'ambito in cui il gruppo è stato creato seguito dal nome del gruppo. Ad esempio, per restituire un gruppo denominato HelpDesk creato nell'ambito globale, utilizzare la seguente sintassi:</p>
<p>-Identity &quot;global/HelpDesk&quot;</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsClsSecurityGroup</strong> restituisce informazioni su tutti i gruppi di sicurezza della registrazione centralizzata.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione dalla replica locale di archivio di gestione centrale, anziché da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClsSecurityGroup** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsClsSecurityGroup** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SecurityGroup\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsClsSecurityGroup](new-csclssecuritygroup.md)  
[Remove-CsClsSecurityGroup](remove-csclssecuritygroup.md)  
[Set-CsClsSecurityGroup](set-csclssecuritygroup.md)

