---
title: Get-CsNetworkInterSitePolicy
TOCTitle: Get-CsNetworkInterSitePolicy
ms:assetid: a4a64048-f8d7-483a-9565-0c6f3b0937b7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412769(v=OCS.15)
ms:contentKeyID: 49301542
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterSitePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più criteri tra siti di rete che definiscono le limitazioni della larghezza di banda tra i siti direttamente collegati in una configurazione di Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkInterSitePolicy [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterSitePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Se si chiama il cmdlet **Get-CsNetworkInterSitePolicy** senza parametri, verranno recuperati tutti i criteri di sito di rete definiti tra due siti di rete collegati direttamente.

    Get-CsNetworkInterSitePolicy

## ESEMPIO 2

Nell'esempio viene recuperato il criterio di sito con Identity Reno\_Portland.

    Get-CsNetworkInterSitePolicy -Identity Reno_Portland

## ESEMPIO 3

Nell'esempio 3 vengono recuperati tutti i criteri di sito della rete che presentano la stringa Reno in qualunque posizione nel valore Identity. I caratteri jolly (\*) presenti nel valore passato al parametro Filter indicano "qualsiasi carattere o serie di caratteri". In altri termini, la stringa \*Reno\* corrisponde ai valori Identity che iniziano con uno o più caratteri qualsiasi, seguiti dalla stringa Reno, a sua volta seguita da qualsiasi carattere o serie di caratteri.

    Get-CsNetworkInterSitePolicy -Filter *Reno*

## ESEMPIO 4

Nell'esempio vengono recuperati tutti i criteri di sito di rete ai quali non è stato assegnato un profilo dei criteri di larghezza di banda. Il comando chiama innanzitutto il cmdlet **Get-CsNetworkInterSitePolicy**, che come illustrato nell'esempio 1 recupera una raccolta di tutti i criteri di sito di rete. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** circoscrive la raccolta solo ai criteri di sito ai quali non è stato assegnato un profilo di criteri di larghezza di banda. Questa operazione viene eseguita tramite un confronto al fine di verificare se la proprietà BWPolicyProfileID di ogni criterio di sito sia uguale a (-eq) Null ($null).

    Get-CsNetworkInterSitePolicy | Where-Object {$_.BWPolicyProfileID -eq $null}

## Descrizione dettagliata

Se due siti di rete condividono un collegamento diretto, è possibile definire dei limiti della larghezza di banda per le connessioni audio e video tra tali siti. Questo cmdlet recupera uno o più criteri di sito della rete che associano le impostazioni di limitazione della larghezza di banda ai siti connessi in modo diretto.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsNetworkInterSitePolicy** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterSitePolicy"}

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
<td><p>Stringa contenente caratteri jolly per eseguire la ricerca dei criteri con valori Identity corrispondenti alla stringa di caratteri jolly.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'identificatore univoco del criterio di sito della rete che si desidera recuperare. I criteri di sito vengono creati solo con ambito globale, pertanto questo identificatore non richiede di specificare un ambito. Contiene invece una stringa che rappresenta un nome univoco che identifica il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative ai criteri inter-sito della rete dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Recupera un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.InterNetworkSitePolicyType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkInterSitePolicy](new-csnetworkintersitepolicy.md)  
[Remove-CsNetworkInterSitePolicy](remove-csnetworkintersitepolicy.md)  
[Set-CsNetworkInterSitePolicy](set-csnetworkintersitepolicy.md)

