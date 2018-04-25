---
title: Get-CsSipResponseCodeTranslationRule
TOCTitle: Get-CsSipResponseCodeTranslationRule
ms:assetid: 075e9e85-8f85-402c-9256-4e73ec93f96b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398130(v=OCS.15)
ms:contentKeyID: 49299585
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSipResponseCodeTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle regole di conversione dei codici di risposta SIP. Queste regole consentono agli amministratori di convertire i codici di risposta SIP con valori compresi tra 400 e 699 in valori utilizzati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsSipResponseCodeTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsSipResponseCodeTranslationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce una raccolta di tutte le regole di conversione dei codici di risposta configurate per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsSipResponseCodeTranslationRule** senza alcun parametro.

    Get-CsSipResponseCodeTranslationRule

## ESEMPIO 2

Nell'esempio 2 viene restituita una singola regola di conversione dei codici di risposta: la regola con Identity PstnGateway:192.168.0.240/Rule404.

    Get-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404"

## ESEMPIO 3

nell'esempio 3, il parametro Filter viene utilizzato per limitare la quantità di dati restituiti a tutte le regole di conversione dei codici di risposta configurate nell'ambito del sito. Il valore del filtro "site:\*" restituisce solo i dati relativi a quelle regole la cui identità inizia con la stringa "site:".

    Get-CsSipResponseCodeTranslationRule -Filter "site:*"

## ESEMPIO 4

Il comando riportato nell'esempio 4 restituisce una raccolta tutte le regole di conversione dei codici di risposta nelle quali non è stato configurato alcun valore per la proprietà ReceivedISUPCauseValue. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsSipResponseCodeTranslationRule** senza alcun parametro per restituire una raccolta di tutte le regole di conversione dei codici di risposta attualmente in uso. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà ReceivedISUPCauseValue è uguale a -1.

    Get-CsSipResponseCodeTranslationRule | Where-Object {$_.ReceivedISUPCauseValue -eq -1}

## Descrizione dettagliata

Il trunking SIP consente di collegare una rete VoIP (Voice over Internet Protocol), ad esempio VoIP aziendale, a una rete PSTN (Public Switched Telephone Network). In Lync Server il Mediation Server utilizza peer di trunking per interagire con la rete PSTN. Se una chiamata in uscita sulla rete PSTN ha esito negativo, viene generato automaticamente un codice di causa ISUP (ISDN User Part). Ad esempio, un gateway PSTN potrebbe inviare un codice di causa 34 per indicare che non sono disponibili circuiti o canali per completare la chiamata. Quando un peer di trunking del Mediation Server riceve questo codice di causa ISUP, lo converte in un codice di risposta SIP, che viene quindi inviato al Mediation Server stesso. A sua volta, Lync Server utilizza questi codici di risposta per prendere le proprie decisioni per il routing in uscita. Ad esempio, a un gateway che non funziona correttamente potrebbe venire assegnato automaticamente uno stato di bassa priorità per limitare l'utilizzo del gateway e aumentare le possibilità di completare correttamente una chiamata.

Non tutti i gateway utilizzano tuttavia il mapping tra codici di causa ISUP e codici di risposta SIP consigliato utilizzato da Lync Server. Per questi gateway, gli amministratori possono utilizzare i cmdlet **CsSipResponseCodeTranslationRule** per convertire i codici di risposta SIP del gateway (in combinazione con l'eventuale codice di causa ISUP) in un codice di risposta SIP utilizzato da Lync Server. Ad esempio, un gateway potrebbe convertire un codice di causa ISUP 34 (nessun circuito/canale disponibile) in un codice di risposta SIP 486 (non disponibile). Sulla base di un codice di riposta 486, la logica di routing in uscita di Lync Server non tenterà di trovare un altro gateway per completare la chiamata.

Per Lync Server, tuttavia, quel codice di risposta SIP 486 potrebbe essere convertito in un codice di risposta SIP 503. Il codice di risposta 503 avvia il meccanismo di riprova nella logica di instradamento in uscita di Lync Server; ciò significa che il sistema cercherà un altro gateway per completare la chiamata. Per gestire questa situazione è possibile creare una regola di conversione che converta un codice di causa ISUP 34 e un codice di risposta SIP 486 in un codice di risposta SIP 503.

Il cmdlet **Get-CsSipResponseCodeTranslationRule** consente di recuperare informazioni relative a tutte le regole di conversione configurate per l'utilizzo nella propria organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsSipResponseCodeTranslationRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsSipResponseCodeTranslationRule"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare la regola o le regole di conversione da ottenere. Ad esempio, la seguente sintassi restituisce tutte le regole di conversione la cui identità contiene la stringa &quot;404&quot;:</p>
<p>-Filter &quot;*404*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della regola di conversione. L'identità di una regola di conversione consta di due parti: l'ambito in cui la regola è stata configurata e il nome assegnato alla regola al momento della creazione. Ad esempio, una regola di conversione denominata Rule404 creata nell'ambito globale avrebbe un'identità simile alla seguente: global/Rule404.</p>
<p>Oltre che nell'ambito globale, le regole di conversione possono anche essere create a livello di sito o di servizio (sebbene solo per il servizio PstnGateway).</p>
<p>Per ottenere tutte le regole di conversione create per un determinato sito o servizio, basta specificare l'identità del sito o servizio in questione. Ad esempio:</p>
<p>-Identity &quot;site:Redmond.&quot;</p>
<p>Se questo parametro viene omesso, il cmdlet <strong>Get-CsSipResponseCodeTranslationRule</strong> restituisce una raccolta di tutti i codici di conversione delle risposte SIP.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati delle regole di conversione del codice di risposta SIP dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsSipResponseCodeTranslationRule** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsSipResponseCodeTranslationRule** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTRanslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)  
[Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)  
[Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

