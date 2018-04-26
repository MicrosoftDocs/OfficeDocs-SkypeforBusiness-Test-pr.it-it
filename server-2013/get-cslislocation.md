---
title: Get-CsLisLocation
TOCTitle: Get-CsLisLocation
ms:assetid: aede2266-5af4-4973-9db1-a7b505c62057
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412834(v=OCS.15)
ms:contentKeyID: 49301669
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisLocation

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più posizioni nel database di configurazione delle posizioni per il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLisLocation [-Unreferenced <SwitchParameter>]

## Esempi

## ESEMPIO 1

La chiamata al cmdlet **Get-CsLisLocation** senza parametri restituisce tutte le posizioni definite nel database di configurazione delle posizioni.

    Get-CsLisLocation

## ESEMPIO 2

Il parametro Unreferenced non accetta un valore. È esclusivamente un commutatore che indica al cmdlet **Get-CsLisLocation** di restituire solo le posizioni non associate a una porta, un commutatore, una subnet o un punto di accesso wireless.

    Get-CsLisLocation -Unreferenced

## ESEMPIO 3

Per recuperare posizioni LIS specifiche, è necessario recuperare tutte le posizioni chiamando il cmdlet **Get-CsLisLocation** e quindi inviare tramite pipe tale raccolta di posizioni al cmdlet **Where-Object** per circoscrivere la raccolta alle posizioni specifiche che si stanno cercando. Nell'esempio 3 viene effettuata esattamente questa operazione: vengono utilizzati i cmdlet **Get-CsLisLocation** e **Where-Object** per recuperare tutte le posizioni con proprietà Location uguale alla stringa NorthCampus. Si noti l'utilizzo dell'operatore di confronto -ceq. Questo operatore effettua un confronto con distinzione tra maiuscole e minuscole. In questo caso pertanto verranno restituite solo le posizioni con valori Location uguali a NorthCampus, non northcampus, Northcampus e così via.

    Get-CsLisLocation | Where-Object {$_.Location -ceq "NorthCampus"}

## Descrizione dettagliata

Il servizio E9-1-1 consente a chi risponde alle chiamate di emergenza di determinare la posizione geografica del chiamante senza dovergli richiedere tali informazioni. In Lync Server la posizione viene determinata in base al mapping di porta, subnet, commutatore o punto di accesso wireless del chiamante a una posizione specifica. Questo cmdlet recupera una o più di queste posizioni.

Questo cmdlet è diverso dal cmdlet **Get-CsLisCivicAddress** in quanto oltre a recuperare le informazioni sull'indirizzo, il cmdlet **Get-CsLisLocation** recupera anche il nome della posizione e il nome della società associato alla posizione. Il cmdlet **Get-CsLisCivicAddress** invece recupera solo le informazioni sull'indirizzo.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsLisLocation** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisLocation"}

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
<td><p><em>Unreferenced</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si include questo parametro, verranno recuperate solo le posizioni che non sono state associate a una porta, a una subnet, a un commutatore o a un punto di accesso wireless. In altri termini, se si include questo parametro, verranno recuperate tutte le posizioni create chiamando il cmdlet <strong>Set-CsLisLocation</strong> oppure assegnate a una subnet, a un commutatore, a un punto di accesso wireless o a una porta del server Informazioni di percorso non più esistente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet restituisce uno o più oggetti di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisLocation](remove-cslislocation.md)  
[Set-CsLisLocation](set-cslislocation.md)  
[Get-CsLisCivicAddress](get-csliscivicaddress.md)

