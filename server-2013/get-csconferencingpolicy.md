---
title: Get-CsConferencingPolicy
TOCTitle: Get-CsConferencingPolicy
ms:assetid: 21dc4774-2306-4425-a561-71e0b293f8df
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398293(v=OCS.15)
ms:contentKeyID: 49299918
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferencingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui criteri conferenza configurati per l'utilizzo nell'organizzazione. I criteri conferenza determinano le funzionalità e le caratteristiche che è possibile utilizzare in una conferenza, ad esempio se includere o meno nella conferenza le funzionalità audio e video IP o il numero massimo di persone che possono partecipare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsConferencingPolicy [-Identity <XdsIdentity>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    Get-CsConferencingPolicy [-Filter <String>] [[-ApplicableTo] <Object>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nel primo esempio viene restituita una raccolta di tutti i criteri conferenza configurati per l'utilizzo nell'organizzazione.

    Get-CsConferencingPolicy

## ESEMPIO 2

Nell'Esempio 2 viene utilizzato il parametro Identity per limitare le informazioni recuperate in modo da includere esclusivamente i criteri relativi alle conferenze con identità uguale a Global. Dal momento che le identità dei criteri devono essere univoche, questo comando restituisce un unico criterio: il criterio globale (Global).

    Get-CsConferencingPolicy -Identity Global

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per ottenere una raccolta di tutti i criteri conferenza che sono stati configurati nell'ambito per utente. Il valore con carattere jolly "tag:\*" indica a Windows PowerShell di restituire solo i criteri conferenza in cui l'identità inizia con la stringa “tag:”.

    Get-CsConferencingPolicy -Filter tag:*

## ESEMPIO 4

Nell'Esempio 4, viene restituita una raccolta di tutti i criteri relativi alle conferenze in cui la proprietà MaxMeetingSize è maggiore di 100. Il comando utilizza per primo il cmdlet **Get-CsConferencingPolicy** per ottenere una raccolta di tutti i criteri relativi alle conferenze configurati per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che filtra i dati restituiti per ottenere solo quelli in cui la proprietà MaxMeetingSize è maggiore di 100.

    Get-CsConferencingPolicy | Where-Object {$_.MaxMeetingSize -gt 100}

## ESEMPIO 5

Nell'esempio 5 vengono restituiti tutti i criteri di conferenza che soddisfano due requisiti: la proprietà AllowExternalUsersToSaveContent è uguale a True e la proprietà AllowExternalUserControl è anch'essa uguale a True. A tale scopo, il comando chiama il cmdlet **Get-CsConferencingPolicy** senza parametri aggiuntivi. In questo modo viene restituita una raccolta di tutti i criteri di conferenza configurati per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui le proprietà AllowExternalUsersToSaveContent e AllowExternalUserControl sono entrambe impostate su True. L'operatore -and indica al cmdlet **Where-Object** che deve restituire esclusivamente gli oggetti che soddisfano tutti i requisiti specificati.

    Get-CsConferencingPolicy | Where-Object {$_.AllowExternalUsersToSaveContent -eq $True -and $_.AllowExternalUserControl -eq $True}

## ESEMPIO 6

L'esempio 6 è una variante del comando riportato nell'esempio 5. In questo caso, il comando restituisce qualsiasi criterio che soddisfa almeno uno dei criteri specificati (non necessariamente entrambi): la proprietà AllowExternalUsersToSaveContent è uguale a True e/o la proprietà AllowExternalUserControl è anch'essa uguale a True. A tale scopo, il comando chiama il cmdlet **Get-CsConferencingPolicy** senza alcun parametro aggiuntivo. Viene così restituita una raccolta di tutti i criteri di conferenza configurati per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà AllowExternalUsersToSaveContent e/o la proprietà AllowExternalUserControl sono uguali a True. L'operatore -or indica al cmdlet **Where-Object** che è sufficiente che un oggetto soddisfi uno dei criteri specificati per essere restituito.

    Get-CsConferencingPolicy | Where-Object {$_.AllowExternalUsersToSaveContent -eq $True -or $_.AllowExternalUserControl -eq $True}

## Descrizione dettagliata

Le conferenze rappresentano un aspetto importante di Lync Server: le conferenze consentono ai gruppi di utenti di incontrarsi online per visualizzare diapositive e video, condividere applicazioni, scambiare file, comunicare e collaborare in altro modo.

Per gli amministratori è importante mantenere il controllo sulle conferenze e sulle impostazioni della conferenza. In alcuni casi potrebbero esserci problemi di sicurezza: per impostazione predefinita, chiunque, inclusi gli utenti non autenticati, può partecipare alle riunioni e salvare le presentazioni o gli stampati distribuiti durante queste riunioni. In altri casi potrebbero esserci problemi di larghezza di banda: molte riunioni contemporaneamente, ciascuna con centinaia di partecipanti e con feed video e scambio di file, possono causare dei problemi sulla rete. In aggiunta, possono esserci occasionali problemi legali. Ad esempio, per impostazione predefinita i partecipanti alla riunione possono effettuare annotazioni sui contenuti condivisi, tuttavia queste annotazioni non vengono salvate quando la riunione viene archiviata. Se l'organizzazione è tenuta a conservare tutte le comunicazioni elettroniche, potrebbe essere opportuno disabilitare le annotazioni.

A fronte della necessità di gestire le impostazioni delle conferenze, naturalmente è necessario valutare come eseguire tale gestione. In Lync Server le conferenze vengono gestite con criteri specifici. Nelle versioni precedenti del software questi erano noti come criteri delle riunioni. Come già detto, i criteri di conferenza consentono di stabilire le caratteristiche e le funzionalità che è possibile utilizzare in una conferenza. Ciò include praticamente qualsiasi aspetto, dallo stabilire se la riunione può includere o meno audio e video IP fino al numero massimo di persone che possono partecipare a una riunione. I criteri di conferenza possono essere configurati nell'ambito globale, del sito o del singolo utente. Questo garantisce agli amministratori una notevole flessibilità nel decidere quali funzionalità rendere disponibili per ogni utente.

Il cmdlet **Get-CsConferencingPolicy** consente di ottenere informazioni sui criteri relativi alle conferenze configurati per l'utilizzo nella propria organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsConferencingPolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferencingPolicy"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare i criteri o il criterio relativo alle conferenze da ottenere. Ad esempio, per ottenere tutti i criteri configurati nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per ottenere una raccolta di tutti i criteri configurati nell'ambito di un singolo utente, utilizzare la seguente sintassi: -Filter tag:*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio relativo alle conferenze da recuperare. È possibile configurare i criteri relativi alle conferenze nell'ambito globale, del sito o di un singolo utente. Per recuperare i criteri globali, utilizzare la seguente sintassi: -Identity global. Per recuperare un criterio a livello di sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per recuperare un criterio a livello di singolo utente, utilizzare una sintassi simile alla seguente: -Identity SalesConferencingPolicy.</p>
<p>Se questo parametro non è incluso, il cmdlet <strong>Get-CsConferencingPolicy</strong> restituisce una raccolta di tutti i criteri di conferenza configurati per l'utilizzo nell'organizzazione.</p>
<p>Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità. Utilizzare i parametro Filter se si desidera utilizzare i caratteri jolly quando si specifica un criterio relativo alle conferenze.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dei criteri relativi alle conferenze dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsConferencingPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsConferencingPolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Meeting.MeetingPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)  
[New-CsConferencingPolicy](new-csconferencingpolicy.md)  
[Remove-CsConferencingPolicy](remove-csconferencingpolicy.md)  
[Set-CsConferencingPolicy](set-csconferencingpolicy.md)

