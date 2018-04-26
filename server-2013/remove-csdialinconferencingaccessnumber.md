---
title: Remove-CsDialInConferencingAccessNumber
TOCTitle: Remove-CsDialInConferencingAccessNumber
ms:assetid: a6d5a6f4-5ad1-4253-b1c4-27f81851046f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412782(v=OCS.15)
ms:contentKeyID: 49301566
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDialInConferencingAccessNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un numero di accesso esistente per le conferenze telefoniche con accesso esterno. Tali conferenze consentono agli utenti di utilizzare un "normale" telefono o cellulare, ovvero un dispositivo sulla rete PSTN (Public Switched Telephone Network), per partecipare alla parte audio di una conferenza. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDialInConferencingAccessNumber -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 elimina il numero di accesso per le conferenze telefoniche con accesso esterno con Identity sip:RedmondDialIn@litwareinc.com.

    Remove-CsDialInConferencingAccessNumber -Identity sip:RedmondDialIn@litwareinc.com

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i numeri gratuiti di accesso alle conferenze telefoniche con accesso esterno, ovvero tutti i numeri con LineUri che inizia con "tel:+1800". A tale scopo, nel comando vengono utilizzati il cmdlet **Get-CsDialInConferencingAccessNumber** e il parametro Filter per restituire una raccolta di tutti i numeri di accesso gratuiti configurati per l'utilizzo nell'organizzazione. Il valore di filtro {LineUri -like "tel:+1800\*"} circoscrive i dati restituiti limitandoli ai numeri in cui la proprietà LineUri inizia con il valore stringa "tel:+1800". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsDialInConferencingAccessNumber**, che elimina tutti i numeri della raccolta.

    Get-CsDialInConferencingAccessNumber -Filter {LineUri -like "tel:+1800*"} | Remove-CsDialInConferencingAccessNumber

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i numeri di accesso per le conferenze telefoniche con accesso esterno dell'area Redmond. A tale scopo, vengono chiamati innanzitutto il cmdlet **Get-CsDialInConferencingAccessNumber** e il parametro Region per restituire una raccolta di tutti i numeri di accesso dell'area Redmond, ovvero tutti i numeri di accesso che includono Redmond nel rispettivo elenco delle aree. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsDialInConferencingAccessNumber**, che elimina tutti i numeri di accesso della raccolta.

    Get-CsDialInConferencingAccessNumber -Region "Redmond" | Remove-CsDialInConferencingAccessNumber

## ESEMPIO 4

Nell'esempio 4 vengono eliminati tutti i numeri di accesso per le conferenze telefoniche con accesso esterno non associati a un'area. A tale scopo, viene chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** insieme al parametro Region e al valore di parametro $Null. In questo modo viene restituita una raccolta di numeri di accesso con proprietà Region vuota. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsDialInConferencingAccessNumber**, che elimina tutti i numeri della raccolta.

    Get-CsDialInConferencingAccessNumber -Region $Null | Remove-CsDialInConferencingAccessNumber

## ESEMPIO 5

Il comando mostrato nell'esempio 5 elimina tutti i numeri di accesso per le conferenze telefoniche con accesso esterno in cui la lingua principale non è impostata sull'italiano. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** senza alcun parametro per restituire una raccolta di tutti i numeri di accesso alle conferenze telefoniche con accesso esterno configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti i numeri con proprietà PrimaryLanguage diversa da "it-IT" (italiano). La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsDialInConferencingAccessNumber**, che elimina tutti i numeri di accesso della raccolta.

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -ne "it-IT"} | Remove-CsDialInConferencingAccessNumber

## ESEMPIO 6

Nell'esempio 6 viene eliminato il numero di accesso alle conferenze telefoniche con accesso esterno con nome visualizzato "Default Dial-In Access Number". A tale scopo, viene chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** insieme al parametro Filter e al valore di filtro {DisplayName -eq "Default Dial-In Access Number"}. Il valore di filtro circoscrive i dati restituiti limitandoli al numero di accesso con proprietà DisplayName uguale a "Default Dial-In Access Number". L'oggetto restituito viene quindi inviato tramite pipe al cmdlet **Remove-CsDialInConferencingAccessNumber**, che elimina il numero di accesso corrispondente.

    Get-CsDialInConferencingAccessNumber -Filter {DisplayName -eq "Default Dial-In Access Number"} | Remove-CsDialInConferencingAccessNumber

## Descrizione dettagliata

Le conferenze telefoniche con accesso esterno consentono agli utenti di utilizzare qualsiasi tipo di telefono, ad esempio una linea terrestre standard, un telefono cellulare o un telefono VoIP, per partecipare alla parte audio di una conferenza. In questo modo è possibile partecipare alla riunione anche non disponendo di un computer o di una connessione Internet. Gli utenti dispongono delle funzionalità audio complete: possono parlare con altri partecipanti e ascoltare tutto. Non sono invece in grado di visualizzare diapositive condivise, trasmissioni video o altri elementi visivi.

Per offrire agli utenti le funzionalità di conferenza telefonica con accesso esterno, è necessario creare numeri di accesso alle conferenze telefoniche con accesso esterno, ovvero numeri telefonici che gli utenti chiamano per connettersi a una riunione. I numeri di accesso alle conferenze telefoniche con accesso esterno vengono creati utilizzando il cmdlet **New-CsDialInConferencingAccessNumber**. Quando si crea un nuovo numero di accesso alle conferenze telefoniche con accesso esterno, si crea in realtà un nuovo oggetto contatto in Servizi di dominio Active Directory. L'oggetto contatto viene utilizzato per rappresentare il numero di accesso e tutte le relative proprietà. Il cmdlet **Remove-CsDialInConferencingAccessNumber** consente di eliminare qualunque numero di accesso alle conferenze telefoniche con accesso esterno creato tramite il cmdlet **New-CsDialInConferencingAccessNumber**. Se si esegue il cmdlet **Remove-CsDialInConferencingAccessNumber**, non viene eliminato solo il numero dalla raccolta di numeri di accesso alle conferenze telefoniche con accesso esterno, ma anche l'oggetto contatto Active Directory che rappresenta tale numero.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsDialInConferencingAccessNumber** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDialInConferencingAccessNumber"}

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
<td><p>L'indirizzo SIP del numero di accesso alle conferenze telefoniche con accesso esterno (ovvero l'oggetto contatto che rappresenta tale numero) da rimuovere. È necessario includere il prefisso sip: quando si specifica il valore Identity, ad esempio -Identity &quot;sip:RedmondDialIn@litwareinc.com&quot;.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.AccessNumber. Il cmdlet **Remove-CsDialInConferencingAccessNumber** accetta l'input da pipeline dell'oggetto numero di accesso.

## Tipi restituiti

Il cmdlet **Remove-CsDialInConferencingAccessNumber** elimina le istanze dell'oggetto Microsoft.Rtc.Management.Xds.AccessNumber.

## Vedere anche

#### Ulteriori risorse

[Get-CsDialInConferencingAccessNumber](get-csdialinconferencingaccessnumber.md)  
[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

