---
title: Get-CsImFilterConfiguration
TOCTitle: Get-CsImFilterConfiguration
ms:assetid: de9b24a1-8d17-4da1-89c2-db5b532674eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398980(v=OCS.15)
ms:contentKeyID: 49302212
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsImFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce i filtri per i collegamenti presenti nei messaggi istantanei configurati nell'organizzazione. Questi filtri vengono utilizzati per impedire agli utenti di inviare messaggi istantanei contenenti collegamenti ipertestuali con determinati prefissi, ad esempio collegamenti con un prefisso http o telnet. A seconda delle impostazioni, ciò significa che qualsiasi URI (Uniform Resource Identifier) preceduto da uno di questi schemi verrà convertito in un collegamento ipertestuale non selezionabile oppure verrà rimosso del tutto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsImFilterConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsImFilterConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce una raccolta di tutti i filtri per i collegamenti ipertestuali dei messaggi istantanei configurati per l'utilizzo nell'organizzazione. Questo è il comportamento predefinito ogni volta che si chiama il cmdlet **Get-CsImFilterConfiguration** senza ulteriori parametri.

    Get-CsImFilterConfiguration

## ESEMPIO 2

Nell'esempio 2 vengono restituite le impostazioni relative a un singolo filtro per messaggi istantanei, ovvero le impostazioni con identità site:Redmond. Poiché le identità devono essere univoche, in comando non restituirà mai più di una configurazione.

    Get-CsImFilterConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per restituire una raccolta di tutti i filtri per messaggi istantanei che sono stati configurati a livello del sito. La stringa con caratteri jolly site:\* indica al cmdlet **Get-CsImFilterConfiguration** di restituire solo le configurazioni dei filtri per messaggi istantanei il cui parametro Identity inizia con il valore stringa site:.

    Get-CsImFilterConfiguration -Filter site:*

## ESEMPIO 4

Nell'esempio 4 il valore della proprietà Prefixes della configurazione globale dei filtri per messaggi istantanei è "espanso" quando viene visualizzato. Questo significa semplicemente che la proprietà e i relativi valori vengono visualizzati in un formato più semplice e leggibile. Per eseguire questa attività, viene innanzitutto utilizzato il cmdlet **Get-CsImFilterConfiguration** per recuperare la configurazione globale dei filtri per messaggi istantanei. Si noti che la chiamata al cmdlet **Get-CsImFilterConfiguration** è racchiusa tra parentesi. Ciò significa che Windows PowerShell deve innanzitutto eseguire il comando racchiuso tra parentesi, quindi deve procedere da quel punto. Una volta recuperata la configurazione, viene visualizzato il valore della proprietà Prefixes con un prefisso su ciascuna riga.

    (Get-CsImFilterConfiguration -Identity Global).Prefixes

## Descrizione dettagliata

Quando vengono inviati messaggi istantanei, gli utenti possono incorporare nel testo del messaggio un URI per rimandare a una condivisione o a un sito Web particolare gli altri partecipanti alla conversazione. È possibile configurare Lync Server in modo che i collegamenti ipertestuali con determinati prefissi vengano bloccati o non risultino attivi. In altri termini, i partecipanti non possono semplicemente fare clic sul collegamento per accedere al sito a cui fa riferimento l'URI, ma devono manualmente copiare e incollare il collegamento in un browser.

Il cmdlet **Get-CsImFilterConfiguration** recupera tutte le impostazioni per filtrare gli URI nei messaggi istantanei. Chiamato da solo (senza alcun parametro), il cmdlet **Get-CsImFilterConfiguration** restituisce tutte le impostazioni di filtro per gli URI presenti nei messaggi istantanei, a livello globale e per tutti i siti. È inoltre possibile specificare un'identità per visualizzare le impostazioni per un determinato sito (o le impostazioni globali).

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsImFilterConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsImFilterConfiguration"}

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
<td><p>Esegue una ricerca con caratteri jolly per individuare le configurazioni che corrispondono a un determinata sequenza di caratteri relativa all'identità. Ad esempio, restituisce tutte le impostazioni la cui identità inizia con site* (tutte impostazioni specifiche del sito).</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>l'identificatore univoco delle impostazioni che si desidera recuperare. Sarà global o site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito al quale si applicano queste impostazioni, ad esempio, site:Redmond.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la configurazione dei filtri per i messaggi istantanei dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsImFilterConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.ImFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsImFilterConfiguration](new-csimfilterconfiguration.md)  
[Remove-CsImFilterConfiguration](remove-csimfilterconfiguration.md)  
[Set-CsImFilterConfiguration](set-csimfilterconfiguration.md)

