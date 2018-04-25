---
title: 'Lync Server 2013: Pianificazione del controllo di accesso basato sui ruoli'
TOCTitle: Pianificazione del controllo di accesso basato sui ruoli
ms:assetid: 41204ba3-ce5b-41a8-a6c3-b444468fa328
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425917(v=OCS.15)
ms:contentKeyID: 49300322
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per consentire la delega delle attività amministrative continuando a mantenere standard elevati di sicurezza, Lync Server 2013 offre il controllo di accesso basato sui ruoli (RBAC). Grazie a questa funzionalità, il privilegio amministrativo viene concesso assegnando gli utenti a ruoli amministrativi. Lync Server 2013 include una vasta gamma di ruoli amministrativi predefiniti e consente di creare nuovi ruoli e di specificare un elenco personalizzato di cmdlet per ognuno di essi. Rende inoltre possibile l'aggiunta di script di cmdlet alle attività consentite sia dei ruoli RBAC predefiniti che di quelli personalizzati.

## Migliore sicurezza dei server e centralizzazione

Grazie al controllo di accesso basato sui ruoli, l'accesso e l'autorizzazione sono più strettamente associati al ruolo Lync Server dell'utente. In questo modo si dispone di un più ampio margine per applicare il metodo di sicurezza basato sul principio dei privilegi minimi, che concede agli amministratori e agli utenti solo i diritti necessari per le attività che devono svolgere.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le restrizioni del controllo di accesso basato sui ruoli si applicano solo per gli amministratori che lavorano da postazione remota, utilizzando il Pannello di controllo di Lync Server o Lync Server Management Shell. Un utente che lavora da un server che esegue Lync Server non è soggetto alle restrizioni del controllo di accesso basato sui ruoli. La sicurezza fisica di Lync Server pertanto è importante per mantenere le restrizioni del controllo di accesso basato sui ruoli.</td>
</tr>
</tbody>
</table>


## Ruoli e ambito

Nel controllo di accesso basato sui ruoli un *ruolo* è abilitato all'uso di un elenco di cmdlet, progettati in modo da essere utilizzati da un determinato tipo di amministratore o tecnico. Un *ambito* è un insieme di oggetti sui cui possono operare i cmdlet definiti in un ruolo. Gli oggetti su cui ha effetto l'ambito possono essere account utente (raggruppati per unità organizzativa) o server (raggruppati per sito).

Nella tabella riportata di seguito sono elencati i ruoli predefiniti in Lync Server e viene fornita una panoramica generale dei tipi di attività che consentono di eseguire. Nella quarta colonna viene indicato l'eventuale ruolo di Microsoft Exchange Server simile per ogni ruolo di Lync Server.

