---
title: Test-CsDialPlan
TOCTitle: Test-CsDialPlan
ms:assetid: e6618394-82c5-4bc2-85cc-97ac4686a1aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399024(v=OCS.15)
ms:contentKeyID: 49302291
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsDialPlan

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica un numero di telefono rispetto a un dial plan (precedentemente noto come profilo località) e restituisce la regola di normalizzazione che verrà applicata al numero, nonché il numero convertito dopo l'applicazione della regola di normalizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsDialPlan -DialedNumber <PhoneNumber> -Dialplan <LocationProfile>

## Esempi

## ESEMPIO 1

Questo esempio esegue un test sul dial plan con il sito Identity:Redmond. Per prima cosa il cmdlet **Get-CsDialPlan** viene eseguito per recuperare il dial plan con il sito Identity:Redmond. Quell'oggetto dial plan viene quindi inviato tramite pipe al cmdlet **Test-CsDialPlan**, in cui il dial plan è testato sul numero di telefono 14255559999. Dopo l'applicazione di una regola di normalizzazione voce con un motivo corrispondente, l'output sarà DialedNumber. Se all'interno del sito ci sono più regole di normalizzazione con motivo corrispondente, verrà applicata la regola con il valore Priority più basso. Se non si rilevano regole con motivi che corrispondo al valore DialedNumber (ad esempio, se la regola di normalizzazione corrisponde al motivo per un numero a 11 cifre e viene fornito un numero a 7 cifre), non verrà restituito alcun valore.

L'output di questo comando include un numero di telefono e una regola di normalizzazione. La regola di normalizzazione presenta numerose proprietà e per impostazione predefinita l'output verrà interrotto con i puntini di sospensione (...). Per visualizzare tutte le proprietà e i valori della regola di normalizzazione vocale restituita, l'output viene inviato tramite pipe al cmdlet **Format-List** prima di essere visualizzato. Questo elencherà i numeri di telefono e le regole di normalizzazione su righe separate e le proprietà e i valori delle regole di normalizzazione verranno visualizzate con il ritorno a capo automatico per l'adattamento allo schermo.

    Get-CsDialPlan -Identity site:Redmond | Test-CsDialPlan -DialedNumber 14255559999 | Format-List

## ESEMPIO 2

L'esempio 2 è identico all'esempio 1, tranne per il fatto che invece di inviare tramite pipe i risultati dell'operazione Get direttamente al cmdlet **Test-CsDialPlan** l'oggetto viene prima memorizzato nella variabile $a e successivamente viene passato come valore al parametro DialPlan per essere utilizzato come configurazione di test.

Come nell'esempio 1, il comando viene concluso inviando tramite pipe l'output al cmdlet **Format-List** per visualizzare ulteriori informazioni sulla regola di normalizzazione vocale visualizzata per impostazione predefinita.

    $a = Get-CsDialPlan -Identity site:Redmond
    Test-CsDialPlan -DialedNumber 14255559999 -Dialplan $a | Format-List

## ESEMPIO 3

Questo esempio esegue un test dial plan su tutti i dial plan definiti all'interno della distribuzione Lync Server. Per prima cosa il cmdlet **Get-CsDialPlan** viene eseguito (senza parametri) per recuperare tutti i dial plan. La raccolta dei dial plan restituita viene quindi inviata tramite pipe al cmdlet **Test-CsDialPlan**, dove ogni dial plan della raccolta viene testato con il numero di telefono 2065559999. L'output conterrà un elenco di numero convertiti e la regola di normalizzazione vocale applicata, una per ogni dial plan della raccolta. Se al valore DialedNumber di un dial plan specifico non è applicabile alcuna regola di normalizzazione vocale (ad esempio, se la regola di normalizzazione corrisponde al modello per un numero a 11 cifre e il numero fornito è composto invece da 7 cifre), comparirà una riga vuota nell'elenco relativo a quel dial plan.

Per impostazione predefinita, l'output interrompe la visualizzazione completa della regola di normalizzazione vocale applicata. Negli esempi 1 e 2 era possibile vedere l'intero output inviando tramite pipe i risultati del test al cmdlet **Format-List**. In questo esempio, l'output viene inviato tramite pipe al cmdlet **Format-Table** e contiene il parametro Wrap. Ogni voce viene visualizzata in formato tabellare (una colonna per il numero convertito e una per la regola di normalizzazione vocale applicata), tuttavia con il ritorno a capo dell'output la regola di normalizzazione vocale ritornerà a capo automaticamente all'interno della colonna.

    Get-CsDialPlan | Test-CsDialPlan -DialedNumber 2065559999 | Format-Table -Wrap

## Descrizione dettagliata

Questo cmdlet consente di vedere i risultati dell'applicazione di un dial plan a un dato numero di telefono. I dial plan forniscono le informazioni necessarie, incluse quelle relative a come le regole di normalizzazione vengono applicate, per consentire agli utenti di VoIP aziendale di effettuare chiamate telefoniche. Specificando un numero di composizione e un dial plan, questo cmdlet verificherà quale regola di normalizzazione del dial plan verrà applicata e quale sarà il numero convertito.

È possibile utilizzare questo cmdlet per risolvere i problemi relativi alle conversioni dei numeri o per verificare l'applicazione delle regole su alcuni numeri.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Test-CsDialPlan** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsDialPlan"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PhoneNumber</p></td>
<td><p>Il numero di telefono sul quale si desidera testare il dial plan specificato nel parametro Dialplan.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>LocationProfile</p></td>
<td><p>Un oggetto contenente un riferimento al dial plan su cui si desidera testare il numero specificato nel parametro DialedNumber.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile. Accetta l'input da pipeline di oggetti dial plan.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.LocationProfileTestResult.

## Vedere anche

#### Ulteriori risorse

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)

