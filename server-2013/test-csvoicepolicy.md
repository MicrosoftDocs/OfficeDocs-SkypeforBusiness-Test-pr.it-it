---
title: Test-CsVoicePolicy
TOCTitle: Test-CsVoicePolicy
ms:assetid: 4d631e36-3a9d-4ca2-913f-8c9f4e93183d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398310(v=OCS.15)
ms:contentKeyID: 49300493
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoicePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica un numero di telefono rispetto a un criterio vocale e determina la route vocale utilizzata da tale criterio per il numero. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsVoicePolicy -TargetNumber <PhoneNumber> -VoicePolicy <VoicePolicy> [-Force <SwitchParameter>] [-RouteSettings <PstnRoutingSettings>]

## Esempi

## ESEMPIO 1

Questo esempio esegue un test sui criteri vocali del sito Identity:Redmond. Per prima cosa viene eseguito il cmdlet **Get-CsVoicePolicy** per recuperare i criteri con Identity site:Redmond. Tale oggetto criterio viene inviato tramite pipe al cmdlet **Test-CsVoicePolicy** che verifica il criterio per il numero telefonico +14255559999. L'output sarà la prima route (basata sulla proprietà Priority della route) con un formato numerico corrispondente al valore di TargetNumber ed un utilizzo telefonico che corrisponde a quello specificato nel criterio. Se non viene trovata una route corrispondente (ad esempio, se il formato del numero corrisponde ad un formato numero di 11 cifre e si fornisce un numero a 7 cifre) verrà restituito un valore nullo.

    Get-CsVoicePolicy -Identity site:Redmond | Test-CsVoicePolicy -TargetNumber "+14255559999"

## ESEMPIO 2

L'esempio 2 è identico all'esempio 1, tranne per il fatto che, invece di inviare tramite pipe i risultati dell'operazione Get direttamente al cmdlet **Test-CsVoicePolicy**, l'oggetto viene prima archiviato nella variabile $a e successivamente viene passato come valore al parametro VoicePolicy per essere utilizzato come criterio per cui viene eseguito il test.

    $a = Get-CsVoicePolicy -Identity site:Redmond
    Test-CsVoicePolicy -TargetNumber "+14255559999" -VoicePolicy $a

## ESEMPIO 3

In questo esempio viene eseguito un test criteri vocali su tutti i criteri vocali definiti nella distribuzione di Lync Server. Viene eseguito innanzitutto il cmdlet **Get-CsVoicePolicy** (senza parametri) per restituire tutti i criteri vocali. La raccolta di criteri viene inviata tramite pipe al cmdlet **Test-CsVoicePolicy**, che ricerca in ogni criterio della raccolta una route che soddisfa il requisiti del numero di telefono di destinazione fornito (+12065559999) e dell'utilizzo del telefono. L'output sarà un elenco di route corrispondenti insieme all'utilizzo del telefono di cui si è verificata la corrispondenza.

    Get-CsVoicePolicy | Test-CsVoicePolicy -TargetNumber "+12065559999"

## Descrizione dettagliata

I criteri vocali sono legati alle route vocali tramite utilizzi PSTN (Public Switched Telephone Network). Una chiamata da un utente al quale sono stati assegnati particolari criteri vocali può essere inviata solo su una route in cui è disponibile un utilizzo PSTN corrispondente all'utilizzo nel criterio e con un formato del numero corrispondente al numero composto. Chiamare il cmdlet **Test-CsVoicePolicy** per determinare quale route verrà eventualmente utilizzata per instradare una chiamata proveniente da un utente con particolari criteri vocali, nonché quale utilizzo del telefono lega il criterio alla rete.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Test-CsVoicePolicy** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoicePolicy"}

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
<td><p><em>TargetNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PhoneNumber</p></td>
<td><p>Il numero di telefono su cui eseguire il test. Questo numero deve essere nel formato E.164 (come +14255551212).</p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>VoicePolicy</p></td>
<td><p>Un riferimento ad un oggetto criterio vocale rispetto al quale eseguire il test. Per recuperare gli oggetti criterio vocale è possibile utilizzare il cmdlet <strong>Get-CsVoicePolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Impostazioni della route sulla quale eseguire il test. Le impostazioni della route può essere recuperata utilizzando il cmdlet <strong>Get-CsRoutingConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy. Accetta input tramite pipeline da oggetti criterio vocale.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.VoicePolicyTestResult.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)

