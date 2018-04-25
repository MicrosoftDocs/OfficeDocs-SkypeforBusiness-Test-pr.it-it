---
title: Get-CsLisServiceProvider
TOCTitle: Get-CsLisServiceProvider
ms:assetid: 060b0b32-5787-487b-b1d9-7a0c7dd44d80
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398116(v=OCS.15)
ms:contentKeyID: 49299565
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLisServiceProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le informazioni sul servizio Web fornito dal provider del routing di rete Enhanced 9-1-1 (E9-1-1) per la convalida delle località. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLisServiceProvider

## Esempi

## ESEMPIO 1

Il cmdlet **Get-CsLisServiceProvider** non ha alcun parametro aggiuntivo (oltre ai parametri comuni di Windows PowerShell, come Verbose). In un'implementazione E9-1-1 non vi sarà mai più di un provider di servizi, pertanto questo cmdlet consentirà di recuperare le informazioni inerenti il servizio Web fornito da quel provider.

    Get-CsLisServiceProvider

## Descrizione dettagliata

In una implementazione di VoIP aziendale che prevede E9-1-1, le chiamate di emergenza devono passare attraverso un provider del routing di rete E9-1-1 in modo da poter essere poi correttamente instradate al punto PSAP (Public Safety Answering Point) appropriato. Negli Stati Uniti, un PSAP è un ente che si occupa di indirizzare le chiamate al servizio di emergenza più vicino, come, ad esempio, la polizia, i vigili del fuoco e il servizio ambulanze. Per effettuare questo servizio, il provider deve ricevere dall'organizzazione un elenco di località da verificare e convalidare sulla base dello stradario ufficiale. Questo cmdlet consente di recuperare le informazioni sul provider, inclusi il suo nome e l'URL del servizio Web che l'organizzazione utilizzerà per inviare l'elenco di località.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsLisServiceProvider** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLisServiceProvider"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Questo cmdlet fornisce solo i parametri comuni di Windows PowerShell.</p></td>
<td><p></p></td>
<td><p></p></td>
<td> </td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet consente di recuperare un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Remove-CsLisServiceProvider](remove-cslisserviceprovider.md)  
[Set-CsLisServiceProvider](set-cslisserviceprovider.md)

