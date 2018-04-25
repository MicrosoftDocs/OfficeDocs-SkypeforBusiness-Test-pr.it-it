---
title: Remove-CsAnnouncement
TOCTitle: Remove-CsAnnouncement
ms:assetid: a3c62d15-1b0a-49d3-973f-abc06c730bb2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412766(v=OCS.15)
ms:contentKeyID: 49301544
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAnnouncement

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un annuncio di Lync Server esistente. Gli annunci vengono riprodotti quando gli utenti compongono un numero di telefono valido ma non assegnato. Un annuncio può essere rappresentato da un messaggio, ad esempio "Questo numero è momentaneamente fuori servizio", oppure da un segnale di occupato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsAnnouncement -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene rimosso l'annuncio con l'identità "ApplicationServer:Redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90". Poiché le identità devono essere univoche, questo comando rimuoverà al massimo un solo annuncio.

    Remove-CsAnnouncement -Identity "ApplicationServer:Redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90"

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti gli annunci applicati al servizio ApplicationServer:Redmond.litwareinc.com. A tale scopo, viene chiamato il cmdlet **Remove-CsAnnouncement** insieme al parametro Identity. Se si specifica il valore di parametro "ApplicationServer:Redmond.litwareinc.com" (senza il GUID che consente di identificare un annuncio univoco), vengono rimossi tutti gli annunci configurati per il servizio specificato.

    Remove-CsAnnouncement -Identity "ApplicationServer:Redmond.litwareinc.com"

## Descrizione dettagliata

Un'organizzazione può disporre di numeri di telefono non assegnati a utenti o telefoni, ma che sono comunque numeri validi per le chiamate. Per impostazione predefinita, quando un utente compone uno di questi numeri, riceve un segnale di occupato e la chiamata può generare un errore restituito al client SIP. Applicando le impostazioni di annuncio ai numeri non assegnati, gli amministratori possono decidere di riprodurre un messaggio, restituire un segnale di occupato o reindirizzare la chiamata. Questo cmdlet consente di rimuovere una o più di queste impostazioni di annuncio.

Se si tenta di rimuovere un annuncio che è associato a un intervallo di numeri non assegnati, per impostazione predefinita, viene visualizzato un prompt che richiede se si desidera realmente rimuovere l'annuncio. Se si elimina l'annuncio, la proprietà AnnouncementName di tale intervallo verrà visualizzata con valore Null e quando vengono composti questi numeri, non verrà riprodotto alcun annuncio, bensì solo il segnale di occupato. Il valore della proprietà AnnouncementId, ovvero il GUID dell'annuncio rimosso, tuttavia continuerà a essere visibile.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsAnnouncement** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsAnnouncement"}

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
<td><p>Un identificatore univoco dell'annuncio che si desidera rimuovere. Il valore per il parametro Identity può essere fornito in uno dei seguenti modi:</p>
<p>- Immettere l'identità del Servizio applicazione per gli annunci che si desidera rimuovere. In tal modo, verranno rimossi tutti gli annunci configurati che presentano l'identità del servizio fornita. Ad esempio, ApplicationServer:Redmond.litwareinc.com.</p>
<p>- Immettere l'identità completa del singolo annuncio che si desidera rimuovere. Questo valore sarà sempre nel formato &lt;IDservizio&gt;/&lt;GUID&gt;, dove IDservizio è l'identità del server applicazioni nel quale è in esecuzione il Servizio annunci, mentre GUID è un identificatore univoco globale associato a questo annuncio. Ad esempio: ApplicationServer:Redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c.</p>
<p></p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Nessuno.

## Tipi restituiti

Elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement.

## Vedere anche

#### Ulteriori risorse

[New-CsAnnouncement](new-csannouncement.md)  
[Set-CsAnnouncement](set-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)

