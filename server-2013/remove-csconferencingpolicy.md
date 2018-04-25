---
title: Remove-CsConferencingPolicy
TOCTitle: Remove-CsConferencingPolicy
ms:assetid: 8fe81ace-d167-414b-9455-8be7ddc0cab5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398728(v=OCS.15)
ms:contentKeyID: 49301308
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il criterio conferenza specificato. I criteri conferenza determinano le funzionalità e le caratteristiche che è possibile utilizzare in una conferenza, ad esempio se includere o meno nella conferenza le funzionalità audio e video IP e il numero massimo di persone che possono partecipare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsConferencingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsConferencingPolicy** per eliminare i criteri di conferenza con identità (Identity) SalesConferencingPolicy.

    Remove-CsConferencingPolicy -Identity SalesConferencingPolicy

## ESEMPIO 2

Nell'esempio 2 vengono eliminati tutti i criteri di conferenza configurati nell'ambito del sito. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsConferencingPolicy** e il parametro Filter per restituire una raccolta di tutti i criteri nell'ambito del sito. Il valore di filtro "site:\*" fa in modo che vengano restituite solo i criteri in cui l'identità (Identity) inizia con il valore stringa "site". Tale raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsConferencingPolicy**, che elimina ogni elemento della raccolta.

    Get-CsConferencingPolicy -Filter "site:*" | Remove-CsConferencingPolicy

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i criteri che consentono una dimensione massima della riunione (MaxMeetingSize) superiore a 100 persone. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsConferencingPolicy** per recuperare una raccolta di tutti i criteri di conferenza configurati per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro per restituire solo i dati relativi ai criteri in cui il valore di MaxMeetingSize è maggiore di 100. La raccolta filtrata viene quindi inviata al cmdlet **Remove-CsConferencingPolicy**, che elimina tutti i criteri della raccolta filtrata.

    Get-CsConferencingPolicy | Where-Object {$_.MaxMeetingSize -gt 100} | Remove-CsConferencingPolicy 

## Descrizione dettagliata

Le conferenze rappresentano un aspetto importante di Lync Server: le conferenze consentono ai gruppi di utenti di incontrarsi online per visualizzare diapositive e video, condividere applicazioni, scambiare file, comunicare e collaborare in altro modo.

Per gli amministratori è importante mantenere il controllo sulle conferenze e sulle impostazioni della conferenza. In alcuni casi potrebbero esserci problemi di sicurezza: per impostazione predefinita, chiunque, inclusi gli utenti non autenticati, può partecipare alle riunioni e salvare le presentazioni o gli stampati distribuiti durante queste riunioni. In altri casi potrebbero esserci problemi di larghezza di banda: molte riunioni contemporaneamente, ciascuna con centinaia di partecipanti e con feed video e scambio di file, possono causare dei problemi sulla rete. In aggiunta, potrebbero insorgere occasionali problemi legali. Ad esempio, per impostazione predefinita i partecipanti alla riunione possono effettuare annotazioni sui contenuti condivisi, tuttavia queste annotazioni non vengono salvate quando la riunione viene archiviata. Se l'organizzazione è tenuta a conservare tutte le comunicazioni elettroniche, potrebbe essere opportuno disabilitare le annotazioni.

A fronte della necessità di gestire le impostazioni delle conferenze, naturalmente è necessario valutare come eseguire tale gestione. In Lync Server le conferenze vengono gestite con criteri specifici. Nelle versioni precedenti del software questi erano noti come criteri delle riunioni. Come già detto, i criteri di conferenza consentono di stabilire le caratteristiche e le funzionalità che è possibile utilizzare in una conferenza. Ciò include praticamente qualsiasi aspetto, dallo stabilire se la riunione può includere o meno audio e video IP fino al numero massimo di persone che possono partecipare a una riunione. I criteri di conferenza possono essere configurati nell'ambito globale, del sito o del singolo utente. Questo garantisce agli amministratori una notevole flessibilità nel decidere quali funzionalità rendere disponibili per ogni utente.

È possibile utilizzare il cmdlet **Remove-CsConferencingPolicy** per eliminare i criteri di conferenza configurati per l'utilizzo nella propria organizzazione, ad eccezione dei criteri globali. Il cmdlet **Remove-CsConferencingPolicy** può anche essere eseguito per il criterio globale. In questo caso però i criteri non vengono effettivamente rimossi. Vengono invece ripristinati i valori predefiniti di tutte le proprietà dei criteri globali

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsConferencingPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingPolicy"}

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
<td><p>Identificatore univoco del criterio relativo alle conferenze da rimuovere. È possibile configurare i criteri relativi alle conferenze nell'ambito globale, del sito o per utente. Per rimuovere il criterio globale, utilizzare la seguente sintassi: -Identity global. Si noti che non è possibile eliminare un criterio globale. Ciò che accade è che per tutte le proprietà dei criteri verranno ripristinati i valori predefiniti. Per eliminare criteri del sito, usare una sintassi simile alla seguente: -Identity site:Redmond. Per eliminare criteri per utente, usare una sintassi simile alla seguente: -Identity SalesConferencingPolicy.</p>
<p>I caratteri jolly non sono consentiti quando si specifica una identità.</p></td>
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
<td><p>Se presente, consente al cmdlet <strong>Remove-CsConferencingPolicy</strong> di eliminare il criterio per singolo utente, anche se tale criterio è attualmente assegnato ad almeno un utente. Se non è presente, verrà richiesto di confermare la richiesta di eliminazione prima di rimuovere i criteri.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy. Il cmdlet **Remove-CsConferencingPolicy** accetta istanze dell'oggetto criterio riunione inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Remove-CsConferencingPolicy** non restituisce alcun oggetto o valore. Elimina invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Meeting.MeetingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingPolicy](get-csconferencingpolicy.md)  
[Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Set-CsConferencingPolicy](set-csconferencingpolicy.md)

