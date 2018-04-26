---
title: Get-CsDialInConferencingConfiguration
TOCTitle: Get-CsDialInConferencingConfiguration
ms:assetid: 75a959f7-5712-4dbc-b7ac-5a15b9b2f404
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398575(v=OCS.15)
ms:contentKeyID: 49301011
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le informazioni relative al modo in cui Lync Server risponde quando gli utenti partecipano a una conferenza telefonica con accesso esterno o escono da essa. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDialInConferencingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialInConferencingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene restituita una raccolta di tutte le impostazioni di configurazione di conferenza telefonica con accesso esterno attualmente in uso nell'organizzazione. Chiamando il cmdlet **Get-CsDialInConferencingConfiguration** senza alcun parametro, viene sempre restituita la raccolta completa delle impostazioni di conferenza telefonica con accesso esterno.

    Get-CsDialInConferencingConfiguration

## ESEMPIO 2

L'Esempio 2 restituisce le impostazioni di configurazione della conferenza telefonica con Identity site:Redmond.

    Get-CsDialInConferencingConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per ottenere tutte le impostazioni di conferenza telefonica con accesso esterno configurate nell'ambito del sito. Il valore di filtro "site:\*" indica al cmdlet **Get-CsDialInConferencingConfiguration** di restituire solo le raccolte di impostazioni in cui l'identità (Identity) inizia con la stringa "site:". Per impostazione predefinita, tutte le impostazioni di conferenza telefonica con accesso esterno con identità (Identity) che inizia con la stringa "site:" sono impostazioni configurate nell'ambito del sito.

    Get-CsDialInConferencingConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 vengono utilizzati i cmdlet **Get-CsDialInConferencingConfiguration** e **Where-Object** per restituire una raccolta di tutte le impostazioni di configurazione di conferenza telefonica con accesso esterno in cui la proprietà EnableNameRecording è impostata su False. A tale scopo, viene chiamato il cmdlet **Get-CsDialInConferencingConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di conferenza telefonica con accesso esterno. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableNameRecording è uguale a False.

    Get-CsDialInConferencingConfiguration | Where-Object {$_.EnableNameRecording -eq $False}

## Descrizione dettagliata

Quando gli utenti partecipano a una conferenza telefonica con accesso esterno o escono da essa, Lync Server può rispondere in diversi modi. Ad esempio, ai partecipanti potrebbe essere richiesto di registrare il proprio nome prima di accedere alla conferenza. Allo stesso modo, gli amministratori possono decidere se impostare un annuncio di Lync Server che segnala l'accesso o l'uscita dei partecipanti alla conferenza telefonica con accesso esterno.

Questi "comportamenti" relativi alla conferenza vengono gestiti utilizzando le impostazioni di configurazione della conferenza telefonica; queste impostazioni possono essere configurate nell'ambito globale o nell'ambito del sito. Le impostazioni configurate nell'ambito del sito hanno la precedenza su quelle configurate nell'ambito globale. Il cmdlet **Get-CsDialInConferencingConfiguration** consente di recuperare le informazioni sulle impostazioni di configurazione della conferenza telefonica attualmente in uso nella propria organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsDialInConferencingConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare le impostazioni di configurazione della conferenza telefonica. Ad esempio, per ottenere una raccolta di tutte le impostazioni di configurazione applicate nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per ottenere tutte le impostazioni che hanno il termine &quot;EMEA&quot; nella loro identità, utilizzare la seguente sintassi: -Filter &quot;*EMEA*&quot;. Si noti che il parametro Filter agisce solo sull'identità delle impostazioni; non è possibile filtrare altre proprietà di configurazione della conferenza telefonica.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità delle impostazioni di configurazione della conferenza telefonica da recuperare. Per ottenere le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per ottenere le impostazioni del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità. Per ottenere questo risultato, utilizzare il parametro Filter.</p>
<p>Se eseguito senza parametri, il cmdlet <strong>Get-CsDialInConferencingConfiguration</strong> restituisce informazioni su tutte le impostazioni di configurazione di conferenza telefoniche con accesso esterno in uso nella propria organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati della conferenza telefonica dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDialInConferencingConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsDialInConferencingConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsDialInConferencingConfiguration](new-csdialinconferencingconfiguration.md)  
[Remove-CsDialInConferencingConfiguration](remove-csdialinconferencingconfiguration.md)  
[Set-CsDialInConferencingConfiguration](set-csdialinconferencingconfiguration.md)

