---
title: Remove-CsLisPort
TOCTitle: Remove-CsLisPort
ms:assetid: b8a648af-1064-4a1e-8462-f267b7b72be1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412899(v=OCS.15)
ms:contentKeyID: 49301765
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisPort

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un'associazione tra una porta del server Informazioni percorso e una posizione. Tale associazione viene utilizzata in un'implementazione di VoIP aziendale con il servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) per notificare a un operatore dei servizi di emergenza la posizione del chiamante. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsLisPort -ChassisID <String> -PortID <String> -PortIDSubType <InterfaceAlias | InterfaceName | LocallyAssigned> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene rimossa la porta LIS con indirizzo MAC (ChassisID) 99-99-99-99-99-99, PortID 4200 e PortIDSubType 1. Si noti che un valore PortIDSubType pari a 1 si converte in un valore di InterfaceAlias. Questo parametro e valore può anche essere immesso come segue: -PortIDSubType InterfaceAlias

Se questa porta è stata associata a una posizione, tale posizione non verrà rimossa. Verrà rimossa solo la porta dal mapping della posizione.

    Remove-CsLisPort -ChassisID 99-99-99-99-99-99 -PortID 4200 -PortIDSubType 1

## ESEMPIO 2

In questo esempio vengono rimosse tutte le posizioni delle porte che non hanno un numero civico. L'esempio inizia con una chiamata al cmdlet **Get-CsLisPort**, che restituisce una raccolta di tutte le porte LIS. La raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che trova tutti gli elementi della raccolta con proprietà HouseNumber vuota, ovvero una proprietà HouseNumber uguale a (-eq) una stringa vuota (""). Questa raccolta di posizioni di porte con proprietà HouseNumber vuota viene infine inviata tramite pipe al cmdlet **Remove-CsLisPort**, che rimuove ogni elemento della raccolta.

Analogamente all'esempio 1, non viene rimossa alcuna posizione dal database di configurazione delle posizioni. Vengono rimosse solo le porte che fanno riferimento a tali posizioni. In questo caso, ciò significa che saranno presenti posizioni non valide (non valide poiché HouseNumber è una proprietà richiesta per una posizione) nel database delle posizioni che devono essere rimosse. È possibile rimuovere le posizioni chiamando il cmdlet **Remove-CsLisLocation**.

    Get-CsLisPort | Where-Object {$_.HouseNumber -eq ""} | Remove-CsLisPort

## Descrizione dettagliata

La funzionalità per le chiamate di emergenza consente a un operatore di servizi di emergenza di identificare la posizione del chiamante senza doverla richiedere a quest'ultimo. Nel caso in cui la chiamata venga effettuata tramite connessione VoIP (Voice over Internet Protocol), questa informazione deve essere estratta in base a diversi fattori di connessione. L'amministratore VoIP deve configurare una mappa di posizioni (detta mappa reticolare) che permetta di determinare la posizione di un chiamante. Questo cmdlet rimuove un'associazione tra una posizione fisica e una porta attraverso la quale verranno instradate le chiamate rimuovendo la porta dal database di configurazione delle posizioni.

La rimozione di una posizione di porta non comporta la rimozione della posizione effettiva della porta. Viene rimossa solo la porta. Per rimuovere la posizione, chiamare il cmdlet **Remove-CsLisLocation**. La rimozione della porta inoltre non comporterà la rimozione del commutatore con il valore ChassisID specificato. Per rimuovere il commutatore, sarà necessario chiamare il cmdlet **Remove-CsLisSwitch**.

Se si tenta di rimuovere una porta che non esiste, non verrà effettuata alcuna azione e non si riceverà alcun errore o messaggio di avviso.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsLisPort** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisPort"}

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
<td><p><em>ChassisID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo MAC (Media Access Control) del commutatore della porta. Questo valore presenta il formato nn-nn-nn-nn-nn-nn, ad esempio, 12-34-56-78-90-ab.</p></td>
</tr>
<tr class="even">
<td><p><em>PortID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>ID della porta da rimuovere.</p></td>
</tr>
<tr class="odd">
<td><p><em>PortIDSubType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Lis.PortIDSubType</p></td>
<td><p>Sottotipo della porta da rimuovere. Questo valore può essere immesso come valore numero o stringa ma deve essere un sottotipo valido. I sottotipi validi sono:</p>
<p>1: InterfaceAlias</p>
<p>5: InterfaceName</p>
<p>7: LocallyAssigned</p></td>
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

Accetta l'input da pipeline di oggetti porta LIS.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuovere un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Set-CsLisPort](set-cslisport.md)  
[Get-CsLisPort](get-cslisport.md)  
[Remove-CsLisLocation](remove-cslislocation.md)  
[Remove-CsLisSwitch](remove-cslisswitch.md)

