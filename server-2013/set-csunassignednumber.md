---
title: Set-CsUnassignedNumber
TOCTitle: Set-CsUnassignedNumber
ms:assetid: e7f52423-58d1-410a-9071-731bde45d3d4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399033(v=OCS.15)
ms:contentKeyID: 49302328
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUnassignedNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un intervallo esistente di numeri non assegnati e le regole di routing applicate a tali numeri. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUnassignedNumber [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> [-Identity <XdsGlobalRelativeIdentity>] [-Instance <PSObject>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] <COMMON PARAMETERS>

    Set-CsUnassignedNumber [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio viene modificato l'intervallo di numeri non assegnati con il nome UNSet1. Al parametro Identity viene innanzitutto passato il valore UNSet1, ovvero il nome dell'intervallo di numeri non assegnati che si desidera modificare. Vengono quindi utilizzati i parametri NumberRangeStart (+14255551000) e NumberRangeEnd (+14255551900) per modificare l'intervallo di numeri non assegnati a cui si applicherà l'operatore automatico o l'annuncio specificato.

    Set-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551900"

## ESEMPIO 2

Nell'esempio viene modificato l'annuncio di tutte le impostazioni dell'intervallo di numeri non assegnati che attualmente presentano un annuncio con la stringa "Welcome" nel nome. Viene innanzitutto chiamato il cmdlet **Get-CsUnassignedNumber** per recuperare tutte le impostazioni dei numeri non assegnati. La raccolta di impostazioni viene quindi inviata tramite pipe al cmdlet **Where-Object**, che circoscrive la raccolta alle sole impostazioni nella cui proprietà AnnouncementName è contenuta (-match) la stringa Welcome. Una volta ottenute, tali impostazioni vengono inviate tramite pipe al cmdlet **Set-CsUnassignedNumber**, dove l'ID del server applicazioni del servizio annunci (ApplicationServer:redmond.litwareinc.com) viene modificato con il parametro AnnouncementService e il nome del nuovo annuncio (Help Desk Announcement) viene modificato con il parametro AnnouncementName. Se il nuovo Annuncio ha un nome diverso ma lo stesso ID del servizio, è necessario specificare l'ID del servizio oltre al nome.

    Get-CsUnassignedNumber | Where-Object {$_.AnnouncementName -match "Welcome"} | Set-CsUnassignedNumber -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Help Desk Announcement"

## Descrizione dettagliata

I numeri non assegnati sono numeri di telefono che sono stati assegnati a un'organizzazione, ma che non sono stati assegnati a utenti o telefoni specifici. Lync Server può essere configurato per instradare le chiamate alle destinazioni appropriate quando viene chiamato un numero non assegnato. Il cmdlet consente di modificare le impostazioni che definiscono tale routing.

Per poter modificare alcune delle impostazioni per il cmdlet, è necessario che nel sistema siano già stati definiti annunci oppure che sia configurato un Operatore automatico di Messaggistica unificata di Exchange. Per determinare se sono presenti annunci, chiamare il cmdlet **Get-CsAnnouncement**. Per creare un nuovo annuncio, chiamare il cmdlet **New-CsAnnouncement**. Per verificare le impostazioni dell'Operatore automatico di Messaggistica unificata di Exchange, eseguire il cmdlet **Get-CsExUmContact**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsUnassignedNumber** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Il nome dell'Annuncio che verrà usato per gestire le chiamate a questo intervallo di numeri.</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Il nome di dominio completo (FQDN) o l'ID del servizio del server degli annunci.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>String</p></td>
<td><p>Il numero di telefono dell'operatore automatico di Messaggistica unificata di Exchange a cui instradare le chiamate comprese nell'intervallo. Il contatto dell'operatore automatico di Messaggistica unificata di Exchange deve essere già configurato per poter assegnare un valore a tale parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome univoco per l'intervallo di numeri non assegnati da modificare.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>DisplayAnnouncementVacantNumberRange</p></td>
<td><p>Un riferimento a un oggetto che contiene le impostazioni dei numeri non assegnati. L'oggetto deve essere di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange e può essere recuperato chiamando il cmdlet <strong>Get-CsUnassignedNumber</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'ultimo numero dell'intervallo di numeri non assegnati. Il valore deve essere maggiore o uguale al numero fornito per NumberRangeStart. Per specificare un intervallo di un numero, utilizzare lo stesso numero per NumberRangeStart e NumberRangeEnd.</p>
<p>Il numero deve corrispondere all'espressione regolare (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Ciò significa che il valore può iniziare con la stringa tel: (se questa non viene specificata, verrà aggiunta automaticamente), un segno più (+) e una cifra compresa tra 1 e 9. Il numero di telefono può contenere fino a 17 cifre e può essere seguito da un interno nel formato ;ext= seguito dal numero dell'interno.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il primo numero nell'intervallo di numeri non assegnati. Il valore deve essere minore o uguale al valore fornito per NumberRangeEnd.</p>
<p>Il numero deve corrispondere all'espressione regolare (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. Ciò significa che il valore può iniziare con la stringa tel: (se questa non viene specificata, verrà aggiunta automaticamente), un segno più (+) e una cifra compresa tra 1 e 9. Il numero di telefono può contenere fino a 17 cifre e può essere seguito da un interno nel formato ;ext= seguito dal numero dell'interno.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Int32</p></td>
<td><p>È possibile sovrapporre intervalli di numeri non assegnati. Se un numero rientra in più di un intervallo, avrà effetto l'intervallo con la priorità più alta.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange. Accetta l'input da pipeline di oggetti numero non assegnato.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange.

## Vedere anche

#### Ulteriori risorse

[New-CsUnassignedNumber](new-csunassignednumber.md)  
[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)

