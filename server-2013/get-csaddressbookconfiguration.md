---
title: Get-CsAddressBookConfiguration
TOCTitle: Get-CsAddressBookConfiguration
ms:assetid: 07757a19-f819-4d65-82da-50bf2f157a9b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398132(v=OCS.15)
ms:contentKeyID: 49299579
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAddressBookConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione della Rubrica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAddressBookConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAddressBookConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutte le impostazioni di configurazione della Rubrica in uso nell'organizzazione. Questo è il comportamento predefinito se si chiama il cmdlet **Get-CsAddressBookConfiguration** senza alcun parametro aggiuntivo.

    Get-CsAddressBookConfiguration

## ESEMPIO 2

Con l'esempio 2 vengono restituite informazioni sulle impostazioni di configurazione della Rubrica con identità site:Redmond.

    Get-CsAddressBookConfiguration -Identity site:Redmond

## ESEMPIO 3

In questo esempio vengono utilizzati il parametro Filter con valore "site:\*" per restituire informazioni su tutte le impostazioni di configurazione della Rubrica applicate nell'ambito del sito. Il valore del filtro fornito restituisce informazioni per tutte le impostazioni della Rubrica la cui identità inizia con il valore stringa "site:".

    Get-CsAddressBookConfiguration -Filter site:*

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni per tutte le impostazioni di configurazione della Rubrica in cui vengono utilizzate regole di normalizzazione durante l'analisi dei numeri di telefono. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsAddressBookConfiguration** per restituire una raccolta di tutte le impostazioni della Rubrica nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà UseNormalizationRules è uguale a True.

    Get-CsAddressBookConfiguration | Where-Object {$_.UseNormalizationRules -eq $True}

## Descrizione dettagliata

I server della Rubrica sono intermediari tra Servizi di dominio Active Directory e Lync Server. Il server della Rubrica garantisce che le informazioni utente archiviate in Lync Server siano sincronizzate con le informazioni utente archiviate in Active Directory. Per eseguire questa operazione i file della Rubrica vengono periodicamente sincronizzati con le informazioni archiviate nel database degli utenti.

I server della Rubrica inoltre generano periodicamente file di indice che vengono scaricati nei computer che eseguono Lync. Quando un utente ricerca contatti, la ricerca viene effettuata tramite questi file di indice o tramite i file di indice della Rubrica archiviati nell'archivio di gestione centrale.

I server della Rubrica sono gestiti tramite le impostazioni di configurazione della Rubrica. Queste impostazioni determinano con quale frequenza i file della Rubrica vengono sincronizzati con il database utenti e con quale frequenza vengono generati questi file di indice della Rubrica. Durante l'installazione di Lync Server viene automaticamente creato un set di impostazioni globali della Rubrica. È inoltre possibile creare impostazioni di configurazione personalizzate che possono essere applicate ai singoli siti. Queste impostazioni, se esistono, si applicano a qualsiasi server della Rubrica che operi nel sito e hanno la precedenza sulle impostazioni globali.

È possibile utilizzare il cmdlet **Get-CsAddressBookConfiguration** per restituire informazioni su una o su tutte le impostazioni della Rubrica attualmente in uso nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsAddressBookConfiguration** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAddressBookConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per restituire una raccolta (o più raccolte) di impostazioni della Rubrica. Ad esempio, per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi riportata di seguito: -Filter site:*. Per restituire una raccolta di tutte le impostazioni in cui la stringa &quot;EMEA&quot; compare nell'identità, utilizzare la seguente sintassi: -Filter *EMEA*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la raccolta di impostazioni della Rubrica da restituire. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond.</p>
<p>Si noti che non è possibile utilizzare i caratteri jolly quando si specifica un parametro Identity. Tuttavia, se è necessario utilizzare caratteri jolly, includere il parametro Filter.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsAddressBookConfiguration</strong> restituisce una raccolta di tutte le impostazioni della Rubrica in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione della Rubrica dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsAddressBookConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsAddressBookConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AddressBook.AddressBookSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)  
[Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)  
[Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

