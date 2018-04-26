---
title: Get-CsTrustedApplicationPool
TOCTitle: Get-CsTrustedApplicationPool
ms:assetid: f8dc4ad7-fc32-482b-a1cb-5ba106df3344
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413055(v=OCS.15)
ms:contentKeyID: 49302539
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplicationPool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le impostazioni per uno o più pool contenenti i computer che ospitano applicazioni attendibili. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsTrustedApplicationPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsTrustedApplicationPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-PoolFqdn <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperati tutti i pool all'interno della distribuzione di Lync Server che sono stati definiti come pool di applicazioni attendibili.

    Get-CsTrustedApplicationPool

## ESEMPIO 2

Nell'esempio è stato utilizzato il parametro Identity per recuperare solamente un pool di applicazioni attendibili, in questo caso il pool con nome di dominio completo (FQDN) TrustPool.litwareinc.com.

    Get-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com

## ESEMPIO 3

In questo esempio vengono recuperati tutti i pool di applicazioni attendibili che contengono il sito TrustPool nel proprio nome di dominio completo (FQDN). Il parametro Filter viene utilizzato con un valore \*:TrustPool.\*. Tale stringa di filtro consentirà di ricercare nei valori Identity di tutti i pool di applicazioni attendibili quelli che contengono la stringa ":TrustPool.". Ad esempio, questo comando recupererà il pool con valore Identity TrustedApplicationPool:TrustPool.litwareinc.com.

    Get-CsTrustedApplicationPool -Filter *:TrustPool.*

## ESEMPIO 4

Il parametro Filter consente di effettuare la ricerca solo in base al parametro Identity, che nei pool di applicazioni attendibili corrisponde all'ID servizio nel formato TrustedApplicationPool:\<FQDN\>. In questo caso i pool vengono ricercati in base all'ID servizio nel formato \<sito\>-ExternalServer-\<id\>, ad esempio Redmond1-ExternalServer-1. In questo modo è possibile trovare i pool attendibili presenti in un sito specifico. Nell'esempio viene innanzitutto chiamato il cmdlet **Get-CsTrustedApplicationPool** senza alcun parametro per recuperare una raccolta di tutti i pool di applicazioni attendibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che circoscrive la raccolta ai soli pool in cui l'ID servizio ($\_.ServiceId) corrisponde alla stringa con caratteri jolly (-like) Redmond1\*. Come risultato, si otterrà una raccolta di tutti i pool di applicazioni attendibili con nomi di dominio completi che iniziano con la stringa Redmond1, ad esempio Redmond1-ExternalServer-1, Redmond1-ExternalServer-2 e Redmond1-ExternalServer-3.

    Get-CsTrustedApplicationPool | Where-Object {$_.ServiceId -like "Redmond1*"}

## Descrizione dettagliata

È consigliabile che i computer che eseguono applicazioni attendibili all'interno di una distribuzione di Lync Server vengano aggiunti a un pool distinto, destinato unicamente a questo tipo di applicazioni. È comunque possibile aggiungere i computer con applicazioni attendibili a un pool esistente, utilizzato anche per altri scopi. Questo cmdlet recupera uno o più pool che sono stati definiti come pool di applicazioni attendibili.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsTrustedApplicationPool** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplicationPool"}

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
<td><p>Una stringa contenente uno o più caratteri jolly che viene utilizzata per cercare un pool con un valore Identity che corrisponde alla stringa con caratteri jolly. Ad esempio, specificando la stringa *Redmond*, verranno recuperati tutti i pool di applicazioni attendibili con identità contenenti la stringa Redmond, come TrustedApplicationPool:Redmond.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome di dominio completo (FQDN) o l'ID servizio del pool di cui si desidera recuperare le impostazioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome di dominio completo (FQDN) del pool che si desidera recuperare. Questo parametro si comporta come il parametro Identity, ad eccezione del fatto che il parametro Identity accetta anche l'ID di servizio.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Recupera uno o più oggetti di tipo Microsoft.Rtc.Management.Xds.DisplayExternalServer.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Set-CsTrustedApplicationPool](set-cstrustedapplicationpool.md)

