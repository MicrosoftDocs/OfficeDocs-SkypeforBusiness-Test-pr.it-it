---
title: Get-CsArchivingPolicy
TOCTitle: Get-CsArchivingPolicy
ms:assetid: 25d7de86-871d-4f07-8825-028137365435
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425731(v=OCS.15)
ms:contentKeyID: 49299966
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsArchivingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni relative ai criteri di archiviazione della sessione di messaggistica istantanea. I criteri di archiviazione consentono di archiviare tutte le sessioni delle conferenze Web e di messaggistica istantanea eseguite tra utenti interni e/o tra utenti interni e utenti esterni. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsArchivingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsArchivingPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene chiamato il cmdlet **Get-CsArchivingPolicy** senza alcun parametro. Viene così restituita una raccolta di tutti i criteri di archiviazione attualmente in uso nell'organizzazione,

    Get-CsArchivingPolicy

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il cmdlet **Get-CsArchivingPolicy** per restituire il criterio di archiviazione con Identity site:Redmond. Poiché le identità devono essere univoche, il comando restituirà sempre un criterio al massimo.

    Get-CsArchivingPolicy -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 viene restituita una raccolta di tutti i criteri di archiviazione configurati nell'ambito per utente. A tale scopo, vengono inclusi il parametro Filter e il valore di filtro "tag:\*". Tale valore indica al cmdlet **Get-CsArchivingPolicy** di restituire solo i criteri in cui l'identità inizia con il valore stringa "tag:".

    Get-CsArchivingPolicy -Filter tag:*

## ESEMPIO 4

Nell'esempio 4 viene restituita una raccolta di tutti i criteri di archiviazione in cui è stata disabilitata l'archiviazione delle sessioni di messaggistica istantanea interne. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsArchivingPolicy** per restituire una raccolta di tutti i criteri di archiviazione attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. A sua volta, il cmdlet **Where-Object** applica un filtro che restituisce solo i dati relativi ai criteri in cui la proprietà ArchiveInternal è uguale a False.

    Get-CsArchivingPolicy | Where-Object {$_.ArchiveInternal -eq $False}

## ESEMPIO 5

L'esempio 5 è simile all'esempio 4. In questo caso, il comando però restituisce tutti i criteri di archiviazione in cui è disabilitata l'archiviazione interna ed esterna. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsArchivingPolicy** per restituire una raccolta di tutti i criteri di archiviazione attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui le proprietà ArchiveInternal e ArchiveExternal sono entrambe uguali a False. L'operatore -and indica al cmdlet **Where-Object** di selezionare solo i criteri che soddisfano tutti i requisiti specificati. Per selezionare criteri che soddisfano solo uno o entrambi i requisiti specificati, utilizzare l'operatore -or:

    Get-CsArchivingPolicy | Where-Object {$_.ArchiveInternal -eq $False -and $_.ArchiveExternal -eq $False}

## Descrizione dettagliata

Per molte organizzazioni è utile conservare un archivio di tutte le sessioni di messaggistica istantanea cui prendono parte i propri utenti; altre organizzazioni sono obbligate per legge a detenere un archivio del genere. Per archiviare sessioni di messaggistica istantanea con Lync Server, è necessario eseguire due passaggi. Innanzitutto è necessario abilitare l'archiviazione nell'ambito globale e/o del sito utilizzando il cmdlet **Set-CsArchivingConfiguration**. Questo consente di poter archiviare sessioni di messaggistica istantanea. Tuttavia, l'archiviazione di tali sessioni non viene avviata automaticamente.

Per salvare effettivamente le trascrizioni delle sessioni di messaggistica istantanea, è necessario completare il passaggio 2, ovvero la creazione di uno o più criteri di archiviazione delle sessioni di messaggistica istantanea. Tali criteri determinano per quali utenti vengono registrate le sessioni di messaggistica istantanea e quali tipi di sessioni di messaggistica istantanea (interne e/o esterne) vengono archiviati. Le sessioni di messaggistica istantanea interne sono sessioni in cui tutti i partecipanti sono utenti autenticati che dispongono di account Active Directory all'interno dell'organizzazione. Le sessioni di messaggistica istantanea esterne sono sessioni in cui almeno un partecipante è un utente non autenticato che non dispone di un account Active Directory all'interno dell'organizzazione. È possibile scegliere di archiviare solo le sessioni interne, solo le sessioni esterne oppure entrambi i tipi.

I criteri di archiviazione (creati utilizzando il cmdlet **New-CsArchivingPolicy**) possono essere assegnati ad un ambito di sito o di sito globale. Inoltre, questi criteri possono essere assegnati ad un ambito per utente; ciò significa che si possono creare criteri ed applicarli a utenti specifici o a un gruppo di utenti specifico. Ad esempio, potrebbe essere presente un criterio globale che archivia le sessioni IM interne per tutti gli utenti. In aggiunta, si potrebbe creare un secondo criterio che archivia le sessioni sia interne sia esterne e applicarlo solo al personale addetto alle vendite. Poiché i criteri per utente hanno la precedenza sui criteri globali e di sito, verranno archiviate tutte le sessioni IM dei membri dello staff delle vendite. Per tutti gli altri utenti (cioè quelli che non fanno parte del reparto vendite e che non sono soggetti ai criteri delle vendite) verranno archiviate solamente le sessioni interne di messaggistica istantanea.

Il cmdlet **Get-CsArchivingPolicy** restituisce informazioni relative ai criteri di archiviazione configurati per l'utilizzo nella propria organizzazione. Tenere presente che questi criteri vengono applicati solo se l'archiviazione della sessione IM è stata abilitata nell'ambito globale o di sito. Per determinare se è stata abilitata o meno l'archiviazione della sessione IM, utilizzare il cmdlet **Get-CsArchivingConfiguration**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsArchivingPolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsArchivingPolicy"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare il criterio o i criteri da ottenere. Ad esempio, per ottenere tutti i criteri configurati nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Consente di restituire ogni criterio in cui Identity (l'unica proprietà che è possibile filtrare) inizia con il valore di stringa &quot;site:&quot;. Per ottenere una raccolta di tutti i criteri per utente la cui identità inizia con &quot;Sales&quot;, utilizzare la sintassi seguente: -Filter &quot;Sales*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco dei criteri di archiviazione da restituire. Per fare riferimento al criterio globale, utilizzare la seguente sintassi: -Identity global. Per fare riferimento ad un criterio del sito, usare una sintassi simile alla seguente: -Identity site:Redmond. Per fare riferimento ad un criterio per utente, usare una sintassi simile alla seguente: -Identity RedmondArchivingPolicy. Se questo parametro viene omesso, verranno restituiti tutti i criteri di archiviazione configurati per l'utilizzo nella propria organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dei criteri di archiviazione dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsArchivingPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsArchivingPolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Im.IMArchivingPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)

