---
title: Remove-CsCommonAreaPhone
TOCTitle: Remove-CsCommonAreaPhone
ms:assetid: f2c93bec-4b99-4b69-abe0-d2d9e33dcadd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413016(v=OCS.15)
ms:contentKeyID: 49302441
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCommonAreaPhone

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un telefono di area comune esistente dalla raccolta dei telefoni gestiti mediante Lync Server. I telefoni di area comune sono telefoni posizionati nelle sale d'attesa degli edifici, nelle sale di ritrovo del personale o in altre posizioni in cui possono essere utilizzati da persone diverse e per usi diversi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 elimina il telefono delle aree comuni con nome visualizzato (DisplayName) "Building 14 Lobby". A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsCommonAreaPhone** con il parametro Filter e il valore di filtro "{DisplayName -eq "Building 14 Lobby"}". L'oggetto restituito viene quindi inviato tramite pipe al cmdlet **Remove-CsCommonAreaPhone**, che lo elimina.

    Get-CsCommonAreaPhone -Filter {DisplayName -eq "Building 14 Lobby"} | Remove-CsCommonAreaPhone

## ESEMPIO 2

Nell'esempio 2 il comando elimina tutti i telefoni delle aree comuni a cui non è stato assegnato un dial plan. Questa attività viene eseguita utilizzando innanzitutto il cmdlet **Get-CsCommonAreaPhone** e il parametro Filter per restituire gli elementi specificati. Il valore di filtro {DialPlan -eq $Null} limita i dati restituiti ai telefoni delle aree comuni a cui non è stato assegnato un dial plan. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsCommonAreaPhone**, che elimina ogni telefono presente nella raccolta.

    Get-CsCommonAreaPhone -Filter {DialPlan -eq $Null} | Remove-CsCommonAreaPhone

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i telefoni di area comune con oggetti contatto presenti nell'unità organizzativa Redmond in Active Directory. Per eseguire questa attività, viene innanzitutto chiamato il cmdlet **Get-CsCommonAreaPhone** per restituire tutti i telefoni di area comune con oggetti contatto nell'unità organizzativa Redmond. Il parametro OU e il valore "ou=Redmond,dc=litwareinc,dc=com" del parametro vengono utilizzati per limitare i dati restituiti all'unità organizzativa specificata. La raccolta restituita viene quindi inviata tramite pipe al cmdlet **Remove-CsCommonAreaPhone**, che elimina ogni telefono presente nella raccolta.

    Get-CsCommonAreaPhone -OU "ou=Redmond,dc=litwareinc,dc=com" | Remove-CsCommonAreaPhone

## Descrizione dettagliata

I telefoni delle aree comuni sono telefoni IP non associati a un singolo utente. Anziché trovarsi nell'ufficio di un dipendente, si trovano in genere nelle sale d'attesa dell'edificio, nelle mense, nelle sale di ritrovo del personale, nelle sale riunioni e in altri luoghi in cui è probabile che si riuniscano molte persone. Da un punto di vista della gestione, ciò rappresenta una sfida per gli amministratori, in quanto l'utilizzo del telefono in Lync Server di solito viene controllato mediante criteri vocali e dial plan assegnati a singoli utenti. Ai telefoni delle aree comuni invece non sono assegnati utenti specifici.

Una soluzione a questa sfida consiste nel creare oggetti contatto di Active Directory per tutti i telefoni delle aree comuni. Tali oggetti contatto possono essere creati tramite il **New-CsCommonAreaPhone**. Analogamente agli account utente, è possibile assegnare criteri e piani vocali agli oggetti contatto. Di conseguenza, sarà possibile mantenere il controllo sui telefoni delle aree comuni anche se i telefoni non sono associati a un singolo utente. Ad esempio, per non consentire alle persone il trasferimento o il parcheggio delle chiamate da un telefono delle aree comuni, è possibile creare un criterio vocale che proibisca il trasferimento e il parcheggio delle chiamate e quindi assegnare tale criterio al telefono delle aree comuni. Oppure, in modo più corretto, all'oggetto contatto che rappresenta il telefono delle aree comuni. Ad esempio, con il comando seguente è possibile assegnare il criterio vocale CommonAreaPhoneVoicePolicy a tutti i telefoni delle aree comuni:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

Di tanto in tanto potrebbe essere necessario eliminare l'oggetto contatto associato a un telefono delle aree comuni. Ad esempio, se si rimuove il telefono dalla sala ritrovo del personale, non sarà necessario un oggetto contatto associato al telefono. Il cmdlet **Remove-CsCommonAreaPhone** consente di eliminare i telefoni delle aree comuni. Quando si esegue questo cmdlet, il telefono viene eliminato dall'elenco dei telefoni delle aree comuni restituito dal cmdlet **Get-CsCommonAreaPhone**. L'oggetto contatto associato al telefono verrà inoltre eliminato da Servizi di dominio Active Directory.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsCommonAreaPhone** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Le autorizzazioni per l'esecuzione di questo cmdlet per siti oppure unità organizzative di Active Directory specifiche possono essere assegnate tramite il cmdlet **Grant-CsOUPermission**. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCommonAreaPhone"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificatore univoco per il telefono delle aree comuni. I telefoni delle aree comuni vengono identificati tramite il nome distinto di Active Directory dell'oggetto contatto associato. Per impostazione predefinita, tali telefoni utilizzano un identificatore univoco globale (GUID) come nome comune e pertanto presentano in genere un valore Identity simile alla seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Potrebbe quindi risultare più semplice recuperare i telefoni delle aree comuni utilizzando il cmdlet <strong>Get-CsCommonAreaPhone</strong> e quindi inviare tramite pipe al cmdlet <strong>Remove-CsCommonAreaPhone</strong> gli oggetti restituiti.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact. Il cmdlet **Remove-CsCommonAreaPhone** accetta le istanze da pipeline dell'oggetto telefono delle aree comuni.

## Tipi restituiti

Il cmdlet **Remove-CsCommonAreaPhone** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Set-CsCommonAreaPhone](set-cscommonareaphone.md)

