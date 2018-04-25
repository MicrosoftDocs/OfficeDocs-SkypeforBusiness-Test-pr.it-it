---
title: Get-CsVoiceConfiguration
TOCTitle: Get-CsVoiceConfiguration
ms:assetid: c5e7afa3-28d3-4bf9-a2f2-c34932c9a3cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398815(v=OCS.15)
ms:contentKeyID: 49301936
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera l'oggetto configurazione vocale che include un elenco completo di tutte le configurazioni di test vocali definite per la distribuzione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

In questo esempio viene recuperata la configurazione vocale. Per recuperare le configurazioni di test vocali, utilizzare il cmdlet **Get-CsVoiceTestConfiguration**.

    Get-CsVoiceConfiguration

## Descrizione dettagliata

Le configurazioni di test vocali sono utilizzate per testare un numero di telefono a fronte di criteri vocali, route e dial plan specifici. Questo cmdlet è utilizzato per recuperare l'istanza globale che contiene un elenco di tutte le configurazioni di test vocali definite nella distribuzione di Lync Server. Per recuperare le singole configurazioni di test vocali o per recuperarle come oggetti singoli anziché sotto forma di elenco, utilizzare il cmdlet **Get-CsVoiceTestConfiguration**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsVoiceConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceConfiguration"}

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
<td><p>Poiché può esistere una sola istanza dell'oggetto, questo parametro non ha alcuna utilità.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'ambito della configurazione vocale da recuperare. L'unico valore possibile è Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la configurazione vocale dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet restituisce un'istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Set-CsVoiceConfiguration](set-csvoiceconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

