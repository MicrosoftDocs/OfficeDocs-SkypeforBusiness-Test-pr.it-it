---
title: Remove-CsArchivingPolicy
TOCTitle: Remove-CsArchivingPolicy
ms:assetid: 41f11a99-14f1-4292-9d58-eb7a7761b829
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425924(v=OCS.15)
ms:contentKeyID: 49300335
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsArchivingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove i criteri di archiviazione della messaggistica istantanea specificati. Questi criteri determinano se Lync Server salverà automaticamente tutte le sessioni di messaggistica istantanea tra utenti interni e/o tutte le sessioni di messaggistica istantanea tra utenti interni e partner federati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsArchivingPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsArchivingPolicy** per eliminare il criterio con identità (Identity) site:Redmond. Quando viene eliminato un criterio configurato nell'ambito del sito, agli utenti precedentemente gestiti da tale criterio verrà automaticamente applicato il criterio di archiviazione globale.

    Remove-CsArchivingPolicy -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimossi tutti i criteri di archiviazione configurati nell'ambito del sito. A tale scopo, vengono utilizzati il cmdlet **Get-CsArchivingPolicy** e il parametro Filter per restituire una raccolta di tutti i criteri di archiviazione assegnati nell'ambito del sito. Per eseguire questa operazione, viene utilizzato il valore di filtro "site:\*", che indica al cmdlet **Get-CsArchivingPolicy** di restituire solo i criteri la cui identità inizia con "site:". Dopo la restituzione della raccolta, i dati vengono inviati tramite pipe al cmdlet **Remove-CsArchivingPolicy**, che elimina tutti i criteri della raccolta.

    Get-CsArchivingPolicy -Filter site:* | Remove-CsArchivingPolicy

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti i criteri di archiviazione in cui la proprietà ArchiveExternal è impostata su False. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsArchivingPolicy** per restituire una raccolta di tutti i criteri di archiviazione configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà ArchiveExternal è uguale a False. La raccolta filtrata viene quindi passata al cmdlet **Remove-CsArchivingPolicy**, che elimina ogni criterio della raccolta.

    Get-CsArchivingPolicy | Where-Object {$_.ArchiveExternal -eq $False} | Remove-CsArchivingPolicy 

## Descrizione dettagliata

Molte organizzazioni considerano utile la possibilità di conservare tutte le sessioni di messaggistica istantanea a cui partecipano gli utenti, mentre altre organizzazioni sono tenute a mantenerle come archivi per vincoli legali. Per archiviare le sessioni di messaggistica istantanea con Lync Server, è necessario eseguire due passaggi. Abilitare innanzitutto l'archiviazione nell'ambito globale e/o del sito utilizzando il cmdlet **Set-CsArchivingConfiguration**. In questo modo è possibile archiviare le sessioni di messaggistica istantanea. L'archiviazione di tali sessioni tuttavia non inizia automaticamente.

Per salvare effettivamente le trascrizioni delle sessioni di messaggistica istantanea, è necessario completare il passaggio 2, ovvero la creazione di uno o più criteri di archiviazione. Tali criteri determinano per quali utenti vengono registrate le sessioni di messaggistica istantanea oltre ai tipi di sessioni di messaggistica istantanea (interne e/o esterne) che vengono archiviati. Le sessioni di messaggistica istantanea interne sono sessioni in cui tutti i partecipanti sono utenti autenticati che dispongono di account Active Directory all'interno dell'organizzazione. Le sessioni di messaggistica istantanea esterne sono sessioni in cui almeno un partecipante è un utente non autenticato che non dispone di un account Active Directory all'interno dell'organizzazione. È possibile scegliere di archiviare solo le sessioni interne, solo le sessioni esterne oppure entrambi i tipi.

I criteri di archiviazione possono essere assegnati nell'ambito globale o del sito. Tali criteri possono inoltre essere assegnati nell'ambito per utente e quindi essere applicati a un utente o a un gruppo di utenti specifico. Si supponga, ad esempio, che il criterio globale in uso consenta di archiviare solo le sessioni di messaggistica istantanea interne per tutti gli utenti. In questo caso, si potrebbe creare un secondo criterio per archiviare sia le sessioni interne che quelle esterne e applicare il criterio solo al personale addetto alle vendite. Poiché i criteri per utente hanno la precedenza sui criteri globali e di sito, per i membri dello staff di vendita verranno archiviate tutte le sessioni di messaggistica istantanea. Per tutti gli altri utenti, ovvero gli utenti che non appartengono al reparto vendite e a cui non viene applicato il criterio relativo alle vendite, verranno archiviate solamente le sessioni di messaggistica istantanea interne.

Il cmdlet **Remove-CsArchivingPolicy** consente di eliminare un criterio di archiviazione creato e utilizzato nell'organizzazione. Se si elimina un criterio per utente, tutti gli utenti ai quali era stato assegnato quel criterio cadranno automaticamente sotto la giurisdizione del criterio per sito appropriato. In assenza di un criterio per sito quegli utenti verranno regolati dal criterio globale. Se si rimuove un criterio per sito, gli utenti ai quali era stato assegnato quel criterio cadranno automaticamente sotto la giurisdizione del criterio globale.

Si noti che è possibile eseguire il cmdlet **Remove-CsArchivingPolicy** anche per un criterio globale, ma che non è possibile rimuovere il criterio globale. Se si esegue il cmdlet **Remove-CsArchivingPolicy** per il criterio globale, tutte le proprietà di quel criterio verranno invece reimpostate sui rispettivi valori predefiniti e di conseguenza non verrà archiviata alcuna sessione di messaggistica istantanea, interna o esterna. Questo perché il valore predefinito di entrambe le proprietà (ArchiveInternal e ArchiveExternal) è False.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsArchivingPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsArchivingPolicy"}

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
<td><p>Identificatore univoco del criterio di archiviazione da rimuovere. È possibile configurare i criteri di archiviazione nell'ambito globale, del sito o di un singolo utente. Per rimuovere il criterio globale, utilizzare la seguente sintassi: -Identity global. Si noti che non è possibile eliminare un criterio globale. Ciò che accade è che per tutte le proprietà dei criteri verranno ripristinati i valori predefiniti.</p>
<p>Per eliminare criteri del sito, usare una sintassi simile alla seguente: -Identity site:Redmond. Per eliminare criteri per utente, usare una sintassi simile alla seguente: -Identity SalesArchivingPolicy.</p>
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
<td><p>Se questo parametro è presente, il criterio verrà rimosso automaticamente anche se attualmente è assegnato ad almeno un utente. Se questo parametro non è presente, il cmdlet <strong>Remove-CsArchivingPolicy</strong> non rimuoverà automaticamente un criterio per utente che è assegnato ad almeno un utente. Verrà invece visualizzato un messaggio che richiede di confermare la rimozione del criterio. Per procedere con l'operazione e rimuovere il criterio, è necessario rispondere affermativamente (premendo il tasto Y).</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.IM.IMArchivingPolicy. Il cmdlet **Remove-CsArchivingPolicy** accetta l'input da pipeline di oggetti criterio di archiviazione.

## Tipi restituiti

Il cmdlet **Remove-CsArchivingPolicy** non restituisce oggetti o valori. Il cmdlet invece rimuove le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.IM.IMArchivingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)

