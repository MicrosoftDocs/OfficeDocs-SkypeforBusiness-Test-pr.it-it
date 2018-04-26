---
title: New-CsCallParkOrbit
TOCTitle: New-CsCallParkOrbit
ms:assetid: d65a000f-905d-4512-b082-066748719f4c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398936(v=OCS.15)
ms:contentKeyID: 49302128
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCallParkOrbit

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo intervallo denominato di numeri assegnati per parcheggiare le chiamate all'interno di un'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsCallParkOrbit -Identity <XdsGlobalRelativeIdentity> -CallParkService <String> -NumberRangeEnd <String> -NumberRangeStart <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Type <CallPark | GroupPickup>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene creato un nuovo orbit del parcheggio di chiamata denominato "Redmond CPO 1" nel server applicazioni con ID servizio ApplicationServer:pool0.litwareinc.com. L'intervallo di numeri disponibile per questo orbit del parcheggio di chiamata è compreso tra 100 e 199.

    New-CsCallParkOrbit -Identity "Redmond CPO 1" -NumberRangeStart 100 -NumberRangeEnd 199 -CallParkService ApplicationServer:pool0.litwareinc.com

## ESEMPIO 2

Questo esempio crea un nuovo orbit del parcheggio di chiamata denominato "Redmond CPO 2" nel server applicazioni Parcheggio di chiamata con FQDN pool0.litwareinc.com. La serie disponibile per questo orbit del parcheggio di chiamata è compresa tra \*1000 e \*1999.

    New-CsCallParkOrbit -Identity "Redmond CPO 2" -NumberRangeStart "*1000" -NumberRangeEnd "*1999" -CallParkService pool0.litwareinc.com

## ESEMPIO 3

In questo esempio viene creato un nuovo intervallo dell'orbit del parcheggio di chiamata denominato "Redmond CPO 3" nel server applicazioni del parcheggio di chiamata con ID servizio ApplicationServer:redmond.litwareinc.com. L'intervallo disponibile per questo orbit del parcheggio di chiamata è compreso tra \#1000 e \#1999.

    New-CsCallParkOrbit -Identity "Redmond CPO 3" -NumberRangeStart "#1000" -NumberRangeEnd "#1999"  -CallParkService ApplicationServer:redmond.litwareinc.com

## Descrizione dettagliata

Il parcheggio di chiamata consente di assegnare una telefonata ricevuta a un numero specifico per recuperarla in seguito. L'intervallo di un orbit del parcheggio di chiamata è l'insieme delle posizioni per il parcheggio di chiamata assegnate a uno specifico servizio di parcheggio di chiamata per questo scopo. Il cmdlet **New-CsCallParkOrbit** definisce i numeri per l'intervallo di un orbit del parcheggio di chiamata e li applica a un servizio specifico. Le chiamate parcheggiate all'interno dell'intervallo dato verranno parcheggiate nel servizio di parcheggio di chiamata specificato. È possibile creare più orbit del parcheggio di chiamata. Ogni orbit deve avere un nome univoco e una serie di numeri univoca definiti globalmente.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsCallParkOrbit** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCallParkOrbit"}

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
<td><p><em>CallParkService</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo o l'ID del servizio dell'applicazione che ospita applicazione Parcheggio di chiamata. Tutte le chiamate parcheggiate nei numeri della serie specificata dai parametri NumberRangeStart e NumberRangeEnd saranno instradate a questo server o pool.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome dell'intervallo dell'orbit del parcheggio di chiamata. Questo nome deve essere univoco all'interno della distribuzione di Lync Server. La stringa può corrispondere a un valore qualsiasi, ma dovrebbe consentire facilmente l'identificazione dell'intervallo dell'orbit del parcheggio di chiamata in questione. Tutti gli intervalli degli orbit del parcheggio di chiamata vengono creati con un ambito globale.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'ultimo numero nella serie per questo orbit del parcheggio di chiamata. Il valore deve essere maggiore o uguale a NumberRangeStart. Inoltre, il valore deve avere la stessa lunghezza del valore di NumberRangeStart. Se ad esempio NumberRangeStart è impostato su 100, NumberRangeEnd non può essere impostato su 1001. Inoltre, se NumberRangeStart inizia con * o #, NumberRangeEnd deve iniziare con lo stesso carattere.</p>
<p>Valori validi: devono corrispondere all'espressione regolare ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8}). In pratica, il valore deve essere una stringa che inizia con il carattere * o # oppure con un numero tra 1 e 9 (il primo carattere non può essere uno zero). Se il primo carattere è * o #, il carattere successivo deve essere un numero tra 1 e 9 (non può essere uno zero). I caratteri successivi possono corrispondere a qualsiasi numero tra 0 e 9, con un massimo di sette caratteri aggiuntivi. Ad esempio, #6000, *92000 e *95551212. Se il primo carattere non è * o #, esso deve essere un numero tra 1 e 9 (non può essere zero), seguito da un massimo otto caratteri compresi tra 0 e 9. Ad esempio, 915551212;41212;300.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il primo numero nella serie per questo orbit del parcheggio di chiamata. Il valore deve essere minore o uguale a NumberRangeEnd. Inoltre, il valore deve avere la stessa lunghezza del valore di NumberRangeEnd.</p>
<p>Valori validi: devono corrispondere all'espressione regolare ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8}). In pratica, il valore deve essere una stringa che inizia con il carattere * o # oppure con un numero tra 1 e 9 (il primo carattere non può essere uno zero). Se il primo carattere è * o #, il carattere successivo deve essere un numero tra 1 e 9 (non può essere uno zero). I caratteri successivi possono corrispondere a qualsiasi numero tra 0 e 9, con un massimo di sette caratteri aggiuntivi. Ad esempio, #6000, *92000 e *95551212. Il numero dopo il simbolo * o # deve essere maggiore di 100. Se il primo carattere non è * o #, esso deve essere un numero tra 1 e 9 (non può essere zero), seguito da un massimo di otto caratteri compresi tra 0 e 9. Ad esempio, 915551212;41212;300.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Core.OrbitType</p></td>
<td><p>Specifica il codice orbit del parcheggio di chiamata da creare. In Lync Server 2013 sono consentiti due diversi tipi di codice orbit del parcheggio di chiamata:</p>
<p>CallPark. Questo è il codice orbit del parcheggio di chiamata standard, con il quale un utente può mettere in attesa una chiamata e quindi recuperarla da qualsiasi telefono componendo il numero specificato per il parcheggio di chiamata. CallPark è il tipo di codice orbit predefinito e verrà utilizzato nel caso non venga specificato il parametro Type.</p>
<p>GroupPickup. Con la risposta di gruppo, gli utenti possono rispondere a qualsiasi chiamata in arrivo diretta a uno dei membri del gruppo di risposta alle chiamate di gruppo. I gruppi di risposta alle chiamate di gruppo vengono configurati dagli amministratori.</p>
<p>Per specificare un tipo di codice orbit del parcheggio di chiamata, utilizzare una sintassi simile alla seguente:</p>
<p>-Type GroupPickup</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
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

Nessuno.

## Tipi restituiti

Questo cmdlet crea un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit.

## Vedere anche

#### Ulteriori risorse

[Remove-CsCallParkOrbit](remove-cscallparkorbit.md)  
[Set-CsCallParkOrbit](set-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

