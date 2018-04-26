---
title: Get-CsOutboundTranslationRule
TOCTitle: Get-CsOutboundTranslationRule
ms:assetid: 0564df17-dcca-44e1-9341-15521e0fa14b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398104(v=OCS.15)
ms:contentKeyID: 49299547
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsOutboundTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più regole di conversione in uscita. Una regola di conversione in uscita consente di convertire i numeri di telefono nel formato di composizione locale per l'interazione con sistemi PBX e gateway PSTN. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsOutboundTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsOutboundTranslationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperate tutte le regole di conversione in uscita per la distribuzione di Lync Server.

    Get-CsOutboundTranslationRule

## ESEMPIO 2

Con questo esempio viene recuperata una singola regola di conversione in uscita, quella con identità site:Redmond/Prefix Redmond.

    Get-CsOutboundTranslationRule -Identity "site:Redmond/Prefix Redmond"

## ESEMPIO 3

In questo esempio vengono recuperate tutte le regole di conversione in uscita a livello di sito. Il comando chiama il cmdlet **Get-CsOutboundTranslationRule** con un filtro uguale a site:\* per restituire una raccolta di tutte le regole con valori di identità che iniziano con la stringa site:.

    Get-CsOutboundTranslationRule -Filter site:*

## Descrizione dettagliata

Chiamare questo cmdlet per recuperare una regola di conversione in uscita esistente. Lync Server normalizza i numeri di telefono nel formato E.164. Numerosi sistemi PBX privati non sono tuttavia in grado di utilizzare questo formato. Le regole di conversione in uscita consentono di convertire il numero nel formato di composizione locale prima dell'invio al Mediation Server o al gateway.

Ogni regola di conversione in uscita è associata a una configurazione del trunk. A ogni configurazione del trunk possono essere associate più regole di conversione in uscita. Pertanto, l'identità per ogni regola è costituita da un ambito con un nome univoco per tale ambito nel formato ambito/nome, ad esempio site:Redmond/OBR1. La regola viene associata automaticamente alla configurazione del trunk con lo stesso ambito.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsOutboundTranslationRule** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsOutboundTranslationRule"}

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
<td><p>Consente di eseguire una ricerca con caratteri jolly che permette di circoscrivere i risultati alle regole di conversione in uscita le cui identità corrispondono alla stringa con caratteri jolly fornita.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della regola di conversione in uscita che si desidera recuperare. L'identità è costituita dall'ambito seguito da un nome univoco per ogni ambito (ad esempio site:Redmond/OutboundRule1). Con l'indicazione di un valore per Identity viene restituita al massimo una regola di conversione in uscita.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la regola di conversione in uscita dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet consente di recuperare uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TranslationRule.

## Vedere anche

#### Ulteriori risorse

[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Remove-CsOutboundTranslationRule](remove-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)