### Ruoli amministrativi predefiniti

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo</th>
<th>Attività consentite</th>
<th>Gruppo Active Directory sottostante</th>
<th>Equivalente di Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CsAdministrator</p></td>
<td><p>Può eseguire tutte le attività amministrative e modificare tutte le impostazioni, tra cui la creazione di ruoli e l'assegnazione di utenti ai ruoli. Può espandere una distribuzione aggiungendo nuovi siti, pool e servizi.</p></td>
<td><p>CSAdministrator</p></td>
<td><p>Gestione dell'organizzazione</p></td>
</tr>
<tr class="even">
<td><p>CsUserAdministrator</p></td>
<td><p>Può abilitare e disabilitare gli utenti per Lync Server, spostare utenti e assegnare criteri esistenti agli utenti. Non può modificare i criteri.</p></td>
<td><p>CSUserAdministrator</p></td>
<td><p>Mail Recipients</p></td>
</tr>
<tr class="odd">
<td><p>CsVoiceAdministrator</p></td>
<td><p>Può creare, configurare e gestire le impostazioni e i criteri vocali.</p></td>
<td><p>CSVoiceAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>CsServerAdministrator</p></td>
<td><p>Può gestire e monitorare server e servizi, nonché risolvere i relativi errori. Può impedire nuove connessioni ai server, arrestare e avviare servizi e applicare aggiornamenti software. Non può apportare modifiche con impatto sulla configurazione globale.</p></td>
<td><p>CSServerAdministrator</p></td>
<td><p>Server Management</p></td>
</tr>
<tr class="odd">
<td><p>CsViewOnlyAdministrator</p></td>
<td><p>Può visualizzare la distribuzione, incluse le informazioni su utenti e server, in modo da monitorare l'integrità della distribuzione.</p></td>
<td><p>CSViewOnlyAdministrator</p></td>
<td><p>Gestione organizzazione in sola visualizzazione</p></td>
</tr>
<tr class="even">
<td><p>CsHelpDesk</p></td>
<td><p>Può visualizzare la distribuzione, tra cui le proprietà e i criteri utente, e può eseguire specifiche attività di risoluzione dei problemi. Non può modificare le proprietà o i criteri utente, la configurazione dei server o i servizi.</p></td>
<td><p>CSHelpDesk</p></td>
<td><p>HelpDesk</p></td>
</tr>
<tr class="odd">
<td><p>CsArchivingAdministrator</p></td>
<td><p>Può modificare la configurazione e i criteri di archiviazione.</p></td>
<td><p>CSArchivingAdministrator</p></td>
<td><p>Gestione conservazione, Conservazione legale</p></td>
</tr>
<tr class="even">
<td><p>CsResponseGroupAdministrator</p></td>
<td><p>Può gestire la configurazione dell'applicazione Response Group in un sito.</p></td>
<td><p>CSResponseGroupAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>CsLocationAdministrator</p></td>
<td><p>Livello minimo di diritti per la gestione di Enhanced 9-1-1 (E9-1-1), incluse la creazione di posizioni E9-1-1 e di identificatori di rete e l'associazione tra questi elementi. Questo ruolo viene sempre assegnato con un ambito globale.</p></td>
<td><p>CSLocationAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>CsResponseGroupManager</p></td>
<td><p>Può gestire Response Group specifici.</p></td>
<td><p>CSResponseGroupManager</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>CsPersistentChatAdministrator</p></td>
<td><p>Può gestire la funzionalità Chat persistente e specifiche chat room di Chat persistente.</p></td>
<td><p>CSPersistentChatAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>CsAdministrator</p></td>
<td><p>Può eseguire tutte le attività amministrative e modificare tutte le impostazioni, tra cui la creazione di ruoli e l'assegnazione di utenti ai ruoli. Può espandere una distribuzione aggiungendo nuovi siti, pool e servizi.</p></td>
<td><p>CSAdministrator</p></td>
<td><p>Gestione dell'organizzazione</p></td>
</tr>
<tr class="odd">
<td><p>CsUserAdministrator</p></td>
<td><p>Può abilitare e disabilitare gli utenti per Lync Server, spostare utenti e assegnare criteri esistenti agli utenti. Non può modificare i criteri.</p></td>
<td><p>CSUserAdministrator</p></td>
<td><p>Mail Recipients</p></td>
</tr>
<tr class="even">
<td><p>CsVoiceAdministrator</p></td>
<td><p>Può creare, configurare e gestire le impostazioni e i criteri vocali.</p></td>
<td><p>CSVoiceAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>CsServerAdministrator</p></td>
<td><p>Può gestire e monitorare server e servizi, nonché risolvere i relativi errori. Può impedire nuove connessioni ai server, arrestare e avviare servizi e applicare aggiornamenti software. Non può apportare modifiche con impatto sulla configurazione globale.</p></td>
<td><p>CSServerAdministrator</p></td>
<td><p>Server Management</p></td>
</tr>
<tr class="even">
<td><p>CsViewOnlyAdministrator</p></td>
<td><p>Può visualizzare la distribuzione, incluse le informazioni su utenti e server, in modo da monitorare l'integrità della distribuzione.</p></td>
<td><p>CSViewOnlyAdministrator</p></td>
<td><p>Gestione organizzazione in sola visualizzazione</p></td>
</tr>
<tr class="odd">
<td><p>CsHelpDesk</p></td>
<td><p>Può visualizzare la distribuzione, tra cui le proprietà e i criteri utente, e può eseguire specifiche attività di risoluzione dei problemi. Non può modificare le proprietà o i criteri utente, la configurazione dei server o i servizi.</p></td>
<td><p>CSHelpDesk</p></td>
<td><p>HelpDesk</p></td>
</tr>
<tr class="even">
<td><p>CsArchivingAdministrator</p></td>
<td><p>Può modificare la configurazione e i criteri di archiviazione.</p></td>
<td><p>CSArchivingAdministrator</p></td>
<td><p>Gestione conservazione, Conservazione legale</p></td>
</tr>
<tr class="odd">
<td><p>CsResponseGroupAdministrator</p></td>
<td><p>Può gestire la configurazione dell'applicazione Response Group in un sito.</p></td>
<td><p>CSResponseGroupAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>CsLocationAdministrator</p></td>
<td><p>Livello minimo di diritti per la gestione di Enhanced 9-1-1 (E9-1-1), incluse la creazione di posizioni E9-1-1 e di identificatori di rete e l'associazione tra questi elementi. Questo ruolo viene sempre assegnato con un ambito globale.</p></td>
<td><p>CSLocationAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>CsResponseGroupManager</p></td>
<td><p>Può gestire Response Group specifici.</p></td>
<td><p>CSResponseGroupManager</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>CsPersistentChatAdministrator</p></td>
<td><p>Può gestire la funzionalità Chat persistente e specifiche chat room di Chat persistente.</p></td>
<td><p>CSPersistentChatAdministrator</p></td>
<td><p>Non applicabile</p></td>
</tr>
</tbody>
</table>


