---
title: Get-CsQoEConfiguration
TOCTitle: Get-CsQoEConfiguration
ms:assetid: e2ed87e0-a5ae-41a2-8572-bda0070c59dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399004(v=OCS.15)
ms:contentKeyID: 49302256
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsQoEConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più raccolte di impostazioni QoE (Quality of Experience, qualità percepita dagli utenti). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsQoEConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsQoEConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

In questo esempio viene utilizzato il cmdlet **Get-CsQoEConfiguration** per restituire una raccolta di tutte le impostazioni QoE configurate per l'utilizzo nell'organizzazione.

    Get-CsQoEConfiguration

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il parametro Identity per garantire che il cmdlet **Get-CsQoEConfiguration** restituisca solo le impostazioni QoE la cui identità è site:Redmond.

    Get-CsQoEConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per restituire tutte le impostazioni QoE che sono state configurate nell'ambito del sito. La stringa con caratteri jolly "site:\*" restituisce tutte le impostazioni QoE la cui identità inizia con il valore stringa site:. Le impostazioni che soddisfano questi criteri sono impostazioni configurate nell'ambito del sito.

    Get-CsQoEConfiguration -Filter site:*

## ESEMPIO 4

Nell'esempio 4 viene restituita una raccolta di tutte le impostazioni QoE per le quali il valore della proprietà KeepQoEDataForDays è minore di 30 giorni. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsQoEConfiguration** per restituire una raccolta di tutte le impostazioni QoE configurate nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro che limita i dati restituiti alle impostazioni che hanno un valore KeepQoEDataForDays minore di 30 giorni.

    Get-CsQoEConfiguration | Where-Object {$_.KeepQoEDataForDays -lt 30}

## Descrizione dettagliata

Le metriche QoE registrano la qualità delle chiamate audio e video effettuate nell'organizzazione, includendo informazioni quali il numero di pacchetti di rete persi, i rumori di fondo e la quantità di "instabilità" (differenze nel ritardo dei pacchetti). Queste metriche vengono archiviate in un database separatamente rispetto ad altri dati, ad esempio la registrazione dettagli chiamata (CDR, Call Detail Record), in modo che sia possibile abilitare e disabilitare il servizio QoE in maniera indipendente rispetto ad altre registrazioni di dati. Utilizzare questo cmdlet per recuperare impostazioni che configurano QoE a livello globale o di sito.

QoE fa parte del ruolo Monitoring Server. È pertanto necessario distribuire il Monitoring Server nell'installazione di Lync Server prima che la registrazione QoE abbia effetto o prima che sia possibile raccogliere i dati QoE.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsQoEConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsQoEConfiguration"}

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
<td><p>Consente di utilizzare caratteri jolly per restituire una o più raccolte di impostazioni di configurazione QoE. Per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi seguente: -Filter site:*. Per restituire una raccolta di tutte le impostazioni la cui identità (l'unica proprietà a cui è possibile applicare un filtro) contiene il valore stringa &quot;Western&quot;, utilizzare la seguente sintassi: -Filter *Western*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni che si desidera recuperare. I valori possibili sono global e site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito nella distribuzione di Lync Server a cui si desidera applicare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le impostazioni dalla replica locale dell'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsQoEConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.QoE.QoESettings.

## Vedere anche

#### Ulteriori risorse

[New-CsQoEConfiguration](new-csqoeconfiguration.md)  
[Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)  
[Set-CsQoEConfiguration](set-csqoeconfiguration.md)

