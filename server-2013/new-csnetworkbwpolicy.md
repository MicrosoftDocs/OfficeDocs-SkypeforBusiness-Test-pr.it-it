---
title: New-CsNetworkBWPolicy
TOCTitle: New-CsNetworkBWPolicy
ms:assetid: bbc91bd1-453c-4ae6-bb77-3b6be9429ed0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412916(v=OCS.15)
ms:contentKeyID: 49301795
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBWPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un criterio di larghezza di banda in memoria che può essere applicato al profilo dei criteri di larghezza di banda. In Lync Server il criterio si applica alla larghezza di banda audio o video. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkBWPolicy -BWLimit <UInt32> -BWPolicyModality <Audio | Video> -BWSessionLimit <UInt32>

## Esempi

## ESEMPIO 1

In questo esempio, si creano nuovi criteri di larghezza di banda e li si assegna alla variabile $bwp. Tutti i parametri del cmdlet **New-CsNetworkBWPolicy** sono obbligatori. Nell'esempio è stato specificato un limite totale di larghezza di banda (BWLimit) di 2000 kbps e un limite di sessione della larghezza di banda (BWSessionLimit) di 300 kbps: questi limiti sono stati poi applicati alle sessioni video (-BWPolicyModality video).

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video

## ESEMPIO 2

L'esempio 2 estende l'esempio 1 assegnando i nuovi criteri di larghezza di banda a un profilo di criteri. Il comando alla riga 1 è identico all'esempio 1: crea limiti della larghezza di banda video. Nella riga 2 viene quindi chiamato il cmdlet **New-CsNetworkBandwidthPolicyProfile** per aggiungere il criterio a un nuovo profilo. Il nuovo profilo riceve l'identità LowBWLimit. Viene utilizzato quindi il parametro BWPolicy con il valore $bwp, che corrisponde alla variabile contenente il nuovo criterio di larghezza di banda appena creato alla riga 1.

    $bwp = New-CsNetworkBWPolicy -BWLimit 200 -BWSessionLimit 3000 -BWPolicyModality video
    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bwp

## Descrizione dettagliata

Questo cmdlet crea un nuovo criterio di larghezza di banda. I criteri di questo tipo vengono utilizzati per definire limitazioni della larghezza di banda per alcune modalità. In Lync Server è possibile assegnare limitazioni della larghezza di banda solo alle modalità audio e video. Poiché il criterio di larghezza di banda viene creato solo in memoria, l'output deve essere assegnato a una variabile e quindi passato come valore al parametro BWPolicy del cmdlet **New-CsNetworkBandwidthPolicyProfile** o **Set-CsNetworkBandwidthPolicyProfile**. I criteri di larghezza di banda vengono applicati ai profili dei criteri, che possono archiviare più criteri per un singolo profilo e che fanno parte della configurazione di rete globale per il servizio Controllo di ammissione di chiamata.

Il metodo consigliato per assegnare criteri audio e video consiste nell'assegnarli direttamente a un profilo di criteri di larghezza di banda chiamando il cmdlet **New-CsNetworkBandwidthPolicyProfile** o **Set-CsNetworkBandwidthPolicyProfile** e specificando i valori per i parametri AudioBWLimit, AudioBWSessionLimit, VideoBWLimit e VideoBWSessionLimit.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsNetworkBWPolicy** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBWPolicy"}

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
<td><p><em>BWLimit</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.UInt32</p></td>
<td><p>La larghezza di banda massima consentita, in kbps, per tutte le sessioni simultanee del tipo specificato nel parametro BWPolicyModality.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyModality</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyModality</p></td>
<td><p>Determina che tipo di larghezza di banda è limitata.</p>
<p>Valori validi: Audio, Video</p></td>
</tr>
<tr class="odd">
<td><p><em>BWSessionLimit</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.UInt32</p></td>
<td><p>La larghezza di banda massima consentita, in kbps, per una sessione singola del tipo specificato nel parametro BWPolicyModality.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Crea un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)