Tutti i ruoli predefiniti forniti in Lync Server hanno un ambito globale. Per applicare il principio dei privilegi minimi, è consigliabile non assegnare utenti a ruoli con ambito globale se amministreranno solo un insieme limitato di server o utenti. A tale scopo, è possibile creare ruoli basati su ruoli esistenti, ma con un ambito molto più limitato.

## Creazione di un ruolo con ambito

Quando si crea un ruolo con ambito limitato, ovvero un ruolo con ambito, si specifica l'ambito insieme al ruolo esistente sui cui si basa e al gruppo Active Directory a cui assegnare il ruolo. Il gruppo Active Directory specificato deve essere già creato. Il cmdlet seguente è un esempio di creazione di un ruolo che dispone dei privilegi di uno dei ruoli amministrativi, ma con ambito limitato. Crea un nuovo ruolo denominato `Site01 Server Administrators`. Il nuovo ruolo ha le capacità del ruolo CsServerAdministrator predefinito, ma solo per i server del sito Site01. Per il funzionamento di questo cmdlet, deve essere già stato definito il sito Site01 e deve esistere già un gruppo di sicurezza universale denominato `Site01 Server Administrators`.

    New-CsAdminRole -Identity "Site01 Server Administrators" -Template CsServerAdministrator -ConfigScopes "site:Site01"

Dopo l'esecuzione di questo cmdlet, tutti gli utenti membri del gruppo `Site01 Server Administrators` disporranno di privilegi di amministratore server per i server del sito Site01. Anche tutti gli utenti che verranno aggiunti a questo gruppo di sicurezza successivamente acquisiranno i privilegi di questo ruolo. Si noti che sia il ruolo stesso che il gruppo di sicurezza universale a cui è assegnato sono denominati `Site01 Server Administrators`.

Nell'esempio seguente si applicano limiti all'ambito utente anziché all'ambito server. Viene creato un ruolo `Sales Users Administrator` per l'amministrazione degli account utente nell'unità organizzativa Sales. Per il funzionamento di questo cmdlet, deve essere stato già creato il gruppo di sicurezza universale SalesUsersAdministrator.

    New-CsAdminRole -Identity "Sales Users Administrator " -Template CsUserAdministrator -UserScopes "OU:OU=Sales, OU=Lync Tenants, DC=Domain, DC=com"

## Creazione di un nuovo ruolo

Per creare un ruolo che disponga di accesso a un insieme di cmdlet non inclusi in uno dei ruoli predefiniti oppure a un insieme di script o moduli, usare di nuovo uno dei ruoli predefiniti come modello. Si noti che gli script e i moduli che i ruoli sono in grado di eseguire devono essere memorizzati nei percorsi seguenti:

  - Il percorso del modulo Lync che, per impostazione predefinita, è C:\\Programmi\\File comuni\\Microsoft Lync Server 2013\\Modules\\Lync

  - Il percorso degli script dell'utente che, per impostazione predefinita, è C:\\Programmi\\File comuni\\Microsoft Lync Server 2013\\AdminScripts

