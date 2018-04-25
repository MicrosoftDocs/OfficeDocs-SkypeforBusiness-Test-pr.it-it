---
title: Remove-CsUserServicesConfiguration
TOCTitle: Remove-CsUserServicesConfiguration
ms:assetid: 8eed6091-ab96-49d4-a0c0-d1f9180a0b90
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398722(v=OCS.15)
ms:contentKeyID: 49301294
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserServicesConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione di Servizi utente. Il servizio Servizi utente viene utilizzato per gestire le conferenze e conservare le informazioni sulla presenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsUserServicesConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 rimuove le impostazioni di configurazione di Servizi utente per il sito Redmond (-Identity site:Redmond).

    Remove-CsUserServicesConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le impostazioni di configurazione di Servizi utente applicate nell'ambito del servizio. A tale scopo, il comando chiama il cmdlet **Get-CsUserServicesConfiguration** insieme al parametro Filter. Il valore di filtro "service:\*" restituisce solo le impostazioni configurate nell'ambito del servizio, ovvero le impostazioni la cui identità (Identity) inizia con i caratteri "service:". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsUserServicesConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsUserServicesConfiguration -Filter "service:*:" | Remove-CsUserServicesConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono rimosse tutte le impostazioni di configurazione di Servizi utente che consentono agli utenti di disporre di più di 250 contatti. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsUserServicesConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione di Servizi utente attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui il valore della proprietà MaxContacts è maggiore di 250. Queste impostazioni vengono quindi inviate tramite pipe al cmdlet **Remove-CsUserServicesConfiguration**, che le rimuove.

    Get-CsUserServicesConfiguration | Where-Object {$_.MaxContacts -gt 250} | Remove-CsUserServicesConfiguration

## Descrizione dettagliata

Lync Server utilizza il servizio Servizi utente per mantenere le informazioni sulla presenza degli utenti e per gestire le riunioni e le conferenze. A loro volta, i cmdlet **CsUserServicesConfiguration** vengono utilizzati per amministrare le impostazioni di configurazione di Servizi utente nell'ambito globale, del sito e del servizio. Si noti che l'unico servizio in grado di ospitare le impostazioni di configurazione di Servizi utente è il servizio stesso. Queste impostazioni consentono di specificare elementi quali il numero di contatti che un utente può avere, il numero di riunioni pianificate che un utente può avere in un determinato momento e l'intervallo di tempo massimo in cui una determinata riunione può rimanere attiva.

Il cmdlet **Remove-CsUserServicesConfiguration** consente di eliminare le impostazioni di configurazione di Servizi utente applicate nell'ambito del sito o del servizio. Questo cmdlet può essere eseguito anche per la raccolta globale. In questo caso, le impostazioni però non verranno rimosse, in quanto le impostazioni globali non possono essere eliminate. Tutte le proprietà della raccolta globale verranno invece reimpostate sui rispettivi valori predefiniti. Se ad esempio il valore MaxContacts nelle impostazioni globali è stato impostato su 500 e quindi si esegue il cmdlet **Remove-CsUserServicesConfiguration**, verrà ripristinato il valore predefinito di MaxContacts, ovvero 250.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsUserServicesConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserServicesConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione di Servizi utente da eliminare. Per eliminare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per eliminare le impostazioni a livello di servizio, utilizzare una sintassi simile alla seguente: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>Il cmdlet <strong>Remove-CsUserServicesConfiguration</strong> può essere eseguito anche per la raccolta globale. In questo caso tuttavia le impostazioni globali non verranno rimosse, ma verranno ripristinati i valori predefiniti di tutte le proprietà della raccolta globale.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings. Il cmdlet **Remove-CsUserServicesConfiguration** accetta istanze inviate tramite pipeline dell'oggetto impostazioni di configurazione di Servizi utente.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsUserServicesConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.UserServicesSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesConfiguration](get-csuserservicesconfiguration.md)  
[New-CsUserServicesConfiguration](new-csuserservicesconfiguration.md)  
[Set-CsUserServicesConfiguration](set-csuserservicesconfiguration.md)

