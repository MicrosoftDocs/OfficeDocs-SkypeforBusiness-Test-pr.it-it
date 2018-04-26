---
title: Get-CsVoiceTestConfiguration
TOCTitle: Get-CsVoiceTestConfiguration
ms:assetid: c23235db-500c-4303-8c75-b4ae341b3807
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412957(v=OCS.15)
ms:contentKeyID: 49301864
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceTestConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno scenario di test utilizzabile per verificare i numeri di telefono rispetto a route e regole specificate. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceTestConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con questo esempio vengono recuperate tutte le impostazioni di configurazione di test vocale.

    Get-CsVoiceTestConfiguration

## ESEMPIO 2

Con questo esempio vengono recuperate tutte le impostazioni di configurazione di test vocale e di ciascuna di esse vengono visualizzati solo i parametri Identity, DialedNumber e ExpectedTranslatedNumber. Le impostazioni restituite dal cmdlet **Get-CsVoiceTestConfiguration** vengono inviate tramite pipe al cmdlet **Select-Object** e l'output viene ristretto alle proprietà Identity, DialedNumber e ExpectedTranslatedNumber.

    Get-CsVoiceTestConfiguration | Select-Object Identity, DialedNumber, ExpectedTranslatedNumber

## ESEMPIO 3

In questo esempio viene utilizzato il parametro Filter per recuperare tutte le impostazioni di configurazione di test vocali con identità che contengono la stringa "test". I caratteri jolly (\*) all'inizio e alla fine del valore di filtro indicano che la stringa "test" può essere posizionata in qualsiasi punto del valore Identity e può essere preceduta o seguita da un numero qualsiasi di caratteri. Ad esempio, il comando potrebbe restituire configurazioni di test vocali con nomi come TestConfig, VoiceNumberTest e VoiceTest1.

    Get-CsVoiceTestConfiguration -Filter *test*

## Descrizione dettagliata

Questo cmdlet recupera la route vocale, l'utilizzo, il dial plan e il criterio vocale rispetto ai quali verificare un numero di telefono specifico. Prima di implementare route vocali e criteri vocali, è opportuno testarli su diversi numeri di telefono per garantire che i risultati siano quelli previsti. È possibile eseguire questa verifica recuperando una configurazione di test con questo cmdlet e quindi eseguendo tale scenario con il cmdlet **Test-CsVoiceConfiguration**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsVoiceTestConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceTestConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro fornisce un modo per effettuare una ricerca con caratteri jolly delle configurazioni di test vocali definite. Per informazioni dettagliate, vedere gli esempi più avanti in questo argomento.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Una stringa che identifica in modo univoco la configurazione di test che si desidera recuperare.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la configurazione del test vocale dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Restituisce uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)

