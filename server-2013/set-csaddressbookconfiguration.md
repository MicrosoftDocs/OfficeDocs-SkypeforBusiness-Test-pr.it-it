---
title: Set-CsAddressBookConfiguration
TOCTitle: Set-CsAddressBookConfiguration
ms:assetid: a700328b-c738-447a-a03c-319852b42240
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412784(v=OCS.15)
ms:contentKeyID: 49301583
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAddressBookConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione della Rubrica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsAddressBookConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAddressBookConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableFileGeneration <$true | $false>] [-EnablePhotoSearch <$true | $false>] [-Force <SwitchParameter>] [-IgnoreGenericRules <$true | $false>] [-KeepDuration <UInt32>] [-MaxDeltaFileSizePercentage <UInt32>] [-MaxFileShareThreadCount <Int32>] [-RunTimeOfDay <DateTime>] [-SynchronizePollingInterval <TimeSpan>] [-UseNormalizationRules <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio la proprietà RunTimeOfDay, che determina l'ora del giorno in cui viene eseguita la sincronizzazione della Rubrica, viene impostata su 23:00 (11:00 della sera) con un formato 24 ore. Il parametro Identity viene utilizzato per limitare la modifica alle impostazioni di configurazione della Rubrica con Identity site:Redmond.

    Set-CsAddressBookConfiguration -identity site:Redmond -RunTimeOfDay 23:00

## ESEMPIO 2

Nell'esempio 2 la proprietà RunTimeOfDay viene impostata sulle 11:00 di sera (23:00) per tutte le raccolte di impostazioni della Rubrica configurate nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsAddressBookConfiguration** insieme al parametro Filter per restituire una raccolta di tutte le impostazioni specifiche del sito. Il valore di filtro "site:\*" circoscrive i dati restituiti limitandoli alle raccolte configurate nell'ambito del sito. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Set-CsAddressBookConfiguration**, che modifica il valore della proprietà RunTimeOfDay di ogni elemento della raccolta.

    Get-CsAddressBookConfiguration -Filter site:* | Set-CsAddressBookConfiguration -RunTimeOfDay 23:00

## ESEMPIO 3

Nell'esempio 3 viene modificata la proprietà KeepDuration di ogni raccolta di impostazioni della Rubrica in cui KeepDuration è inferiore a 30 giorni. A tale scopo, viene utilizzato il cmdlet **Get-CsAddressBookConfiguration** senza parametri aggiuntivi per restituire una raccolta di tutte le impostazioni della Rubrica configurate per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà KeepDuration è impostata su un valore inferiore a 30 giorni. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsAddressBookConfiguration**, che imposta su 30 giorni il valore della proprietà KeepDuration di ogni elemento della raccolta.

    Get-CsAddressBookConfiguration | Where-Object {$_.KeepDuration -lt 30} | Set-CsAddressBookConfiguration -KeepDuration 30

## Descrizione dettagliata

I server della Rubrica sono intermediari tra Servizi di dominio Active Directory e Lync Server. Il server della Rubrica garantisce che le informazioni utente archiviate in Lync Server siano sincronizzate con le informazioni utente archiviate in Servizi di dominio Active Directory. A tale scopo, i file della Rubrica vengono sincronizzati periodicamente con le informazioni archiviate nel database degli utenti.

I server della Rubrica inoltre generano periodicamente file di indice che vengono scaricati nei computer che eseguono Lync. Quando un utente ricerca i contatti, la ricerca viene effettuata in questi file di indice o nei file di indice della Rubrica archiviati nell'archivio di gestione centrale.

I server della Rubrica sono gestiti tramite le impostazioni di configurazione della Rubrica. Queste impostazioni determinano aspetti quali la frequenza con cui i file della Rubrica vengono sincronizzati con il database utenti e la frequenza con cui vengono generati i file di indice della Rubrica. Quando si installa Lync Server, viene automaticamente creato un insieme di impostazioni globali della Rubrica. È inoltre possibile creare impostazioni di configurazione personalizzate che possono essere applicate a singoli siti. Queste impostazioni, se presenti, si applicano a qualsiasi server della Rubrica che operi nel sito e hanno sempre la precedenza sulle impostazioni globali.

Il cmdlet **Set-CsAddressBookConfiguration** consente di modificare qualsiasi raccolta di impostazioni di configurazione della Rubrica attualmente in uso nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsAddressBookConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsAddressBookConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFileGeneration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), il server della Rubrica genera file di indice della Rubrica che possono essere scaricati dai client. Se è impostato su False, i file di indice non vengono generati. Per le applicazioni client sarà pertanto necessario utilizzare il servizio query Web della Rubrica per la ricerca dei contatti.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePhotoSearch</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le foto degli utenti verranno visualizzate nei risultati di ricerca.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco assegnato alla raccolta di impostazioni della Rubrica. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Non è possibile utilizzare caratteri jolly quando si specifica un valore per il parametro Identity.</p>
<p>Se il parametro non viene impostato, il cmdlet <strong>Set-CsAddressBookConfiguration</strong> modificherà le impostazioni globali.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreGenericRules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il server della Rubrica ignora o meno le regole di normalizzazione generiche utilizzate durante l'analisi dei numeri di telefono. Le regole generiche sono regole predefinite di Lync Server. Tali regole non sono modificabili. Se tuttavia si imposta il valore di questa proprietà su True, è possibile indicare ai server della Rubrica di ignorare queste regole e utilizzare invece le regole personalizzate create personalmente. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto AddressBookSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepDuration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il periodo di tempo (in giorni) durante cui i file di modifica vengono conservati nel server della Rubrica. I file di modifica anteriori al valore della proprietà KeepDuration verranno eliminati. Il parametro KeepDuration può essere impostato su qualsiasi valore intero compreso tra 1 e 90, inclusi. Il valore predefinito è 30 giorni.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxDeltaFileSizePercentage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Quando vengono apportate modifiche in Active Directory (ad esempio, viene abilitato un nuovo utente per Lync Server), il server della Rubrica in genere registra tali modifiche in un &quot;file delta&quot;, ovvero un file contenente solo le informazioni aggiornate. Lync può quindi scaricare i file delta anziché un file della Rubrica completo. La proprietà MaxDeltaFileSizePercentage determina le dimensioni massime che i file delta possono raggiungere prima di essere incorporati nel file della Rubrica completo. Per impostazione predefinita, i file delta possono raggiungere una dimensione pari al 20 percento del file della Rubrica completo prima che venga generato un nuovo file di Rubrica. A questo punto, i client Lync scaricheranno il file completo anziché un file delta.</p>
<p>MaxDeltaFileSizePercentage deve essere un valore percentuale compreso fra 1 e 100, inclusi.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxFileShareThreadCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Specifica il numero massimo di risorse di sistema che possono essere usate dal server della Rubrica se si verificano problemi durante l'accesso alla condivisione file del servizio. Il valore predefinito è 300.</p></td>
</tr>
<tr class="odd">
<td><p><em>RunTimeOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Indica l'ora del giorno in cui i server generano nuovi file della Rubrica. La proprietà RunTimeOfDay si basa su un formato 24 ore (ore:minuti:secondi), in cui 00:00:00 rappresenta la mezzanotte e 23:59:00 rappresenta le 11:59 di sera.</p>
<p>Il valore predefinito è 01:30:00 (1:30 del mattino).</p></td>
</tr>
<tr class="even">
<td><p><em>SynchronizePollingInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Indica la frequenza con cui i server della Rubrica sincronizzano le informazioni con quelle archiviate nel database degli utenti. Il parametro SynchronizePollingInterval può essere impostato su qualsiasi valore compreso tra 5 secondi (00:00:05) e 3 ore (03:00:00). Il valore predefinito è 5 minuti (00:05:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>UseNormalizationRules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i server della Rubrica debbano utilizzare le regole di normalizzazione del telefono durante il recupero dei numeri telefonici. Se impostato su False, i numeri di telefono verranno recuperati così come sono e sarà responsabilità dell'applicazione client applicare le regole di normalizzazione durante la visualizzazione di tali numeri.</p>
<p>Il valore predefinito è True.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings. Il cmdlet **Set-CsAddressBookConfiguration** accetta l'input da pipeline degli oggetti configurazione della Rubrica.

## Tipi restituiti

Il cmdlet **Set-CsAddressBookConfiguration** non restituisce un valore o un oggetto. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)  
[Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

