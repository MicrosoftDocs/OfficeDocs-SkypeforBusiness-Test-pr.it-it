---
title: New-CsSipResponseCodeTranslationRule
TOCTitle: New-CsSipResponseCodeTranslationRule
ms:assetid: f7667ffd-3d11-40ec-87d4-7f9b1a861aae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413041(v=OCS.15)
ms:contentKeyID: 49302500
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSipResponseCodeTranslationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova regola di conversione dei codici di risposta SIP. Queste regole consentono agli amministratori di convertire i codici di risposta SIP con valori compresi tra 400 e 699 in valori utilizzati da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSipResponseCodeTranslationRule -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsSipResponseCodeTranslationRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -TranslatedResponseCode <Int32> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Priority <Int32>] [-ReceivedISUPCauseValue <Int32>] [-ReceivedResponseCode <Int32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 consente di creare una nuova regola di conversione per il codice di risposta SIP con Identity PstnGateway:192.168.0.240/Rule404. Questa regola converte un codice di risposta 434 ricevuto nel codice di risposta SIP standard 404 (Non trovato).

    New-CsSipResponseCodeTranslationRule -Identity "PstnGateway:192.168.0.240/Rule404" -ReceivedResponseCode 434 -TranslatedResponseCode 404

## ESEMPIO 2

Il comando mostrato nell'esempio 2 consente di eseguire la stessa operazione del comando nell'esempio 1 con la differenza che vengono utilizzati i parametri Parent e Name al posto del parametro Identity. In questo modo viene mostrato un modo alternativo di creare una nuova regola di conversione per il codice di risposta SIP con Identity PstnGateway:192.168.0.240/Rule404.

    New-CsSipResponseCodeTranslationRule -Parent "PstnGateway:192.168.0.240" -Name "Rule404" -ReceivedResponseCode 434 -TranslatedResponseCode 404

## Descrizione dettagliata

Il trunking SIP consente di connettersi a una rete VoIP (Voice over Internet Protocol) quale VoIP aziendale mediante PSTN (Public Switched Telephone Network). In Lync Server, Mediation Server utilizza i trunking peer per interagire con la rete PSTN. Quando una chiamata in uscita ha esito negativo nella rete PSTN, viene generato automaticamente un codice di causa ISDN User Part (ISUP). Ad esempio, un gateway PSTN può inviare il codice di causa 34 per indicare che non è disponibile alcun circuito o canale per completare la chiamata. Quando un trunking peer Mediation Server riceve tale codice di causa ISUP, lo converte in un codice di risposta SIP che viene quindi inviato a Mediation Server. Lync Server a sua volta utilizza i codici di risposta per le decisioni relative al routing in uscita. Ad esempio, a un gateway che non funziona correttamente potrebbe essere assegnato automaticamente uno stato di priorità secondaria per limitare l'uso di tale gateway e ottimizzare le possibilità di completare correttamente una chiamata.

Non tutti i gateway utilizzano tuttavia la mappatura del codice di causa ISUP al codice di risposta SIP utilizzata da Lync Server. Per tali gateway, gli amministratori possono utilizzare i cmdlet **CsSipResponseCodeTranslationRule** per mappare il codice di risposta SIP del gateway (insieme al codice di causa ISUP, se disponibile) a un codice di risposta SIP utilizzato da Lync Server. Ad esempio, un gateway potrebbe mappare il codice di causa ISUP 34 (nessun circuito/canale disponibile) al codice di risposta SIP 486 (Non disponibile qui). In base al codice di risposta 486, la logica di routing in uscita di Lync Server non tenterà di trovare un altro gateway per completare la chiamata.

Nel caso di Lync Server, tale codice di risposta SIP 486 deve invece essere mappato al codice di risposta SIP 503, che attiva un meccanismo di ripetizione nella logica di routing in uscita di Lync Server. Di conseguenza, il sistema tenterà di trovare un altro gateway per completare la chiamata. Per gestire questa situazione, è possibile creare una regola di conversione che associ la combinazione di codice di causa ISUP 34 e codice di risposta SIP 486 a un codice di risposta SIP 503. Queste nuove regole di conversione vengono create utilizzando il cmdlet **New-CsSipResponseCodeTranslationRule**. È possibile assegnare le regole di conversione all'ambito globale, di sito e di servizio (solo per servizio Gateway PSTN).

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsSipResponseCodeTranslationRule** in locale: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsSipResponseCodeTranslationRule"}

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
<td><p>Identificatore univoco per la regola di conversione da creare. L'identità di una regola di conversione è composta da due parti: l'ambito di assegnazione della regole e il nome da assegnare alla regola. Ad esempio, una regola di conversione denominata Rule404 da creare in ambito globale avrebbe un'identità di questo tipo: global/Rule404.</p>
<p>Anziché utilizzare il parametro Identity, è possibile utilizzare i parametri Parent e Name per creare una nuova regola di conversione.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome utilizzato per differenziale le singole regole di conversione. I nomi devono essere univoci all'interno di un ambito, ad esempio, il sito Redmond può avere solo una regola di conversione denominata Rule404. È tuttavia possibile avere una regole di conversione denominata Rule404 nel sito Redmond e un'altra regola denominata Rule404 nel sito Dublin.</p>
<p>Il parametro Name deve essere sempre utilizzato insieme al parametro Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito di assegnazione della nuova regola di conversione. Per assegnare una regola all'ambito globale, utilizzare la sintassi seguente: -Parent global. Per assegnare una regola all'ambito del sito, utilizzare la sintassi seguente: -Parent site:Redmond. Per assegnare una regola all'ambito del servizio, utilizzare la sintassi seguente: -Parent PstnGateway:192.168.0.242.</p>
<p>Il parametro Parent deve essere sempre utilizzato insieme al parametro Name.</p></td>
</tr>
<tr class="even">
<td><p><em>TranslatedResponseCode</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Valore del codice di risposta SIP di Lync Server in cui deve essere convertito ReceivedResponseCode e/o ReceivedISUPCauseCode. I codici di risposta convertiti possono essere un valore intero compreso tra 400 e 699 inclusi.</p></td>
</tr>
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
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Priorità relativa della regola di conversione. Le regole vengono elaborate in base alla priorità assegnata, ovvero la prima regola ad essere elaborata ha la priorità 0, la seconda ha la priorità 1 e così via. Se non viene specificata alcuna priorità, alla nuova regola verrà assegnata la priorità più bassa nell'ambito.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReceivedISUPCauseValue</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Valore del codice ISUP (ISDN User Part) che deve essere presente nel messaggio di risposta SIP utilizzato da un gateway quando risponde a un messaggio INVITE. Il valore -1 indica che verrà utilizzato solo il codice di risposta SIP quando si esegue la regola di conversione, mentre il codice di causa ISUP verrà ignorato.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceivedResponseCode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Valore del codice di risposta SIP utilizzato da un gateway quando risponde a un messaggio INVITE. Un codice di risposta può essere un valore intero compreso tra 400 e 699 inclusi. Sebbene il cmdlet accetti valori interi inferiori a 400, questi non vengono riconosciuti come risposte finali. Di conseguenza, la regola di conversione non verrà mai utilizzata. Il valore 0 indica che verrà utilizzato solo il codice di causa ISUP quando si esegue la regola di conversione, mentre il codice di risposta SIP verrà ignorato.</p></td>
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

Nessuno. Il cmdlet **New-CsSipResponseCodeTranslationRule** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsSipResponseCodeTranslationRule** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.SipResponseCodeTRanslationRule\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsSipResponseCodeTranslationRule](get-cssipresponsecodetranslationrule.md)  
[Remove-CsSipResponseCodeTranslationRule](remove-cssipresponsecodetranslationrule.md)  
[Set-CsSipResponseCodeTranslationRule](set-cssipresponsecodetranslationrule.md)

