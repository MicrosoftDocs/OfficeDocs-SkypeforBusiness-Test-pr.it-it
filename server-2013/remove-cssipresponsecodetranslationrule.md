---
title: Remove-CsSipResponseCodeTranslationRule
TOCTitle: Remove-CsSipResponseCodeTranslationRule
ms:assetid: beb5f508-5f90-46ee-b5c5-7da8781420e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412932(v=OCS.15)
ms:contentKeyID: 49301830
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsSipResponseCodeTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una regola di conversione dei codici di risposta SIP. Queste regole consentono agli amministratori di convertire i codici di risposta SIP con valori compresi tra 400 e 699 in valori utilizzati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsSipResponseCodeTranslationRule -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 elimina una regola di conversione del codice di risposta singola: la regola con identità PstnGateway:192.168.0.240/Rule404.

    Remove-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404"

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le regole di conversione del codice di risposta dal gateway PSTN 192.168.0.240. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsSipResponseCodeTranslationRule** insieme al parametro Filter. Il valore di filtro "service:PstnGateway:192.168.0.240/\*" circoscrive i dati restituiti limitandoli alle regole con identità (Identity) che inizia con il valore stringa "service:PstnGateway:192.168.0.240/". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsSipResponseTranslationCode**, che elimina ogni regola della raccolta.

    Get-CsSipResponseCodeTranslationRule -Filter "service:PstnGateway:192.168.0.240/*" | Remove-CsSipResponseTranslationCode

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le regole di conversione dei codici di risposta in cui non è stato configurato alcun valore per la proprietà ReceivedISUPCauseValue. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsSipResponseCodeTranslationRule** senza alcun parametro per restituire una raccolta di tutte le regole di conversione dei codici di risposta attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà ReceivedISUPCauseValue è uguale a -1.

A questo punto, la raccolta filtrata viene inviata tramite pipe al cmdlet **Remove-CsSipResponseTranslationCode**, che elimina ogni regola della raccolta.

    Get-CsSipResponseCodeTranslationRule | Where-Object {$_.ReceivedISUPCauseValue -eq -1} | Remove-CsSipResponseTranslationCode

## Descrizione dettagliata

Il trunking SIP consente di connettere una rete VoIP (Voice over Internet Protocol), quale VoIP aziendale, alla rete PSTN (Public Switched Telephone Network). In Lync Server il Mediation Server utilizza i peer di trunking per interagire con la rete PSTN. Se si verifica un errore per una chiamata in uscita sulla rete PSTN, viene generato automaticamente un codice di causa ISUP (ISDN User Part). Un gateway PSTN ad esempio può inviare un codice di causa 34 per indicare che non erano disponibili circuiti o canali per eseguire la chiamata. Quando un peer di trunking del Mediation Server riceve tale codice di causa ISUP, lo converte in un codice di risposta SIP che viene quindi inviato al Mediation Server. In Lync Server questi codici di risposta vengono utilizzati per le decisioni relative al routing in uscita. Ad esempio, a un gateway che non funziona correttamente potrebbe essere assegnato automaticamente uno stato di priorità secondaria per limitare l'utilizzo di tale gateway e ottimizzare le possibilità di completare correttamente una chiamata.

Non in tutti i gateway tuttavia viene utilizzato il mapping consigliato tra codice di causa ISUP e codice di risposta SIP utilizzato da Lync Server. Per tali gateway, gli amministratori possono utilizzare i cmdlet **CsSipResponseCodeTranslationRule** per mappare il codice di risposta SIP del gateway SIP (insieme al codice di causa ISUP, se disponibile) a un codice di risposta SIP utilizzato da Lync Server. Ad esempio, un gateway potrebbe mappare il codice di causa ISUP 34 (nessun circuito/canale disponibile) al codice di risposta SIP 486 (non disponibile qui). In base a un codice di risposta 486, la logica del routing in uscita di Lync Server non tenterà di trovare un nuovo gateway per eseguire la chiamata.

Per Lync Server tuttavia il codice di risposta SIP 486 deve essere invece mappato al codice di risposta SIP 503, che attiva il meccanismo di ripetizione dell'operazione nella logica del routing in uscita di Lync Server. Il sistema pertanto tenterà di trovare un altro gateway per eseguire la chiamata. Per gestire questa situazione, è possibile creare una regola di conversione per mappare la combinazione di codice di causa ISUP 34 e di codice di risposta SIP 486 a un codice di risposta SIP 503.

Il cmdlet **Remove-CsSipResponseCodeTranslationRule** consente di eliminare tutte le regole di conversione precedentemente configurate per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsSipResponseCodeTranslationRule** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati) utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsSipResponseCodeTranslationRule"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la regola di conversione da eliminare. L'identità di una regola di conversione è composta da due parti: l'ambito in cui è stata configurata la regola e il nome assegnato alla regola al momento della creazione. Ad esempio, una regola di conversione denominata Rule404 che sia stata creata nell'ambito globale avrebbe un'identità analoga alla seguente: global/Rule404.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated. Il cmdlet **Remove-CsSipResponseCodeTranslationRule** accetta le istanze da pipeline dell'oggetto regola di conversione dei codici di risposta SIP.

## Tipi restituiti

Il cmdlet **Remove-CsSipResponseCodeTranslationRule** non restituisce alcun oggetto o valore. Elimina invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTranslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)  
[New-CsSipResponseCodeTranslationRule](new-cssipresponsecodetranslationrule.md)  
[Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

