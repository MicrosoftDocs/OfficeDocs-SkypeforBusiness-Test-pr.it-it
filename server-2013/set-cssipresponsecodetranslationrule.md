---
title: Set-CsSipResponseCodeTranslationRule
TOCTitle: Set-CsSipResponseCodeTranslationRule
ms:assetid: 3ce2fafe-9c79-4462-9f24-c2a30502e641
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425895(v=OCS.15)
ms:contentKeyID: 49300278
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSipResponseCodeTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una regola di conversione dei codici di risposta SIP esistente. Queste regole consentono agli amministratori di convertire i codici di risposta SIP con valori compresi tra 400 e 699 in valori utilizzati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsSipResponseCodeTranslationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsSipResponseCodeTranslationRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Priority <Int32>] [-ReceivedISUPCauseValue <Int32>] [-ReceivedResponseCode <Int32>] [-TranslatedResponseCode <Int32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di modificare la proprietà ReceivedISUPCauseValue della regola di conversione con Identity PstnGateway:192.168.0.240/Rule404.

    Set-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404" -ReceivedISUPCauseValue 477

## ESEMPIO 2

Nell'Esempio 2, la regola di conversione con Identity PstnGateway:192.168.0.240/Rule404 ha la priorità più alta, vale a dire che questa regola verrà elaborata per prima. Infatti, la regola ha la priorità (Priority) impostata su 0.

    Set-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404" -Priority 0

## ESEMPIO 3

Nell'esempio 3 viene illustrato come impostare su -1 la proprietà ReceivedISUPCauseValue di tutte le regole di conversione configurate per l'utilizzo nell'organizzazione. In questo modo, il codice di causa ISUP viene ignorato durante la conversione delle regole. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsSipResponseCodeTranslationRule** senza alcun parametro per restituire una raccolta di tutte le regole di conversione dei codici di risposta SIP attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsSipResponseCodeTranslationRule**, che modifica la proprietà ReceivedISUPCauseValue per ogni elemento della raccolta.

    Get-CsSipResponseCodeTranslationRule | Set-CsSipResponseCodeTranslationRule -ReceivedISUPCauseValue -1

## Descrizione dettagliata

Il trunking SIP consente di connettersi a una rete VoIP (Voice over Internet Protocol) come VoIP aziendale mediante PSTN (Public Switched Telephone Network). In Lync Server il Mediation Server utilizza i peer di trunking per interagire con la rete PSTN. Quando una chiamata in uscita ha esito negativo sulla rete PSTN, viene generato automaticamente un codice di causa ISDN User Part (ISUP). Ad esempio, un gateway PSTN può inviare il codice di causa 34 per indicare che non è disponibile alcun circuito o canale per completare la chiamata. Quando un peer di trunking Mediation Server riceve tale codice di causa ISUP, lo converte in un codice di risposta SIP, che viene quindi inviato al Mediation Server. In Lync Server i codici di risposta vengono utilizzati per le decisioni relative al routing in uscita. Ad esempio, a un gateway che non funziona correttamente potrebbe essere assegnato automaticamente uno stato di priorità secondaria per limitare l'utilizzo di tale gateway e aumentare le possibilità di completare correttamente una chiamata.

Tuttavia, non tutti i gateway utilizzano il mapping da codici di causa ISUP a codici di risposta SIP consigliato utilizzato da Lync Server. Per questi gateway, gli amministratori possono utilizzare i cmdlet **CsSipResponseCodeTranslationRule** per convertire i codici di risposta SIP del gateway (in combinazione con il codice di causa ISUP, se disponibile) in un codice di risposta SIP utilizzato da Lync Server. Ad esempio, un gateway potrebbe convertire un codice di causa ISUP 34 ("Nessun circuito/canale disponibile") in un codice di risposta SIP 486 ("Non disponibile qui"). Basandosi su un codice di riposta 486, la logica di instradamento in uscita di Lync Server non cercherà un altro gateway per completare la chiamata.

Per Lync Server, tuttavia, quel codice di risposta SIP 486 potrebbe essere convertito in un codice di risposta SIP 503. Il codice di risposta 503 avvia il meccanismo di riprova nella logica di instradamento in uscita di Lync Server; ciò significa che il sistema cercherà un altro gateway per completare la chiamata. Per gestire questa situazione è possibile creare una regola di conversione che converta un codice di causa ISUP 34 e un codice di risposta SIP 486 in un codice di risposta SIP 503.

Il cmdlet **Set-CsSipResponseCodeTranslationRule** consente di modificare le regole di conversione precedentemente configurate per l'utilizzo nell'organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsSipResponseCodeTranslationRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSipResponseCodeTranslationRule"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della regola di conversione da modificare. L'identità di una regola di conversione consta di due parti: l'ambito in cui la regola è stata configurata e il nome assegnato alla regola al momento della creazione. Ad esempio, una regola di conversione denominata Rule404 creata nell'ambito globale avrebbe un'identità simile alla seguente: global/Rule404.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Numero intero</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Priorità relativa della regola di conversione. Le regole vengono elaborate in ordine di priorità; la prima regola elaborata è quella con priorità 0, la seconda regola elaborata è quella con priorità 1 e così via.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceivedISUPCauseValue</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Il valore del codice ISDN User Part (ISUP) che occorre sia presente nel messaggio di risposta SIP utilizzato da gateway, quando si risponde a un messaggio INVITE. Il valore -1 indica che verrà utilizzato solo il codice di risposta SIP per l'esecuzione della regola di conversione; il codice di causa ISUP verrà ignorato.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceivedResponseCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Il valore del codice di risposta SIP utilizzato da un gateway per la risposta a un messaggio INVITE. Un codice di risposta può essere un valore intero compreso tra 400 e 699, inclusi. Sebbene il cmdlet accetti i valori interi minori di 400, questi valori non sono riconosciuti come risposte finali. Di conseguenza, la regola di conversione non verrà mai utilizzata. Il valore 0 significa che verrà utilizzato solo il codice di risposta ISUP per l'esecuzione della regola di conversione; il codice di causa ISUP verrà ignorato.</p></td>
</tr>
<tr class="even">
<td><p><em>TranslatedResponseCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Il valore del codice di risposta SIP nel quale deve essere convertito il codice ReceivedResponseCode e/o ReceivedISUPCauseCode. I codici di risposta convertiti possono essere un valore intero compreso tra 400 e 699, inclusi.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated. Il cmdlet **Set-CsSipResponseCodeTranslationRule** accetta le istanze dell'oggetto regola di conversione dei codici di risposta SIP inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsSipResponseCodeTranslationRule** non restituisce oggetti o valori. Il cmdlet invece modifica le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)  
[New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)  
[Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)