Per creare un nuovo ruolo, utilizzare il cmdlet **New-CsAdminRole**. Prima di eseguire **New-CsAdminRole** , è necessario creare il gruppo di sicurezza universale sottostante che verrà a esso associato.

I cmdlet seguenti possono essere usati come esempio di creazione di un nuovo ruolo. Essi creano un nuovo tipo di ruolo denominato `MyHelpDeskScriptRole`. Il nuovo ruolo ha le capacità del ruolo CsHelpDesk predefinito e può anche eseguire le funzioni in uno script denominato "testscript".

    New-CsAdminRole -Identity "MyHelpDeskScriptRole" -Template CsHelpDesk -ScriptModules @{Add="testScript.ps1"}

Perché questo cmdlet funzioni, è necessario prima creare il gruppo di sicurezza universale MyHelpDeskScriptRole.

Dopo aver eseguito il cmdlet, è possibile assegnare gli utenti direttamente a questo ruolo (in tal caso avranno ambito globale) o creare un ruolo con ambito basato su questo ruolo, come spiegato nella sezione precedente del presente documento, intitolata Creazione di un ruolo con ambito.

## Assegnazione di ruoli agli utenti

Ogni ruolo Lync Server è associato a un gruppo di sicurezza universale Active Directory sottostante. Tutti gli utenti che vengono aggiunti al gruppo sottostante acquisiscono le capacità di tale ruolo.

Negli esempi delle sezioni precedenti è stato creato un nuovo ruolo, cui è stato assegnato un gruppo di sicurezza universale esistente. Per assegnare un ruolo esistente a uno o più utenti, aggiungere gli utenti desiderati al gruppo associato al ruolo. A tali gruppi è possibile aggiungere singoli utenti e gruppi di sicurezza universale.

Il ruolo **CsAdministrator** viene ad esempio automaticamente concesso al gruppo di sicurezza universale **CS Administrators** in Active Directory. Questo gruppo di sicurezza universale viene creato in Active Directory quando si distribuisce Lync Server. Per concedere questo privilegio a un utente o a un gruppo, è sufficiente aggiungerlo al gruppo **CS Administrators** .

È possibile assegnare a un utente più ruoli di controllo di accesso basato sui ruoli aggiungendo l'utente ai gruppi Active Directory sottostanti che corrispondono a ogni ruolo.

Si noti che quando si crea un ruolo, gli utenti che vengono aggiunti successivamente al gruppo Active Directory sottostante acquisiscono le capacità di tale ruolo.

## Modifica delle capacità di un ruolo

È possibile modificare l'elenco di cmdlet e script che un ruolo può eseguire, nonché modificare sia i cmdlet che gli script che i ruoli personalizzati possono eseguire, ma solo gli script dei ruoli predefiniti. Ogni cmdlet digitato può aggiungere, rimuovere o sostituire cmdlet o script.

Per modificare un ruolo, usare il cmdlet **Set-CsAdminRole** . Il cmdlet seguente rimuove uno script dal ruolo.

    Set-CsAdminRole -Identity "MyHelpDeskScriptRole" -ScriptModules @{Remove="testScript.ps1"}

## Pianificazione del controllo di accesso basato sui ruoli

Per ogni utente a cui devono essere concessi diritti amministrativi per la distribuzione di Lync Server, valutare esattamente le attività che deve eseguire e quindi assegnarlo a ruoli con il privilegio e l'ambito minimi necessari per svolgere le attività di competenza. Se necessario, è possibile utilizzare il cmdlet **Set-CsAdminRole** per creare un nuovo ruolo con i soli cmdlet richiesti per le attività di questo utente.

Gli utenti con ruolo CsAdministrator possono creare tutti i tipi di ruoli, inclusi quelli basati su CsAdministrator, e assegnare utenti a tali ruoli. La procedura consigliata prevede l'assegnazione del ruolo CsAdministrator a un insieme limitato di utenti trusted.

