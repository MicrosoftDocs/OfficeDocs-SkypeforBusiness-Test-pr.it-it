---
title: Get-CsVoiceRoute
TOCTitle: Get-CsVoiceRoute
ms:assetid: 422abb2d-bff3-4b9a-b18c-d8202b01f69b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425926(v=OCS.15)
ms:contentKeyID: 49300338
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceRoute

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle route vocali configurate per l'utilizzo in un'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsVoiceRoute [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceRoute [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Consente di recuperare le proprietà per tutte le route vocali definite nell'organizzazione.

    Get-CsVoiceRoute

## ESEMPIO 2

Consente di recuperare le proprietà per la route vocale Route1.

    Get-CsVoiceRoute -Identity Route1

## ESEMPIO 3

Questo comando consente di visualizzare le impostazioni della route vocale la cui identità contiene la stringa "test" in qualsiasi posizione all'interno del valore. Per trovare la stringa test solo alla fine dell'identità, utilizzare il valore \*test. Analogamente, per trovare la stringa test solo all'inizio dell'identità, specificare il valore test\*.

    Get-CsVoiceRoute -Filter *test*

## ESEMPIO 4

Questo comando recupera tutte le route vocali a cui non sono stati assegnati gateway PSTN. Vengono innanzitutto recuperate tutte le route vocali utilizzando il cmdlet **Get-CsVoiceRoute**. Queste route vocali vengono quindi inviate tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** circoscrive i risultati dell'operazione Get. In questo caso viene esaminata ogni route vocale (ecco che cosa rappresenta $\_) e viene verificata la proprietà Count della proprietà PstnGatewayList. Se il conteggio dei gateway PSTN è pari a 0, l'elenco è vuoto e per la route non sono stati definiti gateway.

    Get-CsVoiceRoute | Where-Object {$_.PstnGatewayList.Count -eq 0}

## Descrizione dettagliata

Utilizzare questo cmdlet per recuperare una o più route vocali esistenti. Le route vocali includono istruzioni che comunicano a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale a numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange).

Questo cmdlet può essere utilizzato per recuperare informazioni sulle route vocali, ad esempio a quali gateway PSTN è associata la route, quali utilizzi PSTN sono associati alla route, il modello (sotto forma di espressione regolare) che identifica i numeri di telefono a cui si applica la route e le impostazioni per l'ID del chiamante. L'utilizzo PSTN associa la route vocale a un criterio telefonico.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsVoiceRoute** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceRoute"}

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
<td><p>Questo parametro consente di filtrare i risultati dell'operazione Get in base al carattere jolly passato al parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Una stringa che identifica in modo univoco la route vocale. Se non viene fornita un'identità, vengono restituite tutte le route vocali per l'organizzazione.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la route vocale dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceRoute](new-csvoiceroute.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Test-CsVoiceRoute](test-csvoiceroute.md)

