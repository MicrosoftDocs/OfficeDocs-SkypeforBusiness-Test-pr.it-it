---
title: Remove-CsAddressBookConfiguration
TOCTitle: Remove-CsAddressBookConfiguration
ms:assetid: d634abc2-988a-48f9-ad11-903759516082
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398934(v=OCS.15)
ms:contentKeyID: 49302106
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAddressBookConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di configurazione della Rubrica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsAddressBookConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene utilizzato il cmdlet **Remove-CsAddressBookConfiguration** per eliminare le impostazioni di configurazione della Rubrica con valore Identity site:Redmond. L'utilizzo del parametro Identity assicura che vengano rimosse solo le impostazioni della Rubrica specificate.

    Remove-CsAddressBookConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le raccolte di impostazioni della Rubrica configurate nell'ambito del sito. A tale scopo, viene utilizzato il cmdlet **Get-CsAddressBookConfiguration** per recuperare una raccolta di tutte le impostazioni della Rubrica che sono state configurate nell'ambito del sito. Tale operazione viene eseguita utilizzando il parametro Filter con il valore di filtro "site:\*". La raccolta recuperata viene quindi inviata tramite pipe al cmdlet **Remove-CsAddressBookConfiguration**, che rimuove tutti gli elementi presenti nella raccolta.

    Get-CsAddressBookConfiguration -Filter site:* | Remove-CsAddressBookConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono rimosse tutte le impostazioni della Rubrica in cui i file delle modifiche vengono conservati per meno di 30 giorni. Per eseguire questa attività, viene utilizzato il cmdlet **Get-CsAddressBookConfiguration** per restituire una raccolta di tutte le impostazioni della Rubrica attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni la cui proprietà KeepDuration è impostata su un valore minore di 30 giorni. Notare la sintassi: 30., con un punto dopo il numero di giorni. La raccolta filtrata viene infine inviata tramite pipe al cmdlet **Remove-CsAddressBookConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CsAddressBookConfiguration | Where-Object {$_.KeepDuration -lt 30.} | Remove-CsAddressBookConfiguration

## Descrizione dettagliata

I server della Rubrica sono intermediari tra Servizi di dominio Active Directory e Lync Server. Il server della Rubrica garantisce che le informazioni degli utenti archiviate in Lync Server siano sincronizzate con le informazioni degli utenti archiviate in Servizi di dominio Active Directory. A tale scopo, i file della Rubrica vengono sincronizzati periodicamente con le informazioni archiviate nel database degli utenti.

I server della Rubrica inoltre generano periodicamente file di indice che vengono scaricati nei computer che eseguono Lync Server. Quando un utente ricerca contatti, esegue la ricerca in tali file di indice o nei file di indice della Rubrica archiviati nell'archivio di gestione centrale.

I server della Rubrica vengono gestiti tramite impostazioni di configurazione della Rubrica. Queste impostazioni determinano quanto spesso i file della Rubrica debbano essere sincronizzati con il database degli utenti e la frequenza di generazione di tali file di indice della Rubrica. Durante l'installazione di Lync Server viene creato automaticamente un insieme di impostazioni globali della Rubrica. È inoltre possibile creare impostazioni di configurazione personalizzate che possono essere applicate ai singoli siti. Queste impostazioni, se esistono, si applicano a qualsiasi server della Rubrica che operi nel sito e hanno la precedenza sulle impostazioni globali.

Il cmdlet **New-CsAddressBookConfiguration** consente di creare impostazioni di configurazione della Rubrica a livello di sito. Per rimuovere successivamente le impostazioni della Rubrica configurate nell'ambito del sito, utilizzare il cmdlet **Remove-CsAddressBookConfiguration**. È anche possibile eseguire il cmdlet **Remove-CsAddressBookConfiguration** per le impostazioni globali, le quali tuttavia non possono essere realmente rimosse. Invece, eseguendo il cmdlet **Remove-CsAddressBookConfiguration** per le impostazioni globali, i valori predefiniti di tutte le proprietà globali verranno ripristinati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsAddressBookConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAddressBookConfiguration"}

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
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione della Rubrica da rimuovere. Per rimuovere la raccolta globale, utilizzare la seguente sintassi: -Identity global. Quando si &quot;rimuovono&quot; le impostazioni globali, semplicemente si reimpostano tutte le proprietà sui rispettivi valori predefiniti. Per rimuovere la raccolta di un sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Non è possibile utilizzare i caratteri jolly per specificare l'identità di un criterio.</p></td>
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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings. Il cmdlet **Remove-CsAddressBookConfiguration** accetta l'input da pipeline di oggetti di configurazione della Rubrica.

## Tipi restituiti

Il cmdlet **Remove-CsAddressBookConfiguration** non restituisce alcun oggetto o valore. Questo cmdlet rimuove piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)  
[New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)  
[Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

