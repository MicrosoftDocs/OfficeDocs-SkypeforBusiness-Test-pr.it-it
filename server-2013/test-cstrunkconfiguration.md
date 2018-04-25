---
title: Test-CsTrunkConfiguration
TOCTitle: Test-CsTrunkConfiguration
ms:assetid: 07f2ef04-49aa-4857-b213-fa98506c0427
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398137(v=OCS.15)
ms:contentKeyID: 49299592
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsTrunkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Convalida una configurazione trunk rispetto a un numero di telefono. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsTrunkConfiguration -TrunkConfiguration <TrunkConfiguration> [-CallingNumber <PhoneNumber>] [-DialedNumber <PhoneNumber>]

## Esempi

## ESEMPIO 1

In questo esempio viene eseguito un test sulla configurazione trunk definita per il sito Redmond. La prima riga in questo esempio utilizza il cmdlet **Get-CsTrunkConfiguration** per recuperare la configurazione del sito Redmond (la configurazione con Identity site:Redmond). L'oggetto configurazione trunk recuperato viene assegnato alla variabile $tc.

Nella riga 2 viene chiamato il cmdlet **Test-CsTrunkConfiguration**, passando il numero di telefono da testare al parametro DialedNumber, e la configurazione trunk recuperata nella riga 1 (archiviata in $tc) al parametro TrunkConfiguration.

    $tc = Get-CsTrunkConfiguration -Identity Site:Redmond
    Test-CsTrunkConfiguration -DialedNumber 4255551212 -TrunkConfiguration $tc

## Descrizione dettagliata

Utilizzare questo cmdlet per verificare che una configurazione trunk agisca secondo le aspettative nei confronti di un numero telefonico. Ciascuna configurazione contiene impostazioni specifiche che definiscono le relazioni e le possibilità tra Mediation Server e gateway per la rete telefonica pubblica commutata (PSTN), IP-PBX, o Session Border Controller (SBC) al provider di servizi. Queste impostazioni configurano se è attivo un bypass multimediale su questo trunk, se pacchetti RTCP vengono spediti sotto certe condizioni e se è necessaria la crittografia SRTP(secure real-time protocol).

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Test-CsTrunkConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsTrunkConfiguration"}

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
<td><p><em>TrunkConfiguration</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration</p></td>
<td><p>Un riferimento ad un oggetto configurazione trunk rispetto al quale eseguire il test. Per recuperare gli oggetti configurazione trunk è possibile utilizzare il cmdlet <strong>Get-CsTrunkConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>CallingNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>Quando è specificato, restituisce le regole di conversione in uscita corrispondenti per il numero di telefono specificato, ad esempio:</p>
<p>-CallingNumber &quot;tel:+14255551219&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>DialedNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>Il numero di telefono del quale testare la configurazione.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration. Accetta l'input tramite pipeline di un oggetto configurazione trunk.

## Tipi restituiti

Restituisce un valore di tipo Microsoft.Rtc.Management.Voice.TrunkConfigurationTestResult.

## Vedere anche

#### Ulteriori risorse

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)

