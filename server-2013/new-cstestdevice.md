---
title: New-CsTestDevice
TOCTitle: New-CsTestDevice
ms:assetid: 3d223c5e-b987-4353-9bf7-b247a2bdfa25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425899(v=OCS.15)
ms:contentKeyID: 49300274
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTestDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo dispositivo di test per la gestione degli aggiornamenti dei dispositivi. I dispositivi di test consentono agli amministratori di testare gli aggiornamenti del firmware prima della distribuzione in tutti i dispositivi di un'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsTestDevice -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsTestDevice -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identifier <String> -IdentifierType <MACAddress | SerialNumber> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creato un nuovo dispositivo di test denominato UCPhone per il sito Redmond. Si noti la sintassi utilizzata per specificare l'identità del dispositivo: ambito del dispositivo (site:Redmond) seguito dal carattere / e quindi dal nome del dispositivo (UCPhone). Questo dispositivo utilizza il suo numero di serie (07823-A345) come identificativo (IdentifierType).

    New-CsTestDevice -Identity site:Redmond/UCPhone -IdentifierType SerialNumber -Identifier "07823-A345"

## ESEMPIO 2

Il comando riportato nell'Esempio 2 è una variante del comando riportato nell'Esempio 1. Nell'Esempio 2, però, non viene utilizzato il parametro Identity. Al suo posto, viene utilizzato il parametro Parent per specificare l'ambito del nuovo dispositivo di test (site:Redmond) e il parametro Name per indicare il nome del nuovo dispositivo (UCPhone). Il cmdlet **New-CsTestDevice** utilizzerà i valori di questi due parametri per ricavare automaticamente l'identità del dispositivo di test (site:Redmond/UCPhone).

    New-CsTestDevice -Parent "site:Redmond" -Name UCPhone -IdentifierType SerialNumber -Identifier "07823-A345"

## Descrizione dettagliata

Identificando telefoni specifici compatibili con Lync Phone Edition o altri dispositivi come dispositivi di test, gli amministratori possono verificare e approvare gli aggiornamenti del firmware prima che vengano applicati ai dispositivi pertinenti dell'organizzazione. Dopo l'importazione delle regole di aggiornamento dei dispositivi in Lync Server, queste regole vengono contrassegnate come "in sospeso", ovvero gli aggiornamenti che corrispondono a tali regole non vengono scaricati e installati automaticamente dai dispositivi interessati.

Per contro, tali regole in sospeso vengono scaricate e installate dai dispositivi di test designati. L'idea generale alla base dei dispositivi di test è la seguente: le nuove regole di aggiornamento del dispositivo vengono applicate automaticamente ai dispositivi di test, offrendo agli amministratori la possibilità di verificare che gli aggiornamenti firmware funzionino nel modo appropriato. Se gli aggiornamenti funzionano, gli amministratori possono contrassegnare le regole come approvate; le regole approvate vengono quindi scaricate e installate da tutti i dispositivi pertinenti dell'organizzazione.

I dispositivi di test vengono creati utilizzando il cmdlet **New-CsTestDevice**. Questi dispositivi possono essere configurati nell'ambito globale o del sito.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsTestDevice** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTestDevice"}

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
<td><p><em>Identifier</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>In base al valore di IdentifierType, indica l'indirizzo MAC (Media Access Control) o il numero di serie del nuovo dispositivo di test. I numeri di serie possono essere specificati utilizzando numeri, lettere, trattini e sottolineature ad esempio:</p>
<p>-Identifier &quot;AB37_679e&quot;</p>
<p>Gli indirizzi MAC devono essere specificati sotto forma di sei o più coppie di caratteri; a seconda del tipo di indirizzo MAC, queste coppie di caratteri possono essere unite insieme in una singola stringa oppure essere separate da trattini o due punti. Si noti che l'indirizzo MAC può includere lettere e/o numeri. Ciascuno dei seguenti esempi rappresenta un indirizzo MAC valido:</p>
<p>010203040506</p>
<p>01-02-03-04-05-06</p>
<p>01:02:03:04:05:06</p>
<p>Un indirizzo MAC come 01-02-03-04-05 non può essere accettato poiché non comprende almeno sei coppie di caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>IdentifierType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.IdentifierType</p></td>
<td><p>Indica se il dispositivo di test sarà univocamente identificato tramite il suo indirizzo MAC o il suo numero di serie. Per identificare un dispositivo tramite il suo indirizzo MAC, impostare IdentifierType su MACAddress. Per identificare un dispositivo tramite il suo numero di serie, impostare IdentifierType su SerialNumber. MACAddress e SerialNumber sono i soli valori consentiti.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità per il nuovo dispositivo di test. L'identità è composta dall'ambito a cui è assegnato il dispositivo di test (ad esempio, site:Redmond) e dal nome del nuovo dispositivo (ad esempio, UCPhone). Per assegnare un dispositivo di test denominato UCPhone al sito Redmond, il parametro Identity deve essere impostato nel seguente modo: -Identity &quot;site:Redmond/UCPhone&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome del nuovo dispositivo di test (i nomi devono essere univoci in un dato ambito). Il parametro Name deve essere utilizzato solo quando è specificato il parametro Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'ambito (ad esempio, site:Redmond) a cui verrà assegnato il nuovo dispositivo di test. Se si utilizza il parametro Parent, è necessario specificare anche il parametro Name; ad esempio: -Parent site:Redmond –Name UCPhone. Se si utilizza il parametro Parent, non si deve specificare il parametro Identity e viceversa.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. Il cmdlet **New-CsTestDevice** non accetta input da pipeline.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice.

## Vedere anche

#### Ulteriori risorse

[Get-CsTestDevice](get-cstestdevice.md)  
[Remove-CsTestDevice](remove-cstestdevice.md)  
[Set-CsTestDevice](set-cstestdevice.md)

