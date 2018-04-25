---
title: New-CsAddressBookConfiguration
TOCTitle: New-CsAddressBookConfiguration
ms:assetid: 5a92a2b0-c46e-44e3-b07c-fc9ff0d33b2b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398395(v=OCS.15)
ms:contentKeyID: 49300676
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAddressBookConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione della Rubrica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsAddressBookConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableFileGeneration <$true | $false>] [-EnablePhotoSearch <$true | $false>] [-Force <SwitchParameter>] [-IgnoreGenericRules <$true | $false>] [-InMemory <SwitchParameter>] [-KeepDuration <UInt32>] [-MaxDeltaFileSizePercentage <UInt32>] [-MaxFileShareThreadCount <Int32>] [-RunTimeOfDay <DateTime>] [-SynchronizePollingInterval <TimeSpan>] [-UseNormalizationRules <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione della Rubrica con identità (Identity) site:Redmond. Per creare una nuova raccolta è necessario chiamare il cmdlet **New-CsAddressBookConfiguration** insieme al parametro Identity e qualunque altro parametro facoltativo, ad esempio i parametri KeepDuration e SynchronizePollingInterval.

    New-CsAddressBookConfiguration -Identity site:Redmond -KeepDuration 15 -SynchronizePollingInterval 00:10:00

## ESEMPIO 2

Nell'esempio 2 viene creata una nuova raccolta di impostazioni della Rubrica per il sito Paris. In questa nuova raccolta vengono utilizzati due valori (KeepDuration e SynchronizePollingInterval) copiati dalle impostazioni della Rubrica configurate per il sito Redmond. A tale scopo, nel primo comando viene utilizzato il cmdlet **Get-CsAddressBookConfiguration** per restituire una raccolta di tutte le impostazioni della Rubrica configurate per il sito Redmond. Queste informazioni vengono memorizzate nella variabile denominata $x.

Nel secondo comando viene quindi utilizzato il cmdlet **New-CsAddressBookConfiguration** per creare le impostazioni della Rubrica per il sito Paris. Questo comando include due parametri facoltativi (KeepDuration e SynchronizePollingInterval), in cui sono contenuti i valori copiati da site:Redmond. Ad esempio, KeepDuration utilizza il valore di parametro $x.KeepDuration. Tale valore valore di parametro rappresenta le informazioni KeepDuration copiate dal sito Redmond.

    $x = Get-CsAddressBookConfiguration -Identity site:Redmond
    New-CsAddressBookConfiguration -Identity site:Paris -KeepDuration $x.KeepDuration -SynchronizePollingInterval $x.SynchronizePollingInterval

## ESEMPIO 3

Nell'esempio 3 viene illustrato come utilizzare il parametro InMemory per creare un'istanza solo in memoria di una raccolta di impostazioni della Rubrica, modificare tali impostazioni in memoria e utilizzare quindi il cmdlet **Set-CsAddressBookConfiguration** per creare una raccolta effettiva con identità (Identity) site:Redmond. A tale scopo, il primo comando crea una nuova istanza solo in memoria di una configurazione delle impostazioni della Rubrica, archiviando tale istanza in una variabile denominata $x. Il parametro InMemory garantisce che tali impostazioni della Rubrica siano presenti solo in memoria. Nel caso in cui si termini la sessione Lync Server o si elimini la variabile $x, le impostazioni verranno rimosse e non verranno applicate al sito Redmond.

Nei comandi 2 e 3 vengono modificate due proprietà delle di impostazioni virtuali della Rubrica: il comando 2 imposta il valore della proprietà KeepDuration su 15 giorni e il comando 3 imposta SynchronizePollingInterval su 10 minuti (00:10:00). Il quarto e ultimo comando utilizza il cmdlet **Set-CsAddressBookConfiguration** e il parametro Instance per trasformare le impostazioni della Rubrica virtuali in una raccolta effettiva di impostazioni configurate nel sito Redmond.

    $x = New-CsAddressBookConfiguration -Identity site:Redmond -InMemory
    $x.KeepDuration = 15
    $x.SynchronizePollingInterval = "00:10:00"
    Set-CsAddressBookConfiguration -Instance $x

## Descrizione dettagliata

I server della Rubrica sono intermediari tra Servizi di dominio Active Directory e Lync Server. Il server della Rubrica garantisce che le informazioni utente archiviate in Lync Server siano sincronizzate con le informazioni utente archiviate in Servizi di dominio Active Directory. A tale scopo, i file della Rubrica vengono sincronizzati periodicamente con le informazioni archiviate nel database degli utenti.

I server della Rubrica inoltre generano periodicamente file di indice che vengono scaricati nei computer che eseguono Lync. Quando un utente ricerca i contatti, la ricerca viene effettuata in questi file di indice o nei file di indice della Rubrica archiviati nell'archivio di gestione centrale.

I server della Rubrica sono gestiti tramite le impostazioni di configurazione della Rubrica. Queste impostazioni determinano aspetti quali la frequenza con cui i file della Rubrica vengono sincronizzati con il database utenti e la frequenza con cui vengono generati i file di indice della Rubrica. Quando si installa Lync Server, viene automaticamente creato un insieme di impostazioni globali della Rubrica. È inoltre possibile creare impostazioni di configurazione personalizzate che possono essere applicate a singoli siti. Queste impostazioni, se presenti, si applicano a qualsiasi server della Rubrica che operi nel sito e hanno sempre la precedenza sulle impostazioni globali.

Le impostazioni a livello di sito vengono create utilizzando il cmdlet **New-CsAddressBookConfiguration**. È possibile creare le impostazioni solo nell'ambito del sito. La creazione di nuove impostazioni in altri ambiti, compreso l'ambito globale, avrà esito negativo. Il comando avrà esito negativo anche se il sito contiene già una raccolta di impostazioni della Rubrica.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsAddressBookConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAddressBookConfiguration"}

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
<td><p>Identificatore univoco da assegnare alla nuova raccolta di impostazioni della Rubrica. Poiché è possibile creare nuove raccolte solo nell'ambito del sito, l'identità avrà sempre il prefisso &quot;site:&quot; seguito dal nome del sito; ad esempio &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableFileGeneration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), il server della Rubrica genera file di indice della Rubrica che possono essere scaricati dai client. Se è impostato su False, i file di indice non vengono generati. Per le applicazioni client sarà pertanto necessario utilizzare il servizio query Web della Rubrica per la ricerca dei contatti.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePhotoSearch</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le foto degli utenti verranno visualizzate nei risultati di ricerca.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreGenericRules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il server della Rubrica ignora o meno le regole di normalizzazione generiche utilizzate durante l'analisi dei numeri di telefono. Le regole generiche sono regole predefinite di Lync Server. Tali regole non sono modificabili. Se tuttavia si imposta il valore di questa proprietà su True, è possibile indicare ai server della Rubrica di ignorare queste regole e utilizzare invece le regole personalizzate create personalmente. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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
<p>MaxDeltaFileSizePercentage deve essere immesso come valore percentuale, da 1 a 100, compresi.</p></td>
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

Nessuno. Il cmdlet **New-CsAddressBookConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Consente di creare le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)  
[Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

