---
title: Set-CsArchivingPolicy
TOCTitle: Set-CsArchivingPolicy
ms:assetid: 2213f1e7-ebdb-4a70-83d9-41eee6d0e14f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398294(v=OCS.15)
ms:contentKeyID: 49299915
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsArchivingPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio di archiviazione di messaggistica istantanea esistente. Un criterio di archiviazione consente di archiviare tutte le sessioni di messaggistica istantanea e le conferenze eseguite tra gli utenti interni. È inoltre possibile archiviare le sessioni eseguite tra utenti interni e partner federati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsArchivingPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsArchivingPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ArchiveExternal <$true | $false>] [-ArchiveInternal <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene utilizzato il cmdlet **Set-CsArchivingPolicy** per modificare il criterio di archiviazione globale. In questo caso, la proprietà ArchiveInternal è impostata su True.

    Set-CsArchivingPolicy -Identity global -ArchiveInternal $True

## ESEMPIO 2

L'esempio 2 è una variante del comando riportato nell'esempio 1. Questa volta, però, tutti i criteri di archiviazione dell'organizzazione sono configurati per consentire l'archiviazione delle sessioni di messaggistica istantanea. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsArchivingPolicy** per restituire una raccolta di tutti i criteri di archiviazione delle sessioni di messaggistica istantanea attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsArchivingPolicy**, che imposta la proprietà ArchiveInternal di ogni criterio su True.

    Get-CsArchivingPolicy | Set-CsArchivingPolicy -ArchiveInternal $True

## Descrizione dettagliata

Molte organizzazioni ritengono utile conservare un archivio di tutte le sessioni di messaggistica istantanea a cui prendono parte gli utenti. Altre organizzazioni sono obbligate a mantenere tale archivio per legge. Per archiviare sessioni di messaggistica istantanea con Lync Server, è necessario eseguire due passaggi. È necessario innanzitutto abilitare l'archiviazione nell'ambito globale e/o del sito utilizzando il cmdlet **Set-CsArchivingConfiguration**. Questo consente di archiviare sessioni di messaggistica istantanea. L'archiviazione di tali sessioni tuttavia non viene avviata automaticamente.

Per salvare le trascrizioni delle sessioni di messaggistica istantanea, è necessario completare il secondo passaggio: creare uno o più criteri di archiviazione che determinano per quali utenti vengono registrate le sessioni di messaggistica istantanea e quali tipi di sessioni di messaggistica istantanea (interne e/o esterne) vengono archiviati. Le sessioni di messaggistica istantanea interne sono sessioni in cui tutti i partecipanti sono utenti autenticati che dispongono di account Active Directory all'interno dell'organizzazione. Le sessioni di messaggistica istantanea esterne sono sessioni in cui almeno un partecipante è un utente non autenticato che non dispone di un account Active Directory all'interno dell'organizzazione. È possibile scegliere di archiviare solo le sessioni interne, solo le sessioni esterne oppure entrambi i tipi.

I criteri di archiviazione (creati con il cmdlet **New-CsArchivingPolicy**) possono essere assegnati al sito globale o nell'ambito del sito. Inoltre, questi criteri possono essere assegnati nell'ambito per utente: in pratica, è possibile creare un criterio e applicarlo a un utente o a un gruppo di utenti specifico. Ad esempio, si potrebbe disporre di un criterio globale che consente di archiviare sessioni di messaggistica istantanea interne per tutti gli utenti. A questo si potrebbe aggiungere un secondo criterio che archivia sia le sessioni interne sia le sessioni esterne, applicandolo solo al personale addetto alle vendite. Poiché i criteri per utente hanno la precedenza sui criteri globali e di sito, verranno archiviate tutte le sessioni di messaggistica istantanea dei membri dello staff vendite. Per tutti gli altri utenti (che non appartengono al reparto delle vendite e che non sono soggetti ai criteri delle vendite) verranno archiviate solamente le sessioni di messaggistica istantanea interne.

Il cmdlet **Set-CsArchivingPolicy** consente di modificare i valori delle proprietà per qualsiasi criterio di archiviazione delle sessioni di messaggistica istantanea attualmente in uso nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsArchivingPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsArchivingPolicy"}

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
<td><p><em>ArchiveExternal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se vengono archiviate le sessioni di messaggistica istantanea esterne. Una sessione di messaggistica istantanea esterna è una sessione in cui almeno un partecipante è un utente non autenticato che non dispone di un account Active Directory all'interno dell'organizzazione. Il valore predefinito è False, ovvero le sessioni di messaggistica istantanea che includono utenti esterni non vengono archiviate.</p></td>
</tr>
<tr class="even">
<td><p><em>ArchiveInternal</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se vengono archiviate le sessioni di messaggistica istantanea interne. Una sessione di messaggistica istantanea interna è una sessione in cui tutti i partecipanti sono utenti autenticati che dispongono di account Active Directory all'interno dell'organizzazione. Il valore predefinito è False, ovvero le sessioni di messaggistica istantanea interne non vengono archiviate.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un testo aggiuntivo riguardante il criterio. Ad esempio, è possibile utilizzare la proprietà Description per specificare gli utenti a cui dovrebbe essere applicato il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il criterio di archiviazione da modificare. I criteri di archiviazione possono essere configurati negli ambiti globale, di sito o per utente. Per modificare il criterio globale, utilizzare la sintassi seguente: -Identity global. Per modificare un criterio di sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per modificare un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity SalesArchivingPolicy. Se questo parametro non viene specificato, verrà modificato il criterio globale.</p>
<p>I caratteri jolly non sono consentiti quando si specifica una identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto IMArchivingPolicy</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Il cmdlet **Set-CsArchivingPolicy** non restituisce oggetti o valori. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Policy.IM.IMArchivingPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingPolicy](get-csarchivingpolicy.md)  
[Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)  
[New-CsArchivingPolicy](new-csarchivingpolicy.md)  
[Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)

