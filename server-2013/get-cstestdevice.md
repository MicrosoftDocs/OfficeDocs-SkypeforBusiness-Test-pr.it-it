---
title: Get-CsTestDevice
TOCTitle: Get-CsTestDevice
ms:assetid: 4c88d448-4130-40de-b7e9-7389922322f4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398304(v=OCS.15)
ms:contentKeyID: 49300481
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTestDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera informazioni sui dispositivi di test per la gestione degli aggiornamenti dei dispositivi configurati per l'utilizzo nella propria organizzazione. I dispositivi di test consentono agli amministratori di testare gli aggiornamenti del firmware prima di distribuirli in tutti i dispositivi di un'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsTestDevice [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsTestDevice [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituiti tutti i dispositivi di test dell'organizzazione. Chiamando il cmdlet **Get-CsTestDevice** senza alcun parametro aggiuntivo, vengono restituiti tutti i dispositivi di test attualmente in uso.

    Get-CsTestDevice

## ESEMPIO 2

In questo esempio viene restituito il dispositivo di test denominato UCPhone assegnato al sito Redmond.

    Get-CsTestDevice -Identity site:Redmond/UCPhone

## ESEMPIO 3

Nell'Esempio 3, il comando restituisce tutti i dispositivi di test configurati per il sito Redmond.

``` 
Get-CsTestDevice -Identity site:Redmond  
```

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti i dispositivi di test configurati nell'ambito del sito. Per ottenere questo risultato, il comando utilizza il parametro Filter. Il valore di filtro "site:\*" restituisce solo i dati relativi ai dispositivi di test la cui identità (Identity) inizia con il valore "site:".

    Get-CsTestDevice -Filter site:*

## Descrizione dettagliata

Identificando telefoni specifici compatibili con Lync Phone Edition o altri dispositivi come dispositivi di test, gli amministratori possono verificare e approvare gli aggiornamenti del firmware prima che vengano applicati a tutti i dispositivi pertinenti dell'organizzazione. Dopo l'importazione delle regole di aggiornamento dei dispositivi in Lync Server, queste regole vengono contrassegnate come "in sospeso", ovvero gli aggiornamenti che corrispondono a tali regole non vengono scaricati e installati automaticamente dai dispositivi interessati.

Per contro, tali regole in sospeso vengono scaricate e installate dai dispositivi di test designati. Grazie ai dispositivi di test, le nuove regole di aggiornamento del dispositivo vengono applicate automaticamente ai dispositivi di test, offrendo agli amministratori la possibilità di verificare che gli aggiornamenti firmware funzionino nel modo appropriato. Se gli aggiornamenti funzionano, gli amministratori possono contrassegnare le regole come approvate; le regole approvate vengono quindi scaricate e installate da tutti i dispositivi pertinenti dell'organizzazione.

I dispositivi di test possono essere assegnati nell'ambito globale o del sito. È possibile utilizzare il cmdlet **Get-CsTestDevice** per recuperare le informazioni sui dispositivi di test configurati per l'utilizzo nella propria organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsTestDevice** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTestDevice"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare il dispositivo o i dispositivi di test da ottenere. Ad esempio, per ottenere tutte le raccolte di dispositivi di test configurate nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per ottenere tutti i dispositivi che hanno il termine &quot;EMEA&quot; nella loro identità, utilizzare la seguente sintassi: -Filter &quot;*EMEA*&quot;. Si noti che il parametro Filter agisce solo sull'identità della raccolta di dispositivi di test; non è possibile filtrare altre proprietà della raccolta.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità del dispositivo di test da ottenere. Per fare riferimento ad un singolo dispositivo denominato UCPhone e archiviato nella raccolta globale, utilizzare la seguente sintassi: -Identity global/UCPhone. Per ottenere le informazioni su un dispositivo in una raccolta nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond/UCPhone. Per ottenere le informazioni su un'intera raccolta, omettere il nome del dispositivo. Ad esempio, la sintassi seguente restituisce tutti i dispositivi di test configurati per il sito Redmond: -Identity site:Redmond.</p>
<p>Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dei dispositivi di test dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsTestDevice** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsTestDevice** restituisce una o più istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice.

## Vedere anche

#### Ulteriori risorse

[New-CsTestDevice](new-cstestdevice.md)  
[Remove-CsTestDevice](remove-cstestdevice.md)  
[Set-CsTestDevice](set-cstestdevice.md)

