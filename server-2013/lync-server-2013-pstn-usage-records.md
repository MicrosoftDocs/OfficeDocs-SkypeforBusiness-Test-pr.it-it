---
title: 'Lync Server 2013: Record utilizzo PSTN'
TOCTitle: Record utilizzo PSTN
ms:assetid: b5f624aa-abe8-455b-a8e3-c228be230463
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412878(v=OCS.15)
ms:contentKeyID: 49301736
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Record utilizzo PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La pianificazione dei record utilizzo PSTN consiste principalmente nell'elencare tutte le autorizzazioni per le chiamate attualmente in vigore nell'organizzazione, dal CEO fino ai dipendenti a tempo determinato, ai consulenti e al personale contingente. Questo processo offre anche la possibilità di riesaminare le autorizzazioni esistenti per le chiamate e modificarle. È possibile creare record utilizzo PSTN solo per le autorizzazioni per le chiamate applicabili agli utenti previsti di VoIP aziendale, ma potrebbe essere una soluzione a lungo termine più efficace creare record utilizzo PSTN per tutte le autorizzazioni per le chiamate, anche se alcune potrebbero non essere al momento applicabili al gruppo di utenti da abilitare per VoIP aziendale. In questo modo, se le autorizzazioni per le chiamate subiscono modifiche o vengono aggiunti nuovi utenti con autorizzazioni diverse per le chiamate, saranno già stati creati i record utilizzo PSTN necessari.

Nella tabella seguente viene illustrata una tipica tabella di record di utilizzo PSTN:

### Record di utilizzo PSTN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo telefono</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Local</p></td>
<td><p>Chiamate locali</p></td>
</tr>
<tr class="even">
<td><p>Long-Distance</p></td>
<td><p>Chiamate interurbane</p></td>
</tr>
<tr class="odd">
<td><p>International</p></td>
<td><p>Chiamate internazionali</p></td>
</tr>
<tr class="even">
<td><p>Delhi</p></td>
<td><p>Dipendenti a tempo pieno di Delhi</p></td>
</tr>
<tr class="odd">
<td><p>Redmond</p></td>
<td><p>Dipendenti a tempo pieno di Redmond</p></td>
</tr>
<tr class="even">
<td><p>RedmondTemps</p></td>
<td><p>Dipendenti a tempo determinato di Redmond</p></td>
</tr>
<tr class="odd">
<td><p>Zurich</p></td>
<td><p>Dipendenti a tempo pieno di Zurigo</p></td>
</tr>
</tbody>
</table>


I record di utilizzo PSTN non svolgono di per sé alcuna funzione. Per utilizzarli, è necessario associarli agli elementi seguenti:

  - Criteri vocali, assegnati agli utenti.

  - Route, assegnate ai numeri di telefono.

Per informazioni dettagliate sui criteri vocali e sulle route, vedere [Criteri vocali in Lync Server 2013](lync-server-2013-voice-policies.md) e [Route vocali in Lync Server 2013](lync-server-2013-voice-routes.md). Per informazioni dettagliate su come crearli e configurarli, vedere [Configurazione di route vocali per le chiamate in uscita in Lync Server 2013](lync-server-2013-configuring-voice-routes-for-outbound-calls.md).

