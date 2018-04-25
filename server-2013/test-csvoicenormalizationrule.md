---
title: Test-CsVoiceNormalizationRule
TOCTitle: Test-CsVoiceNormalizationRule
ms:assetid: e2d27ce1-883f-4679-a288-f35846842258
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399003(v=OCS.15)
ms:contentKeyID: 49302255
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceNormalizationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica un numero di telefono rispetto a una regola di normalizzazione vocale e restituisce il numero dopo l'applicazione della regola di normalizzazione. Le regole di normalizzazione vocale vengono utilizzate per convertire un requisito di composizione telefonica (ad esempio la necessità di comporre il 9 per accedere a una linea esterna) nel formato per numeri di telefono E.164 utilizzato da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsVoiceNormalizationRule -DialedNumber <PhoneNumber> -NormalizationRule <NormalizationRule>

## Esempi

## ESEMPIO 1

In questo esempio viene eseguito un test di normalizzazione vocale sulla regola di normalizzazione vocale con l'identità "global/11 digit number rule". Viene innanzitutto eseguito il cmdlet **Get-CsVoiceNormalizationRule** per recuperare la regola con valore Identity "global/11 digit number rule". Questo oggetto regola viene quindi inviato tramite pipe al cmdlet **Test-CsVoiceNormalizationRule**, dove la regola viene testata sul numero di telefono 14255559999. l'output corrisponderà al valore DialedNumber che si otterrà dopo l'applicazione della regola di normalizzazione vocale "global/11 digit number rule". Se questa regola non si applica al valore DialedNumber (ad esempio, se la regola di normalizzazione corrisponde a una sequenza per un numero a 11 cifre ma il numero fornito è composto da 7 cifre), non verrà restituito alcun valore.

    Get-CsVoiceNormalizationRule -Identity "global/11 digit number rule" | Test-CsVoiceNormalizationRule -DialedNumber 14255559999

## ESEMPIO 2

l'esempio 2 è identico al precedente, ma anziché inoltrare tramite pipe i risultati dell'operazione Get direttamente al cmdlet Test, l'oggetto viene prima memorizzato nella variabile $a, dopodiché viene passato come valore al parametro NormalizationRule per essere utilizzato come regola di normalizzazione vocale su cui eseguire il test.

    $a = Get-CsVoiceNormalizationRule -Identity "global/11 digit number rule"
    Test-CsVoiceNormalizationRule -DialedNumber 5551212 -NormalizationRule $a

## ESEMPIO 3

In questo esempio viene eseguito un test di normalizzazione vocale su tutte le regole di normalizzazione vocale definite nella distribuzione di Lync Server. Viene innanzitutto eseguito il cmdlet **Get-CsVoiceNormalizationRule** senza alcun parametro per recuperare tutte le regole di normalizzazione vocale. La raccolta di regole restituita viene quindi inviata tramite pipe al cmdlet **Test-CsVoiceNormalizationRule**, dove ogni regola presente nella raccolta viene testata sul numero di telefono 2065559999. l'output sarà un elenco di numeri convertiti, uno per ciascuna regola testata. Se una regola non si applica al valore DialedNumber (ad esempio, se la regola di normalizzazione corrisponde a una sequenza per un numero a 11 cifre ma il numero fornito è composto da 7 cifre), ci sarà una riga vuota nell'elenco per la regola in questione.

    Get-CsVoiceNormalizationRule | Test-CsVoiceNormalizationRule -DialedNumber 2065559999

## Descrizione dettagliata

Questo cmdlet consente di vedere i risultati dell'applicazione di una regola di normalizzazione vocale a un determinato numero di telefono. Le regole di normalizzazione vocali sono una parte obbligatoria dell'autorizzazione telefonica e del routing delle chiamate. Definiscono i requisiti per convertire in un formato standard (E.164) i numeri di telefono in genere composti in un formato diverso dagli utenti. Eseguire questo cmdlet per risolvere problemi di composizione o per verificare che le regole funzionino come previsto utilizzando i numeri specificati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Test-CsVoiceNormalizationRule** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceNormalizationRule"}

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
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>Il numero di telefono su cui si desidera testare la regola di normalizzazione specificata nel parametro NormalizationRule.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>NormalizationRule</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule</p></td>
<td><p>Un oggetto contenente un riferimento alla regola di normalizzazione su cui si desidera testare il numero specificato nel parametro DialedNumber.</p>
<p>Per recuperare le regole di normalizzazione vocale, è possibile chiamare il cmdlet <strong>Get-CsVoiceNormalizationRule</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule. Accetta l'input da pipeline di oggetti regola di normalizzazione vocale.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.NormalizationRuleTestResult.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

