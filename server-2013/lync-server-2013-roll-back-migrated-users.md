---
title: 'Lync Server 2013: Eseguire il rollback degli utenti migrati'
TOCTitle: Eseguire il rollback degli utenti migrati
ms:assetid: bfabaf0b-9a42-4057-b729-a7ab9eee8c72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205224(v=OCS.15)
ms:contentKeyID: 49301850
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire il rollback degli utenti migrati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-07_

Se è necessario eseguire il rollback della funzionalità relativa all'archivio contatti unificato, eseguire il rollback dei contatti solo se l'utente deve essere ritrasferito in Exchange 2010 o Lync Server 2010. Per eseguire il rollback, disabilitare il criterio per l'utente e quindi eseguire il cmdlet **Invoke-CsUcsRollback**. La sola esecuzione di **Invoke-CsUcsRollback** non è sufficiente ad assicurare un rollback permanente, in quanto la migrazione dell'archivio contatti unificato verrà avviata di nuovo se il criterio non viene disabilitato. Ad esempio, se viene eseguito il rollback di un utente perché da Exchange 2013 si torna a Exchange 2010 e quindi la cassetta postale dell'utente viene spostata in Exchange 2013, la migrazione dell'archivio contatti unificato verrà riavviata sette giorni dopo il rollback finché tale archivio resta abilitato per l'utente nel criterio dei servizi utente.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il cmdlet <strong>Move-CsUser</strong> esegue automaticamente il rollback dell'archivio contatti dell'utente da Exchange 2013 a Lync Server 2013 nelle situazioni seguenti:
<ul>
<li><p>Quando gli utenti vengono spostati da Lync Server 2013 a Lync Server 2010.</p></li>
<li><p>Quando viene eseguita la migrazione degli utenti tra locali, ad esempio quando un utente viene spostato da Skype for Business online a Lync Server 2013 in locale o viceversa.</p></li>
</ul></td>
</tr>
</tbody>
</table>


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>L'importazione dei dati dell'archivio contatti unificato da un database di backup può danneggiare i dati dell'archivio e degli utenti se la modalità dell'archivio stesso è cambiata tra l'esportazione e l'importazione. Ad esempio:
<ul>
<li><p>Se si esportano gli elenchi contatti prima che venga eseguita la migrazione in Exchange 2013 dei contatti degli utenti e quindi, dopo la migrazione, si importano gli stessi dati, i dati dell'archivio contatti unificato e gli elenchi contatti si danneggeranno.</p></li>
<li><p>Se si esportano i dati degli utenti dopo aver eseguito la migrazione degli utenti in Exchange 2013, si esegue il rollback della migrazione e quindi per qualche motivo si importano i dati da dopo la migrazione, i dati dell'archivio contatti unificato e gli elenchi contatti si danneggeranno.</p></li>
</ul></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prima che sia possibile spostare una cassetta postale di Exchange da Exchange 2013 a Exchange 2010, l'amministratore di Exchange deve verificare che l'amministratore di Lync Server abbia prima eseguito il rollback dei contatti degli utenti di Lync Server da Exchange 2013 a Lync Server. Per riportare i contatti dell'archivio contatti unificato a Lync Server, vedere la procedura &quot;Per eseguire il rollback dei contatti dell'archivio contatti unificato da Exchange 2013 a Lync Server 2013&quot; più avanti in questa sezione.</td>
</tr>
</tbody>
</table>


Nella procedura seguente viene illustrato come eseguire il rollback dei contatti degli utenti. Se si utilizza il cmdlet **Move-CsUser** per spostare gli utenti tra Lync Server 2013 e Lync Server 2010, è possibile ignorare questi passaggi perché il cmdlet **Move-CsUser** esegue automaticamente il rollback dell'archivio contatti unificato quando sposta gli utenti da Lync Server 2013 a Lync Server 2010. **Move-CsUser** non disabilita il criterio dell'archivio contatti unificato, pertanto la migrazione nell'archivio verrà ripetuta se l'utente viene ritrasferito in Lync Server 2013.

## Per eseguire il rollback dei contatti degli utenti da Lync Server 2013 a Lync Server 2010

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Disabilitare l'archivio contatti unificato per gli utenti di cui è necessario eseguire il rollback in modo che, dopo il rollback, non ne venga ripetuta la migrazione. Eseguire questo passaggio solo se si desidera essere certi che gli utenti non vengano ritrasferiti in futuro. Per disabilitare l'archivio contatti unificato per i singoli utenti, nella riga di comando digitare quanto segue:
    
        Set-CsUserServicesPolicy -Identity "<policy name>" -UcsAllowed $False
    
    Ad esempio:
    
        Set-CsUserServicesPolicy -Identity "UCS Enabled Users" -UcsAllowed $False

3.  Prima di spostare un utente da Lync Server 2013 a Lync Server 2010, eseguire il rollback dell'elenco contatti per gli utenti specificati in Lync Server.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si ignora questo passaggio, l'elenco contatti andrà perso.</td>
    </tr>
    </tbody>
    </table>


4.  Eseguire il rollback degli utenti specificati. Nella riga di comando digitare quanto segue:
    
        Invoke-CsUcsRollback -Identity "<user display name>"
    
    Ad esempio:
    
        Invoke-CsUcsRollback -Identity "Ken Myer"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Non è consigliabile utilizzare l'opzione –Force per forzare il rollback. Se si utilizza tale opzione, i contatti degli utenti andranno persi.</td>
    </tr>
    </tbody>
    </table>


## Per eseguire il rollback dei contatti dell'archivio contatti unificato da Exchange 2013 a Lync Server 2013

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Disabilitare l'archivio contatti unificato per gli utenti di cui è necessario eseguire il rollback in modo che, dopo il rollback, non ne venga ripetuta la migrazione. Per disabilitare l'archivio contatti unificato per i singoli utenti, nella riga di comando digitare quanto segue:
    
        Set-CsUserServicesPolicy -Identity "<policy name>" -UcsAllowed $False
    
    Ad esempio:
    
        Set-CsUserServicesPolicy -Identity "UCS Enabled Users" -UcsAllowed $False

3.  Eseguire il rollback degli utenti specificati. Nella riga di comando digitare quanto segue:
    
        Invoke-CsUcsRollback -Identity "<user display name>"
    
    Ad esempio:
    
        Invoke-CsUcsRollback -Identity "Ken Myer"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>È necessario innanzitutto eseguire il rollback dell'utente di Lync Server e quindi spostare la cassetta postale di Exchange 2013. L'amministratore di Exchange non potrà eseguire il rollback di Exchange fino al completamento del rollback di Lync Server. Non è consigliabile utilizzare l'opzione –Force per forzare il rollback. Se si utilizza tale opzione, i contatti degli utenti andranno persi.</td>
    </tr>
    </tbody>
    </table>


4.  Dopo che l'utente è stato riportato a Lync Server, l'amministratore di Exchange può eseguire il rollback dell'utente di Exchange da Exchange 2013 a Exchange 2010.

