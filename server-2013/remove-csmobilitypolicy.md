---
title: Remove-CsMobilityPolicy
TOCTitle: Remove-CsMobilityPolicy
ms:assetid: d3dc4653-25ab-45ef-b325-fba01e45acca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690048(v=OCS.15)
ms:contentKeyID: 49302069
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMobilityPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un criterio per dispositivi mobili esistente. I criteri per dispositivi mobili determinano se un utente può o meno utilizzare la funzionalità Chiamata tramite ufficio, che consente agli utenti di effettuare e ricevere chiamate telefoniche sul cellulare utilizzando il numero dell'ufficio anziché quello del cellulare. I criteri per dispositivi mobili possono essere utilizzati anche per richiedere connessioni Wi-Fi quando si effettuano o ricevono chiamate.Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Remove-CsMobilityPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di rimuovere il criterio per dispositivi mobili configurato per il sito Redmond. Quando il criterio viene rimosso, gli utenti in precedenza gestiti dal criterio per il sito Redmond vengono gestiti dal criterio globale.

    Remove-CsMobilityPolicy -Identity "site:Redmond"

## ESEMPIO 2

Nell'esempio 2 vengono rimossi tutti i criteri per dispositivi mobili configurati nell'ambito per utente. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsMobilityPolicy** e il parametro Filter per recuperare tutti i criteri con valore Identity che inizia con il valore stringa "Tag:". Per definizione, qualsiasi criterio che soddisfa questa regola è un criterio per utente. La raccolta di criteri per utente viene quindi inviata tramite pipe al cmdlet **Remove-CsMobilityPolicy**, che elimina ogni criterio nella raccolta.

    Get-CsMobilityPolicy -Filter "tag:*" | Remove-CsMobilityPolicy

## ESEMPIO 3

Nell'esempio 3 viene illustrato come eliminare tutti i criteri per dispositivi mobili in cui la caratteristica Chiamata tramite ufficio è stata abilitata. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsMobilityPolicy** per recuperare una raccolta di tutti i criteri per dispositivi mobili attualmente in uso nell'organizzazione. Tale raccolta viene quindi inviata tramite pipe al cmdlet where-Object, che preleva solo i criteri in cui la proprietà EnableOutsideVoice è impostata su False. Tali criteri vengono quindi inviati tramite pipe al cmdlet **Remove-CsMobilityPolicy**, che provvede alla loro rimozione.

    Get-CsMobilityPolicy | Where-Object {$_.EnableOutsideVoice -eq $False} | Remove-CsMobilityPolicy

## Descrizione dettagliata

Lync Mobile è un'applicazione client che consente agli utenti di eseguire Lync nei cellulari. La caratteristica Chiamata tramite ufficio consente agli utenti di effettuare chiamate con il cellulare che risultano provenire dal numero dell'ufficio anziché da quello del cellulare. Gli utenti abilitati per la caratteristica Chiamata tramite ufficio possono ottenere questo risultato componendo il numero direttamente dal cellulare oppure utilizzando l'opzione di conferenza telefonica con chiamata in uscita. Con questa opzione, un utente richiede in effetti al server dei servizi per dispositivi mobili di effettuare una chiamata al suo posto. La chiamata viene configurata dal server e quindi l'utente viene richiamato sul cellulare. Dopo che l'utente ha risposto, il server compone il numero della parte chiamata. Entrambe queste funzionalità possono essere gestite tramite i criteri per dispositivi mobili.

Con Lync Server 2013, i dispositivi mobili possono effettuare o ricevere chiamate tramite la rete cellulare standard oppure tramite connessioni Wi-Fi. I criteri per dispositivi mobili possono essere utilizzati per richiedere connessioni Wi-Fi e impedire le chiamate tramite la rete cellulare.

Quando si installa Lync Server, è presente un singolo criterio per dispositivi mobili globale che si applica a tutti gli utenti. Gli amministratori possono tuttavia utilizzare il cmdlet **New-CsMobilityPolicy** per creare criteri personalizzati nell'ambito del sito o per utente.

Se si creano criteri personalizzati nell'ambito del sito o per utente, è successivamente possibile eliminare questi criteri utilizzando il cmdlet **Remove-CsMobilityPolicy**. Se si elimina un criterio per utente, gli utenti assegnati a tale criterio verranno gestiti dal criterio del sito appropriato (se disponibile) o dal criterio globale. Se si rimuove un criterio del sito, gli utenti controllati da tale criterio verranno gestiti dal criterio globale.

Si noti che è anche possibile eseguire il cmdlet **Remove-CsMobilityPolicy** sul criterio globale. Eseguendo questa operazione, tuttavia, il criterio globale non viene effettivamente eliminato, ma vengono ripristinati i valori predefiniti delle proprietà di tale criterio. In questo caso ciò significa che viene abilitata la caratteristica Chiamata tramite ufficio.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsMobilityPolicy** in locale: RTCUniversalServerAdmins.

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
<td><p>Identificatore univoco del criterio client da rimuovere. Per &quot;rimuovere&quot; il criterio globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Si noti, tuttavia, che il criterio globale non può essere realmente rimosso, ma vengono ripristinati i valori predefiniti di tutte le proprietà.</p>
<p>Per rimuovere un criterio del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per rimuovere un criterio per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;SalesDepartmentPolicy&quot;</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica l'identità di un criterio.</p></td>
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
<td><p>Se questo parametro è presente, i criteri verranno rimossi anche se sono assegnati ad almeno un utente. Se questo parametro non è presente, il cmdlet <strong>Remove-CsMobilityPolicy</strong> non rimuoverà automaticamente i criteri per utente assegnati ad almeno un utente. Verrà invece visualizzato un messaggio in cui viene richiesto di confermare la rimozione dei criteri. Per procedere con l'operazione e rimuovere i criteri, è necessario rispondere Sì (premendo il tasto S).</p>
<p>Questo parametro si applica solo ai criteri per utente.</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility. Il cmdlet **Remove-CsMobilityPolicy** accetta istanze inviate tramite pipeline dell'oggetto Mobility.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsMobilityPolicy** elimina le istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Policy.Mobility.Mobility.

