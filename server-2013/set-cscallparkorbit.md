---
title: Set-CsCallParkOrbit
TOCTitle: Set-CsCallParkOrbit
ms:assetid: 9a159a9a-69a6-4e4d-8224-49aa42092ea8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398796(v=OCS.15)
ms:contentKeyID: 49301445
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkOrbit

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Imposta le proprietà di un intervallo di codici orbit del parcheggio di chiamata esistente in un'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsCallParkOrbit [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsCallParkOrbit [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-CallParkService <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NumberRangeEnd <String>] [-NumberRangeStart <String>] [-Type <CallPark | GroupPickup>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio, l'intervallo di numeri per l'orbit del parcheggio di chiamata denominato "Redmond CPO 1" viene modificato e impostato in modo che parta da 500 e arrivi fino a 699. Tutti i valori nell'intervallo devono essere univoci in tutti gli intervalli di orbit del parcheggio di chiamata nell'organizzazione.

    Set-CsCallParkOrbit -Identity "Redmond CPO 1" -NumberRangeStart 500 -NumberRangeEnd 699

## ESEMPIO 2

In questo esempio, l'intervallo di numeri per l'orbit del parcheggio di chiamata denominato "Redmond CPO 2" viene modificato e impostato in modo che parta da \*7000 e arrivi fino a \*7100. Tutti i valori nell'intervallo devono essere univoci in tutti gli intervalli di orbit del parcheggio di chiamata nell'organizzazione. A differenza dell'esempio precedente, i valori assegnati a NumberRangeStart e NumberRangeEnd sono stati racchiusi tra virgolette doppie. Se questi valori iniziano con \* o \# (gli unici valori non numerici ammessi), il valore deve essere racchiuso tra virgolette doppie.

    Set-CsCallParkOrbit -Identity "Redmond CPO 2" -NumberRangeStart "*7000" -NumberRangeEnd "*7100"

## Descrizione dettagliata

Il parcheggio di una chiamata consente di assegnare una telefonata ricevuta a un numero all'interno di un intervallo specifico in modo che sia possibile recuperarla successivamente. Un orbit del parcheggio di chiamata è un set di interni definito a tale scopo. Il cmdlet **Set-CsCallParkOrbit** consente di modificare gli intervalli di numeri e l'ID del servizio Parcheggio di chiamata. Il nuovo intervallo di numeri deve essere univoco in tutti gli orbit del parcheggio di chiamata definiti nell'organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsCallParkOrbit** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkOrbit"}

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
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo (FQDN) o l'ID del servizio dell'applicazione che ospita il applicazione Parcheggio di chiamata. Tutte le chiamate parcheggiate verso numeri nell'intervallo specificato dai parametri NumberRangeStart e NumberRangeEnd saranno instradate a questo server o pool.</p>
<p></p></td>
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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco dell'intervallo di orbit del parcheggio di chiamata da modificare. Se l'identità contiene spazi, questo valore deve essere racchiuso tra virgolette doppie.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>DisplayCallParkOrbit</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro. Questo oggetto deve essere di tipo DisplayCallParkOrbit e può essere recuperato utilizzando il cmdlet <strong>Get-CsCallParkOrbit</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'ultimo numero nell'intervallo per questo orbit del parcheggio di chiamata. Il valore deve essere maggiore o uguale a NumberRangeStart. Inoltre, il valore deve avere la stessa lunghezza del valore di NumberRangeStart. Ad esempio, se NumberRangeStart è impostato su 100, NumberRangeEnd non può essere impostato su 1001. Inoltre se NumberRangeStart inizia con un * o # anche NumberRangeEnd deve iniziare con lo stesso carattere.</p>
<p>Valori validi: devono corrispondere all'espressione regolare ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8}). In pratica, il valore deve essere una stringa che inizia con il carattere * o # oppure con un numero tra 1 e 9 (il primo carattere non può essere uno zero). Se il primo carattere è * o #, il carattere successivo deve essere un numero tra 1 e 9 (non può essere uno zero). I caratteri successivi possono corrispondere a qualsiasi numero tra 0 e 9, con un massimo di sette caratteri aggiuntivi. Ad esempio, &quot;#6000&quot;, &quot;*92000&quot; e &quot;*95551212&quot;. Se il primo carattere non è * o #, il primo carattere deve essere un numero tra 1 e 9 (non può essere zero), seguito da al massimo otto caratteri, ognuno di loro un numero compreso tra 0 e 9. (Ad esempio:</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il primo numero nell'intervallo per questo orbit del parcheggio di chiamata. Il valore deve essere minore o uguale a NumberRangeEnd. Inoltre, il valore deve avere la stessa lunghezza del valore di NumberRangeEnd.</p>
<p>Valori validi: devono corrispondere all'espressione regolare ([\*|#]?[1-9]\d{0,7})|([1-9]\d{0,8}). In pratica, il valore deve essere una stringa che inizia con il carattere * o # oppure con un numero tra 1 e 9 (il primo carattere non può essere uno zero). Se il primo carattere è * o #, il carattere successivo deve essere un numero tra 1 e 9 (non può essere uno zero). I caratteri successivi possono corrispondere a qualsiasi numero tra 0 e 9, con un massimo di sette caratteri aggiuntivi. Ad esempio, &quot;#6000&quot;, &quot;*92000&quot; e &quot;*95551212&quot;. Il numero che segue un * o # deve essere maggiore di 100. Se il primo carattere non è un * o #, il primo carattere deve essere un numero tra 1 e 9 (non può essere zero), seguito da fino 8 caratteri ciascuno un numero da 10 a 9 (ad esempio, 915551212;41212;300.)</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Core.OrbitType</p></td>
<td><p>Specifica il tipo di codice orbit del parcheggio di chiamata. Lync Server 2013 supporta due tipi diversi di codici orbit del parcheggio di chiamata:</p>
<p>CallPark. Questo è il codice orbit standard del parcheggio di chiamata, in base al quale un utente mette una chiamata in attesa e quindi può recuperarla da un altro telefono componendo il numero del parcheggio di chiamata specificato. CallPark è il tipo di codice orbit predefinito che verrà utilizzato se non viene specificato il parametro Type.</p>
<p>GroupPickup. Con la risposta alle chiamate di gruppo, gli utenti possono rispondere a una chiamata in arrivo effettuata a qualsiasi membro del gruppo di risposta alle chiamate di gruppo. I gruppi di risposta alle chiamate di gruppo vengono configurati dagli amministratori.</p>
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

Oggetto Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit. Accetta input tramite pipeline da oggetti orbit del parcheggio di chiamata.

## Tipi restituiti

Questo cmdlet consente di modificare un oggetto di tipo Microsoft.Rtc.Management.Voice.Helpers.DisplayCallParkOrbit.

## Vedere anche

#### Ulteriori risorse

[New-CsCallParkOrbit](new-cscallparkorbit.md)  
[Remove-CsCallParkOrbit](remove-cscallparkorbit.md)  
[Get-CsCallParkOrbit](get-cscallparkorbit.md)

