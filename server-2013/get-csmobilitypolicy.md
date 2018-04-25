---
title: Get-CsMobilityPolicy
TOCTitle: Get-CsMobilityPolicy
ms:assetid: 51ef83de-9cc2-4df8-b4f1-8d816b8de431
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690017(v=OCS.15)
ms:contentKeyID: 49300574
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMobilityPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le informazioni sui criteri per dispositivi mobili attualmente in uso nell'organizzazione. Tali criteri determinano se un utente può o meno utilizzare Lync Mobile. Questi criteri gestiscono inoltre la possibilità di un utente di utilizzare la funzionalità Chiamata tramite ufficio, che consente di effettuare e ricevere chiamate telefoniche sul cellulare utilizzando il numero dell'ufficio anziché quello del cellulare. I criteri per dispositivi mobili possono anche essere utilizzati per richiedere connessioni Wi-Fi quando si effettuano o ricevono chiamate. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsMobilityPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMobilityPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 restituisce le informazioni su tutti i criteri per dispositivi mobili configurati per l'utilizzo nell'organizzazione.

    Get-CsMobilityPolicy

## ESEMPIO 2

Nell'esempio 2 vengono restituite le informazioni su un singolo criterio per dispositivi mobili: il criterio con valore Identity site:Redmond.

    Get-CsMobilityPolicy -Identity "site:Redmond"

## ESEMPIO 3

Nell'esempio 3 vengono restituite le informazioni per tutti i criteri per dispositivi mobili per utente. A tale scopo, viene incluso il parametro Filter insieme al valore di filtro "tag:\*". In questo modo, vengono restituiti gli eventuali criteri per dispositivi mobili con un valore Identity che inizia con la stringa "tag:". Per definizione, i criteri con un valore Identity che inizia con tale valore stringa sono criteri per utente.

    Get-CsMobilityPolicy -Filter "tag:*"

## ESEMPIO 4

Il comando riportato nell'esempio 4 restituisce solo i dati relativi ai criteri per dispositivi mobili in cui la funzionalità Chiamata tramite ufficio è stata disabilitata. A tale scopo, nel comando viene chiamato innanzitutto il cmdlet **Get-CsMobilityPolicy** senza alcun parametro, in modo che venga restituita una raccolta di tutti i criteri per dispositivi mobili configurati per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà EnableOutsideVoice è uguale a (-eq) False.

    Get-CsMobilityPolicy | Where-Object {$_.EnableOutsideVoice -eq $False}

## Descrizione dettagliata

Lync Mobile è un'applicazione client che consente agli utenti di eseguire Lync nei cellulari. La funzionalità Chiamata tramite ufficio consente agli utenti di effettuare con il cellulare chiamate che risultano provenire dal numero dell'ufficio anziché da quello del cellulare. Gli utenti abilitati per la funzionalità Chiamata tramite ufficio possono ottenere questo risultato componendo il numero direttamente dal cellulare oppure utilizzando l'opzione di conferenza telefonica con chiamata in uscita. Con questa opzione, un utente richiede al server dei servizi per dispositivi mobili di Lync Server di effettuare una chiamata al suo posto. Il server appronta la chiamata e quindi richiama l'utente sul cellulare. Dopo che l'utente ha risposto, il server compone il numero della parte da chiamare. Entrambe queste funzionalità possono essere gestite utilizzando criteri per dispositivi mobili.

Con Lync Server 2013, i dispositivi mobili possono effettuare o ricevere chiamate tramite la rete cellulare standard oppure tramite connessioni Wi-Fi. I criteri per dispositivi mobili possono essere utilizzati per richiedere connessioni Wi-Fi e impedire le chiamate tramite la rete cellulare.

I criteri per dispositivi mobili possono essere configurati nell'ambito globale, di sito o per utente e le informazioni su questi criteri possono essere recuperate utilizzando il cmdlet **Get-CsMobilityPolicy**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsMobilityPolicy** in locale: RTCUniversalServerAdmins.

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
<td><p>Consente di utilizzare i caratteri jolly quando si indicano uno o più criteri da restituire. Per restituire, ad esempio, tutti i criteri configurati nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;site:*&quot;</p>
<p>Per restituire una raccolta di tutti i criteri per utente, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;tag:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio per dispositivi mobili da restituire. Per fare riferimento al criterio globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per fare riferimento a un criterio del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Per fare riferimento a un criterio per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity SalesDepartmentPolicy</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Get-CsMobilityPolicy</strong> restituisce una raccolta di tutti i criteri per dispositivi mobili in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati relativi ai criteri per dispositivi mobili dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Get-CsMobilityPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsMobilityPolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility.

