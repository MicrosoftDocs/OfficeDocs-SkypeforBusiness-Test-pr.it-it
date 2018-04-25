---
title: Set-CsTestDevice
TOCTitle: Set-CsTestDevice
ms:assetid: 0a9fabfc-b0d3-4c94-ae04-0a87f0886db8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398156(v=OCS.15)
ms:contentKeyID: 49299631
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTestDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica uno o più dispositivi di test per la gestione degli aggiornamenti dei dispositivi configurati per l'utilizzo nella propria organizzazione. I dispositivi di test consentono agli amministratori di testare gli aggiornamenti del firmware prima di distribuirli in tutti i dispositivi di un'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsTestDevice [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTestDevice [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identifier <String>] [-IdentifierType <MACAddress | SerialNumber>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene modificata la proprietà Identifier del dispositivo di test denominato UCPhone assegnato al sito Redmond.

    Set-CsTestDevice -Identity site:Redmond/UCPhone -Identifier "09768-ABDR-83295"

## ESEMPIO 2

Il comando riportato nell'Esempio 2 consente anche di modificare il dispositivo di test denominato UCPhone assegnato al sito Redmond. In questo caso, tuttavia, il comando non solo specifica un nuovo Identifier ma assegna anche un nuovo IdentifierType: SerialNumber

    Set-CsTestDevice -Identity site:Redmond/UCPhone -IdentifierType SerialNumber -Identifier "09768-ABDR-83295"

## Descrizione dettagliata

Identificando telefoni specifici che utilizzano Lync Phone Edition o altri dispositivi come dispositivi di test, gli amministratori possono verificare e approvare gli aggiornamenti del firmware prima che vengano applicati a tutti i dispositivi pertinenti dell'organizzazione. Dopo l'importazione delle regole di aggiornamento dei dispositivi in Lync Server, queste regole vengono contrassegnate come "in sospeso", ovvero gli aggiornamenti che corrispondono a tali regole non vengono scaricati e installati automaticamente dai dispositivi interessati.

Per contro, tali regole in sospeso vengono scaricate e installate dai dispositivi di test designati. L'idea generale alla base dei dispositivi di test è la seguente: le nuove regole di aggiornamento del dispositivo vengono applicate automaticamente ai dispositivi di test, offrendo agli amministratori la possibilità di verificare che gli aggiornamenti firmware funzionino nel modo appropriato. Se gli aggiornamenti funzionano, gli amministratori possono contrassegnare le regole come approvate; le regole approvate vengono quindi scaricate e installate da tutti i dispositivi pertinenti dell'organizzazione.

I dispositivi di test vengono creati utilizzando il cmdlet **New-CsTestDevice**. Una volta creato un dispositivo di test, è possibile utilizzare il cmdlet **Set-CsTestDevice** per modificare il valore di Identifier e IdentifierType di quel dispositivo o di qualunque altro dispositivo di test.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsTestDevice** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTestDevice"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identifier</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>In base al valore di IdentifierType, indica l'indirizzo MAC (Media Access Control) o il numero di serie del nuovo dispositivo di test. I numeri di serie possono essere specificati utilizzando numeri, lettere, trattini e sottolineature ad esempio:</p>
<p>-Identifier &quot;AB37_679e&quot;</p>
<p>Gli indirizzi MAC devono essere specificati sotto forma di sei o più coppie di caratteri; a seconda del tipo di indirizzo MAC, queste coppie di caratteri possono essere unite insieme in una singola stringa oppure essere separate da trattini o due punti. Si noti che gli indirizzi MAC possono includere lettere e/o numeri. Ciascuno dei seguenti esempi rappresenta un indirizzo MAC valido:</p>
<p>010203040506</p>
<p>01-02-03-04-05-06</p>
<p>01:02:03:04:05:06</p>
<p>Un indirizzo MAC come 01-02-03-04-05 non può essere accettato poiché non comprende almeno sei coppie di caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>IdentifierType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.IdentifierType</p></td>
<td><p>Indica se il dispositivo di test sarà univocamente identificato tramite il suo indirizzo MAC o il suo numero di serie. Per identificare un dispositivo tramite il suo indirizzo MAC, impostare IdentifierType su MACAddress. Per identificare un dispositivo tramite il suo numero di serie, impostare IdentifierType su SerialNumber. MACAddress e SerialNumber sono i soli valori consentiti.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità del dispositivo di test da modificare. Ad esempio: -Identity site:Redmond/UCPhoneTestDevice. Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto dispositivo di test</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice. Il cmdlet **Set-CsTestDevice** accetta l'input da pipeline dell'oggetto dispositivo di test.

## Tipi restituiti

Il cmdlet **Set-CsTestDevice** non restituisce alcun oggetto o valore. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice.

## Vedere anche

#### Ulteriori risorse

[Get-CsTestDevice](get-cstestdevice.md)  
[New-CsTestDevice](new-cstestdevice.md)  
[Remove-CsTestDevice](remove-cstestdevice.md)

