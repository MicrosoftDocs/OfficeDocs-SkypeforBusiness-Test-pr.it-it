---
title: Get-CsAudioConferencingProvider
TOCTitle: Get-CsAudioConferencingProvider
ms:assetid: 4632e9d0-aa87-459f-ad7e-27125c11da5b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994030(v=OCS.15)
ms:contentKeyID: 52062152
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAudioConferencingProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui provider di servizi di audioconferenza autorizzati per l'uso nell'organizzazione. I provider di servizi di audioconferenza sono società di terze parti che forniscono servizi di conferenza alle organizzazioni.

Il cmdlet **Get-CsAudioConferencingProvider** può essere usato solo con Microsoft Lync Online.

## Sintassi

    Get-CsAudioConferencingProvider [[-Identity] <XdsGlobalRelativeIdentity>] [-LocalStore][<CommonParameters>]Get-CsAudioConferencingProvider [-Filter <string>] [-LocalStore] [<CommonParameters>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni relative a tutti i provider di servizi di audioconferenza disponibili per l'uso nell'organizzazione.

    Get-CsAudioConferencingProvider

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per un singolo provider di servizi di audioconferenza, ovvero il provider con identità (Identity) Fabrikam Telecom.

    Get-CsAudioConferencingProvider -Identity "Fabrikam Telecom"

## Esempio 3

L'esempio 3 dimostra come si possono usare valori jolly (e il parametro Filter) per restituire informazioni sui provider di servizi di audioconferenza. In questo esempio, il valore di filtro "\*Fabrikam\*" restituisce tutti i provider di servizi di audioconferenza con il valore stringa "Fabrikam" in qualsiasi posizione nel parametro Identity.

    Get-CsAudioConferencingProvider -Filter "*Fabrikam*"

## Descrizione dettagliata

Un provider di servizi di audioconferenza è una società terza che fornisce servizi di conferenza alle organizzazioni. Tra l'altro, i provider di servizi di audioconferenza consentono agli utenti in trasferta non connessi alla rete aziendale o a Internet di accedere ai contenuti audio di una conferenza o di una riunione. Tali provider offrono spesso servizi di qualità elevata quali traduzione immediata, trascrizione e assistenza diretta di un operatore durante la conferenza.

Dopo aver stabilito un rapporto contrattuale con un provider di servizi di audioconferenza, le organizzazioni possono assegnare gli utenti al provider tramite il cmdlet **Set-CsUserAcp**. Gli amministratori possono usare il cmdlet **Get-CsAudioConferencingProvider** per recuperare informazioni sui provider di servizi di audioconferenza disponibili.

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
<td><p>Consente di usare caratteri jolly per indicare il provider di servizi di audioconferenza (o i provider) da restituire. Questa sintassi, ad esempio, restituisce informazioni su tutti i provider di servizi di audioconferenza con il valore stringa &quot;fabrikam&quot; in qualche posizione nel parametro Identity:</p>
<p>-Filter &quot;*fabrikam*&quot;</p>
<p>Si noti che non è possibile usare il parametro Filter e il parametro Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il provider di servizi di audioconferenza da restituire. Esempio:</p>
<p>-Identity &quot;Fabrikam Telecom&quot;</p>
<p>Se nel comando non viene incluso né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsAudioConferencingProvider</strong> restituisce informazioni per tutti i provider disponibili.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati sui provider di servizi di audioconferenza dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsAudioConferencingProvider** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsAudioConferencingProvider** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AudioConferencingProvider.AudioConferencingProvider\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)  
[Set-CsUserAcp](set-csuseracp.md)

