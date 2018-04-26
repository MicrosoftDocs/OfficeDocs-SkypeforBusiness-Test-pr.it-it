---
title: Get-CsMediaConfiguration
TOCTitle: Get-CsMediaConfiguration
ms:assetid: 071c1733-07c3-4075-8745-367634e37941
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398128(v=OCS.15)
ms:contentKeyID: 49299575
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMediaConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni multimediali, inclusi il livello di crittografia supportato, l'eventuale utilizzo di Siren come codec vocale da parte del Mediation Server nelle interazioni con i client Lync Server e la risoluzione video massima consentita. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsMediaConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMediaConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite tutte le configurazioni multimediali in uso nell'organizzazione chiamando il cmdlet **Get-CsMediaConfiguration** senza alcun parametro aggiuntivo.

    Get-CsMediaConfiguration

## ESEMPIO 2

Nell'esempio 2 viene restituita solamente la configurazione multimediale con Identity site:Redmond1. Poiché le identità devono essere univoche, l'utilizzo del parametro Identity garantisce che non verrà mai recuperato più di un elemento.

    Get-CsMediaConfiguration -Identity site:Redmond1

## ESEMPIO 3

Nell'esempio 3, il parametro Filter è utilizzato per restituire tutte le configurazioni che sono state impostate in ambito sito. La stringa di caratteri jolly site:\* garantisce che Windows PowerShell restituisca solamente le raccolte di configurazioni multimediali le cui identità iniziano con la stringa site:.

    Get-CsMediaConfiguration -Filter site:*

## ESEMPIO 4

In questo esempio vengono utilizzati i cmdlet **Get-CsMediaConfiguration** e **Where-Object** per ottenere tutte le configurazioni multimediali che supportano (ma non richiedono) la crittografia. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsMediaConfiguration** per recuperare tutte le configurazioni multimediali in uso nell'organizzazione. Le informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che applica un filtro per limitare i dati restituiti alle configurazioni in cui la proprietà EncryptionLevel è uguale a (-eq) SupportEncryption.

    Get-CsMediaConfiguration | Where-Object {$_.EncryptionLevel -eq "SupportEncryption"}

## ESEMPIO 5

In questo esempio vengono recuperate tutte le configurazioni multimediali definite per i siti e servizi i cui nomi contengono la stringa "med". Ad esempio, questo comando consente di recuperare le impostazioni di configurazione multimediale definite per il sito medford1, il sito TwoMedfordPlace, il servizio MediationServer:redmond.litwareinc.com.

    Get-CsMediaConfiguration -Filter *:*med*

## Descrizione dettagliata

Questo cmdlet consente di recuperare una o più raccolte di impostazioni che definiscono le interazioni multimediali.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsMediaConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsMediaConfiguration"}

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
<td><p>Questo parametro consente di filtrare i risultati dell'operazione Get in base ai caratteri jolly specificati per il parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco della configurazione multimediale che si desidera recuperare. Questo identificatore specifica l'ambito a cui viene applicata la configurazione (globale, sito o servizio).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la configurazione multimediale dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsMediaConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Media.MediaSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsMediaConfiguration](new-csmediaconfiguration.md)  
[Remove-CsMediaConfiguration](remove-csmediaconfiguration.md)  
[Set-CsMediaConfiguration](set-csmediaconfiguration.md)

