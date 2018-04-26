---
title: Remove-CsTestDevice
TOCTitle: Remove-CsTestDevice
ms:assetid: 995111e0-2ab2-49a1-83f0-fc873f5b5426
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398790(v=OCS.15)
ms:contentKeyID: 49301416
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTestDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il dispositivo di test per la gestione degli aggiornamenti dei dispositivi specificato. I dispositivi di test consentono agli amministratori di testare gli aggiornamenti del firmware prima della distribuzione in tutti i dispositivi di un'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsTestDevice -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono rimossi tutti i dispositivi di test dal sito Redmond. Questa operazione rimuove la raccolta di dispositivi, nonché i singoli dispositivi di test.

    Remove-CsTestDevice -Identity site:Redmond

## ESEMPIO 2

Il comando mostrato nell'esempio 2 rimuove tutti i dispositivi di test configurati per l'utilizzo nell'organizzazione. A tale scopo, viene utilizzato il cmdlet **Get-CsTestDevice** per restituire tutte le raccolte di dispositivi di test e quindi tutti questi elementi vengono inviati tramite pipe al cmdlet **Remove-CsTestDevice**. Si noti che non è possibile rimuovere la raccolta globale di dispositivi di test. Questo comando tuttavia eliminerà tutti i singoli dispositivi di test configurati a livello globale.

    Get-CsTestDevice | Remove-CsTestDevice

## ESEMPIO 3

Nell'esempio 3 vengono rimossi tutti i dispositivi di test configurati nell'ambito del sito. A tale scopo, vengono utilizzati il cmdlet **Get-CsTestDevice** e il parametro Filter per restituire tutti i dispositivi di test con valore Identity che inizia con il valore stringa "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsTestDevice**, che elimina tutti gli elementi della raccolta.

    Get-CsTestDevice -Filter "site:" | Remove-CsTestDevice

## ESEMPIO 4

Il comando mostrato nell'esempio 4 elimina tutti i dispositivi di test LG-Nortel Phone. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsTestDevice** per restituire tutti i dispositivi di test configurati per l'utilizzo nell'organizzazione. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che utilizza l'operatore -match per restituire tutti i dispositivi con valore stringa "LG-Nortel" all'interno della proprietà Name. Tutti i dispositivi di test che soddisfano questo criterio verranno quindi eliminati tramite il cmdlet **Remove-CsTestDevice**.

    Get-CsTestDevice | Where-Object {$_.Name -match "LG-Nortel Phone"} | Remove-CsTestDevice

## Descrizione dettagliata

Identificando determinati telefoni compatibili con Lync Phone Edition o altri dispositivi come dispositivi di test, gli amministratori possono verificare e approvare gli aggiornamenti del firmware prima che questi vengano applicati a tutti i relativi dispositivi nell'organizzazione. Quando vengono importate in Lync Server, le regole di aggiornamento dei dispositivi vengono contrassegnate come "in sospeso". Questo significa che gli aggiornamenti che corrispondono a tali regole non verranno scaricati e installati automaticamente dai dispositivi interessati.

Al contrario, queste regole in sospeso verranno scaricate e installate in tutti i relativi dispositivi di test. Il concetto alla base dei dispositivi di test è il seguente: le nuove regole di aggiornamento dei dispositivi vengono applicate automaticamente ai dispositivi di test, offrendo agli amministratori la possibilità di verificare che gli aggiornamenti del firmware funzionino come previsto. In tal caso, gli amministratori possono contrassegnare tali regole come approvate; una volta approvate, queste regole vengono scaricate e installate in tutti i relativi dispositivi dell'organizzazione.

I dispositivi di test sono dispositivi hardware che eseguono Lync Server. Vengono creati utilizzando il cmdlet **New-CsTestDevice**. Dopo essere stati creati, questi dispositivi possono essere rimossi eseguendo il cmdlet **Remove-CsTestDevice**. Si noti che la rimozione del dispositivo come dispositivo di test non influisce sul dispositivo in sé. Sarà possibile ad esempio continuare a utilizzare il telefono compatibile con Lync Phone Edition per accedere a Lync Server. L'unica differenza consiste nel fatto che, non essendo più un dispositivo di test, non scaricherà più le regole di aggiornamento "in sospeso". Al contrario, prima di poterle scaricare e installare, il dispositivo attenderà che tali regole vengano approvate.

Per rimuovere i singoli dispositivi di test configurati nell'ambito globale o del sito, è possibile utilizzare il cmdlet **Remove-CsTestDevice**. È inoltre possibile utilizzare questo cmdlet per rimuovere tutti i dispositivi di test configurati in un particolare ambito.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsTestDevice** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTestDevice"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità del dispositivo di test da rimuovere. Per rimuovere un dispositivo specifico, includere sia l'ambito, ad esempio site:Redmond, che il nome del dispositivo, ad esempio -Identity &quot;site:Redmond/UCPhoneTest&quot;. Per rimuovere tutti i dispositivi da un particolare sito, utilizzare la sintassi: -Identity &quot;site:Redmond&quot;.</p>
<p>È possibile rimuovere i dispositivi di test anche dall'ambito globale. La raccolta di dispositivi di test globale non può essere rimossa. Il seguente comando tuttavia eliminerà tutti i dispositivi archiviati nella raccolta globale:</p>
<p>Remove-CsTestDevice –Identity global</p></td>
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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice. Il cmdlet **Remove-CsTestDevice** accetta l'input da pipeline dell'oggetto dispositivo di test.

## Tipi restituiti

Il cmdlet **Remove-CsTestDevice** non restituisce un valore o un oggetto. Elimina invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.TestDevice.

## Vedere anche

#### Ulteriori risorse

[Get-CsTestDevice](get-cstestdevice.md)  
[New-CsTestDevice](new-cstestdevice.md)  
[Set-CsTestDevice](set-cstestdevice.md)

