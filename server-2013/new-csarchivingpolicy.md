---
title: New-CsArchivingPolicy
TOCTitle: New-CsArchivingPolicy
ms:assetid: e7c9b310-fbd0-4793-90ef-c752b941e02f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399032(v=OCS.15)
ms:contentKeyID: 49302302
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsArchivingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea nuovi criteri di archiviazione per sessioni di messaggistica istantanea. Tali criteri consentono di archiviare tutte le sessioni di messaggistica istantanea eseguite tra utenti interni e/o di archiviare tutte le sessioni di messaggistica istantanea eseguite tra utenti interni e partner esterni. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsArchivingPolicy -Identity <XdsIdentity> [-ArchiveExternal <$true | $false>] [-ArchiveInternal <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **New-CsArchivingPolicy** viene utilizzato per creare nuovi criteri di archiviazione con Identity site:Redmond. Il parametro ArchiveInternal viene inoltre impostato su True e ciò significa che i nuovi criteri consentiranno l'archiviazione delle sessioni di messaggistica istantanea interne e delle conferenze.

    New-CsArchivingPolicy -Identity site:Redmond -ArchiveInternal $True

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il parametro InMemory per creare un criterio di archiviazione che inizialmente esista soltanto in memoria. In questo set di comandi viene innanzitutto chiamato il cmdlet **New-CsArchivingPolicy**, insieme al parametro InMemory, per creare nuovi criteri di sito con Identity site:Redmond. I nuovi criteri presenti soltanto in memoria vengono archiviati nella variabile $x. Nei comandi 2 e 3 vengono modificati i valori delle proprietà per tali criteri virtuali. Nel comando 2 il valore della proprietà ArchiveInternal viene impostato su True, mentre nel comando 3 la proprietà ArchiveExternal viene impostata su True.

Infine, l'ultimo comando dell'esempio utilizza il cmdlet **Set-CsArchivingPolicy** per trasformare i criteri virtuali site:Redmond in criteri effettivi per l'archiviazione delle sessioni di messaggistica istantanea.

    $x = New-CsArchivingPolicy -Identity site:Redmond -InMemory
    $x.ArchiveInternal = $True
    $x.ArchiveExternal = $True
    Set-CsArchivingPolicy -Instance $x

## Descrizione dettagliata

Per molte organizzazioni è utile conservare un archivio di tutte le sessioni di messaggistica istantanea cui prendono parte i propri utenti; altre organizzazioni sono obbligate per legge a detenere un archivio del genere. Per archiviare sessioni di messaggistica istantanea con Lync Server, è necessario eseguire due passaggi. Innanzitutto è necessario abilitare l'archiviazione nell'ambito globale e/o del sito utilizzando il cmdlet **Set-CsArchivingConfiguration**. Questo consente di poter archiviare sessioni di messaggistica istantanea. Tuttavia, l'archiviazione di tali sessioni non viene avviata automaticamente.

Per salvare effettivamente le trascrizioni di sessioni di messaggistica istantanea è infatti necessario completare il passaggio 2: creare uno o più criteri di archiviazione delle sessioni di messaggistica istantanea per determinare gli utenti di cui verranno registrate le sessioni nonché quale tipo di sessioni di messaggistica istantanea (interne e/o esterne) verranno archiviate. Le sessioni di messaggistica istantanea interne sono sessioni in cui tutti i partecipanti sono utenti autenticati che dispongono di account Active Directory all'interno dell'organizzazione; le sessioni di messaggistica istantanea esterne sono sessioni in cui almeno un partecipante è un utente non autenticato che non dispone di un account Active Directory all'interno dell'organizzazione. È possibile scegliere di archiviare soltanto sessioni interne, soltanto sessioni esterne oppure entrambi i tipi.

I criteri di archiviazione possono essere assegnati all'ambito globale o all'ambito del sito. Tali criteri possono inoltre essere assegnati all'ambito per utente e quindi essere applicati a un utente o a un insieme di utenti specifico. Si supponga ad esempio che il criterio globale in uso consenta di archiviare solo le sessioni di messaggistica istantanea interne per tutti gli utenti. In questo caso, si potrebbe creare un secondo criterio che archivia sia le sessioni interne sia le sessioni esterne, applicandolo solo al personale addetto alle vendite. Poiché i criteri per utente hanno la precedenza sui criteri globali e di sito, verranno archiviate tutte le sessioni di messaggistica istantanea dei membri dello staff vendite. Per tutti gli altri utenti, ovvero gli utenti che non appartengono al reparto vendite e che non sono soggetti al criterio relativo alle vendite, verranno archiviate solamente le sessioni di messaggistica istantanea interne.

È possibile creare nuovi criteri di archiviazione (nell'ambito del sito o per utente) utilizzando il cmdlet **New-CsArchivingPolicy**. Se viene creato un criterio nell'ambito del sito, questo verrà applicato automaticamente al sito nel momento stesso in cui il criterio viene creato. Se viene creato un criterio per utente, tale criterio non verrà utilizzato finché non verrà esplicitamente assegnato a un utente o un insieme di utenti richiamando il cmdlet **Grant-CsArchivingPolicy**. Non è possibile creare un nuovo criterio nell'ambito globale.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsArchivingPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsArchivingPolicy"}

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
<td><p>Indica l'identità univoca da assegnare al criterio. È possibile creare nuovi criteri di archiviazione nell'ambito del sito o nell'ambito per utente. Per creare un nuovo criterio di sito, utilizzare il prefisso &quot;site:&quot; seguito dal nome del sito. Ad esempio, questa sintassi consente di creare un nuovo criterio per il sito Redmond: -Identity site:Redmond. Per creare un nuovo criterio per utente utilizzare un'identità simile alla seguente: -Identity SalesArchivingPolicy.</p>
<p>Non è possibile creare un nuovo criterio globale; se si desidera apportare modifiche al criterio globale, utilizzare il cmdlet <strong>Set-CsArchivingPolicy</strong>. Analogamente, non è possibile creare un nuovo criterio di sito o per utente se è già presente un criterio con tale identità.</p></td>
</tr>
<tr class="even">
<td><p><em>ArchiveExternal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se vengono archiviate le sessioni di messaggistica istantanea esterne. Una sessione di messaggistica istantanea esterna è una sessione in cui almeno un partecipante è un utente non autenticato che non dispone di un account Active Directory all'interno dell'organizzazione. Il valore predefinito è False, ovvero le sessioni di messaggistica istantanea che includono utenti esterni non vengono archiviate.</p></td>
</tr>
<tr class="odd">
<td><p><em>ArchiveInternal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se vengono archiviate le sessioni di messaggistica istantanea interne. Una sessione di messaggistica istantanea interna è una sessione in cui tutti i partecipanti sono utenti autenticati che dispongono di account Active Directory all'interno dell'organizzazione. Il valore predefinito è False, ovvero le sessioni di messaggistica istantanea interne non vengono archiviate.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire una breve descrizione del criterio di archiviazione. Ad esempio, la descrizione potrebbe essere usata per indicare a quali utenti deve essere applicato il criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. Il cmdlet **New-CsArchivingPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsArchivingPolicy** crea istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.IM.IMArchivingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)  
[Set-CsArchivingPolicy](set-csarchivingpolicy.md)

