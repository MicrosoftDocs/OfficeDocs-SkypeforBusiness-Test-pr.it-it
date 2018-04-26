---
title: New-CsVoiceRegex
TOCTitle: New-CsVoiceRegex
ms:assetid: a1a498b7-8353-40bd-9c02-424c95743ec3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412751(v=OCS.15)
ms:contentKeyID: 49301511
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceRegex

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea il formato e la conversione di un'espressione regolare per convertire i numeri di telefono in formati diversi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsVoiceRegex -AtLeastLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    New-CsVoiceRegex -ExactLength <Int32> [-DigitsToPrepend <String>] [-DigitsToStrip <Int32>] [-StartsWith <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

In questo esempio vengono creati il formato e la conversione di una nuova espressione regolare. Questa espressione include un formato la cui lunghezza esatta è di 7 cifre (-ExactLength 7) e rimuove le prime tre cifre del numero corrispondente (-DigitsToStrip 3). Il valore Pattern creato da questa espressione regolare è ^\\d{3}(\\d{4})$, mentre il valore Translation è $1. Ad esempio, il numero 5551212 corrisponderebbe al formato e la conversione risultante sarebbe 1212: il numero a 7 cifre senza le prime 3 cifre.

    $regex = New-CsVoiceRegex -ExactLength 7 -DigitsToStrip 3

## ESEMPIO 2

Anche in questo esempio vengono creati il formato e la conversione di una nuova espressione regolare, ma successivamente questi valori vengono utilizzati per creare una nuova regola di normalizzazione vocale. Nella prima riga viene chiamato il cmdlet **New-CsVoiceRegEx** per creare un'espressione regolare il cui numero di corrispondenza deve essere costituito da almeno 7 caratteri (-AtLeastLength 7) e deve iniziare con 1 (-StartsWith "1"). I risultati dell'esecuzione del comando vengono assegnati alla variabile $regex.

Nella seconda riga viene chiamato il cmdlet **New-CsVoiceNormalizationRule**. Alla nuova regola viene assegnato un nome univoco, in questo caso "global/internal rule". Come formato per la regola di normalizzazione viene quindi assegnato il valore Pattern creato tramite la chiamata al cmdlet **New-CsVoiceRegex**: -Pattern $regex.Pattern. Viene eseguita la stessa operazione per la conversione, assegnando il valore Translation creato tramite la chiamata al cmdlet **New-CsVoiceRegex**: -Translation $regex.Translation.

Nota: Il valore Pattern creato in questo esempio è ^(1\\d{5}\\d+)$. Questo valore può essere decifrato come un numero che inizia con 1 (1), seguito da cinque cifre (\\d{5}), che a loro volta sono seguite da un numero qualsiasi di cifre (\\d+). Questo numero si somma a un numero di almeno 7 cifre (1 più 5 più 1 o più) che inizia con 1, ovvero esattamente il numero richiesto.

    $regex = New-CsVoiceRegex -AtLeastLength 7 -StartsWith "1"
    New-CsVoiceNormalizationRule "global/internal rule" -Pattern $regex.Pattern -Translation $regex.Translation

## Descrizione dettagliata

Le espressioni regolari vengono utilizzate per la corrispondenza con i formati di caratteri. In Lync Server le espressioni regolari vengono utilizzate per convertire i numeri di telefono in e da diversi formati, inclusi i numeri composti, E.164 e i formati del centralino locale (PBX) e della rete PSTN (Public Switched Telephone Network). Se non si conoscono le regole di sintassi e di formato delle espressioni regolari, la definizione di queste regole di conversione può risultare complessa. Il cmdlet **New-CsVoiceRegex** fornisce i parametri che consentono di specificare alcuni criteri, quindi genera automaticamente l'espressione regolare.

Utilizzare questo cmdlet per facilitare la generazione di espressioni regolari da utilizzare come valori Pattern e Translation per le regole di normalizzazione (cmdlet **New-CsVoiceNormalizationRule**) e le regole di conversione in uscita (cmdlet **New-CsOutboundTranslationRule**), nonché come valori NumberPattern per le route vocali (cmdlet **New-CsVoiceRoute**).

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsVoiceRegex** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceRegex"}

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
<td><p><em>AtLeastLength</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Lunghezza minima richiesta affinché la stringa, ossia il numero di telefono, corrisponda all'espressione. Ad esempio, se si definisce una regola di normalizzazione che coinvolge solo i numeri di almeno 7 cifre, o caratteri, specificare il valore 7 per questo parametro.</p>
<p>È necessario specificare un valore per questo parametro o per il parametro ExactLength. Non è possibile inserire un valore per entrambi.</p></td>
</tr>
<tr class="even">
<td><p><em>ExactLength</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>La lunghezza della stringa, del numero di telefono, deve corrispondere all'espressione regolare. Ad esempio, se si desidera che la regola di normalizzazione coinvolga unicamente i numeri a 10 cifre, specificare il valore 10 per questo parametro.</p>
<p>È necessario specificare un valore per questo parametro o per il parametro AtLeastLength. Non è possibile inserire un valore per entrambi.</p></td>
</tr>
<tr class="odd">
<td><p><em>DigitsToPrepend</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una stringa in cui sono specificati i caratteri o i numeri da aggiungere all'inizio del numero telefonico. Il valore immesso per questo parametro influisce sul valore Translation, ponendo i caratteri all'inizio del numero corrispondente all'espressione regolare Pattern. Ad esempio, se il numero corrispondente al formato è 5551212 e il valore DigitsToPrepend è 425, il numero convertito sarà 4255551212 (purché non siano state applicate altre conversioni).</p></td>
</tr>
<tr class="even">
<td><p><em>DigitsToStrip</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>La quantità di caratteri da eliminare dall'inizio della stringa, o del numero di telefono. Ad esempio, se viene immesso il numero 2065551212 e il valore DigitsToStrip è 3, il numero verrà convertito in 5551212.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartsWith</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il primo carattere della stringa, o numero di telefono. La stringa non corrisponderà all'espressione regolare a meno che non inizi con la stringa specificata nel parametro StartsWith. Ad esempio, se per StartsWith viene specificato il valore &quot;+1&quot;, solo i numeri che iniziano con +1 corrisponderanno a questo formato e verranno, pertanto, convertiti. Il numero di caratteri presenti nella stringa StartsWith verrà incluso nel totale di ExactLength e AtLeastLenght. Se ad esempio sono stati specificati una lunghezza esatta (ExactLength) pari a 10 e una stringa valore iniziale (StartWith) pari a +1, il numero di telefono corrispondente sarà costituito da 8 caratteri preceduti da +1, per un totale di 10 cifre.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.Voice.OcsVoiceRegex.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[New-CsVoiceRoute](new-csvoiceroute.md)

