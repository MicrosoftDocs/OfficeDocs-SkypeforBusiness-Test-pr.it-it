---
title: Set-CsConferenceDisclaimer
TOCTitle: Set-CsConferenceDisclaimer
ms:assetid: 97afce6d-b031-466d-a170-3ca50d6df245
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398776(v=OCS.15)
ms:contentKeyID: 49301398
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConferenceDisclaimer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà della dichiarazione di non responsabilità per le conferenze utilizzata nell'organizzazione. Tale dichiarazione è un messaggio visualizzato agli utenti che accedono a una conferenza utilizzando un collegamento ipertestuale (ad esempio, incollando un collegamento alla conferenza in un browser come Windows Internet Explorer). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsConferenceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Header <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono modificate le proprietà Header e Body per la dichiarazione di non responsabilità per le conferenze dell'organizzazione. Dal momento che è possibile disporre di una singola dichiarazione di non responsabilità, non è necessario specificare un'identità nella chiamata a **Set-CsConferenceDisclaimer**.

    Set-CsConferenceDisclaimer -Header "Litwareinc.com Online Conference" -Body "Important note: Conferencing proceedings are recorded and archived."

## Descrizione dettagliata

Quando si configurano le impostazioni per le conferenze, gli amministratori possono includere una dichiarazione di non responsabilità legale da visualizzare ai partecipanti nel momento in cui prendono parte alle conferenze ospitate da Lync Server. La dichiarazione di non responsabilità viene generalmente utilizzata per esporre le questioni legali e le leggi sulla proprietà intellettuale pertinenti alla conferenza. Gli utenti non possono partecipare alla conferenza senza accettare le condizioni precedentemente stabilite nella dichiarazione di non responsabilità. La dichiarazione di non responsabilità viene tuttavia visualizzata solamente agli utenti che accedono a una conferenza utilizzando un collegamento ipertestuale.

Lync Server consente una singola istanza globale della dichiarazione di non responsabilità per le conferenze. Il cmdlet **Set-CsConferenceDisclaimer** consente di modificare la dichiarazione utilizzata nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsConferenceDisclaimer** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsConferenceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Contenuto della dichiarazione di non responsabilità per la conferenza.</p></td>
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
<td><p><em>Header</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Titolo assegnato alla dichiarazione di non responsabilità per la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca della dichiarazione di non responsabilità per le conferenze. Dal momento che è possibile disporre di una singola istanza globale della dichiarazione di non responsabilità per le conferenze, non è necessario specificare un'identità nella chiamata al cmdlet <strong>Set-CsConferenceDisclaimer</strong>. È tuttavia possibile utilizzare la sintassi riportata di seguito per fare riferimento alla dichiarazione di non responsabilità globale: -Identity global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto ConferenceDisclaimer</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer. Il cmdlet **Set-CsConferenceDisclaimer** accetta l'input di oggetti dichiarazione di non responsabilità per le conferenze inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsConferenceDisclaimer** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)

