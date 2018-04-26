---
title: New-CsAdminRole
TOCTitle: New-CsAdminRole
ms:assetid: 1e46c02e-0937-4e3b-b02e-e7507189f6aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398271(v=OCS.15)
ms:contentKeyID: 49299872
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAdminRole

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo ruolo RBAC (Role-Based Access Control, controllo di accesso basato sui ruoli). I ruoli RBAC vengono utilizzati per definire le attività di gestione che gli utenti sono autorizzati a svolgere e l'ambito in cui sono autorizzati a operare. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsAdminRole -Identity <String> -Template <String> [-Cmdlets <PSListModifier>] [-ConfigScopes <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-ScriptModules <PSListModifier>] [-UserScopes <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di duplicare il ruolo RBAC CsVoiceAdministrator. Poiché non sono stati specificati parametri aggiuntivi, il nuovo ruolo (RedmondVoiceAdministrators) sarà un duplicato perfetto di CsVoiceAdministrator in cui entrambe le proprietà UserScopes e ConfigScopes sono impostate su "global".

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator"

## ESEMPIO 2

Nell'esempio 2 viene creato un nuovo ruolo RBAC (RedmondVoiceAdministrator) che viene configurato per l'ambito di un utente singolo: l'unità organizzativa (OU) Redmond. Per ottenere questo risultato, viene incluso il parametro UserScopes con il valore seguente: "OU:ou=Redmond,dc=litwareinc,dc=com". Questo valore sostituisce il valore corrente della proprietà UserScopes con un elemento: l'unità organizzativa (OU) con nome distinto "ou=Redmond,dc=litwareinc,dc=com".

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator" -UserScopes "OU:ou=Redmond,dc=litwareinc,dc=com"

## ESEMPIO 3

Il comando riportato nell'Esempio 3 è una variante del comando riportato nell'Esempio, con la sola differenza che, in questo esempio, alla proprietà UserScopes vengono aggiunte 2 unità organizzative. Per ottenere questo risultato, al metodo Sostituisci viene assegnato un elenco di elementi delimitati da virgole: i due elementi nell'elenco rappresentano gli identificatori delle due unità organizzative Redmond e Portland da assegnare al nuovo ruolo RBAC.

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator" -UserScopes "OU:ou=Redmond,dc=litwareinc,dc=com","OU:ou=Portland,dc=litwareinc,dc=com"

## ESEMPIO 4

Nell'Esempio 4, il sito con SiteId Redmond è assegnato alla proprietà ConfigScopes per un nuovo ruolo RBAC. Si noti che la sintassi per la proprietà ConfigScopes prevede che il prefisso "site:" sia seguito dal valore della proprietà SiteId per il sito da aggiungere.

    New-CsAdminRole -Identity "RedmondVoiceAdministrator" -Template "CsVoiceAdministrator" -ConfigScopes "site:Redmond"

## Descrizione dettagliata

Il controllo di accesso basato sui ruoli (RBAC) consente agli amministratori di delegare il controllo di specifiche attività di gestione in Lync Server. Ad esempio, invece di concedere al personale dell'Help Desk dell'organizzazione privilegi completi di amministratore, è possibile concedere loro diritti molto specifici: il diritto di gestire esclusivamente gli account utente, il diritto di gestire esclusivamente i componenti di VoIP aziendale, il diritto di gestire esclusivamente l'archiviazione e il server di archiviazione. Questi diritti inoltre possono essere circoscritti a un ambito: a qualcuno può essere concesso il diritto di gestire VoIP aziendale, ma soltanto nel sito Redmond, a qualcun altro può essere concesso il diritto di gestire gli utenti, ma soltanto se i relativi account appartengono all'unità organizzativa Finance.

L'implementazione del controllo RBAC in Lync Server è basata su due elementi chiave: i gruppi di sicurezza di Active Directory e i cmdlet di Windows PowerShell. Quando si installa Lync Server, vengono creati automaticamente numerosi gruppi di sicurezza universali, ad esempio CsAdministrator, CsArchivingAdministrator e CsHelpDesk. Questi gruppi di sicurezza universali hanno una corrispondenza uno a uno con i ruoli RBAC. Ciò significa che ogni utente del gruppo di sicurezza CsArchivingAdministrator dispone di tutti i diritti concessi al ruolo RBAC CsArchivingAdministrator. A loro volta, i diritti concessi a un ruolo RBAC sono basati sui cmdlet assegnati a tale ruolo (i cmdlet possono essere assegnati a più ruoli RBAC). Si supponga ad esempio che a un ruolo siano stati assegnati i cmdlet seguenti:

Get-ArchivingPolicy

Grant-ArchivingPolicy

New-ArchivingPolicy

Remove-ArchivingPolicy

Set-ArchivingPolicy

Get-ArchivingConfiguration

New-ArchivingConfiguration

Remove-ArchivingConfiguration

Set-ArchivingConfiguration

Get-CsUser

Export-CsArchivingData

Get-CsComputer

Get-CsPool

Get-CsService

Get-CsSite

L'elenco sopra riportato include gli unici cmdlet che un utente, a cui sia stato assegnato un ipotetico ruolo di controllo di accesso basato sui ruoli (RBAC), è autorizzato a eseguire durante una sessione dell'interfaccia della riga di comando Windows PowerShell remota. Se l'utente tenta di eseguire il cmdlet **Disable-CsUser**, tale comando avrà esito negativo perché gli utenti a cui è stato assegnato quell'ipotetico ruolo non sono autorizzati a eseguire il cmdlet **Disable-CsUser**. Lo stesso vale per il Pannello di controllo di Lync Server. Un amministratore dell'archiviazione ad esempio non è autorizzato a disabilitare un utente utilizzando il Pannello di controllo di Lync Server, in quanto il Pannello di controllo di Lync Server è soggetto ai ruoli RBAC. Ogni volta che si esegue un comando nel Pannello di controllo di Lync Server, in realtà si sta chiamando un cmdlet di Windows PowerShell. Se non si è autorizzati a eseguire il cmdlet **Disable-CsUser**, non avrà alcuna importanza se si tenta di eseguirlo direttamente da Windows PowerShell o indirettamente nel Pannello di controllo di Lync Server. Il comando avrà comunque esito negativo.

Si noti che il ruolo RBAC si applica solo alla gestione remota. Se si è collegati a un computer con Lync Server e si apre Lync Server Management Shell, i ruoli RBAC non verranno applicati. In questo caso, la sicurezza viene garantita principalmente attraverso i gruppi di sicurezza RTCUniversalServerAdmins, RTCUniversalUserAdmins e RTCUniversalReadOnlyAdmins.

Quando si installa Lync Server, vengono creati numerosi ruoli RBAC predefiniti. Questi ruoli riguardano le aree amministrative comuni come l'amministrazione dell'audio, la gestione degli utenti e l'amministrazione di Response Group. Non è possibile modificare in alcun modo questi ruoli predefiniti: è impossibile aggiungere o rimuovere cmdlet dai ruoli o eliminare i ruoli. Qualsiasi tentativo di eliminare un ruolo predefinito genererà un errore. È tuttavia possibile utilizzare i ruoli predefiniti come base per la creazione di ruoli RBAC personalizzati. È possibile modificare i ruoli personalizzati cambiandone gli ambiti amministrativi. È ad esempio possibile limitare l'ambito del ruolo di gestione degli account utente a una determinata unità organizzativa di Active Directory.

Per creare un nuovo ruolo, è innanzitutto necessario creare un gruppo di sicurezza universale in Servizi di dominio Active Directory che condivida un nome con il ruolo. Ad esempio, per creare un nuovo ruolo denominato DialInConferencingAdministrator, è necessario creare un gruppo di sicurezza in cui SamAccountName è DialInConferencingAdministrator. Si noti che il cmdlet **New-CsAdminRole** non creerà automaticamente questo gruppo. Se il gruppo DialInConferencingAdministrator non esiste quando si chiama il cmdlet **New-CsAdminRole**, il comando avrà esito negativo. L'identità assegnata al nuovo ruolo deve essere il SamAccountName del corrispondente gruppo di Active Directory.

Dopo avere creato il gruppo di sicurezza di Active Directory, è necessario selezionare un ruolo RBAC incorporato come modello per il nuovo ruolo personalizzato. Non è possibile creare un ruolo RBAC vuoto utilizzando il cmdlet **New-CsAdminRole**. Tutti i ruoli personalizzati devono invece essere basati su uno dei ruoli RBAC incorporati. Ciò significa che un ruolo personalizzato deve avere gli stessi cmdlet assegnati a uno dei ruoli incorporati. È tuttavia possibile utilizzare il cmdlet **Set-CsAdminRole** per cambiare l'ambito amministrativo del ruolo personalizzato.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsAdminRole** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAdminRole"}

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
<td><p>System.String</p></td>
<td><p>Identificatore univoco per il ruolo RBAC da creare. L'identità di un ruolo RBAC deve essere uguale al SamAccountName del gruppo di sicurezza universale di Active Directory associato a quel ruolo. Ad esempio, il ruolo Help Desk ha un'identità uguale a CsHelpDesk; CsHelpDesk è anche il valore SamAccountName del gruppo di sicurezza di Active Directory associato a quel ruolo.</p></td>
</tr>
<tr class="even">
<td><p><em>Template</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome del ruolo RBAC incorporato che fungerà da modello per il nuovo ruolo RBAC personalizzato in corso di creazione. Tutti i nuovi ruoli RBAC devono essere basati su un ruolo esistente; non è possibile creare un ruolo RBAC &quot;vuoto&quot;, cioè un ruolo a cui non sono assegnati cmdlet o con un valore assegnato per la proprietà ConfigScope o UserScope. Tuttavia, una volta creato il nuovo ruolo personalizzato, sarà possibile utilizzare il cmdlet <strong>Set-CsAdminRole</strong> per modificarne le proprietà.</p></td>
</tr>
<tr class="odd">
<td><p><em>Cmdlets</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Consente di specificare i cmdlet che saranno disponibili per gli utenti a cui è assegnato il nuovo ruolo RBAC. Per creare ad esempio un nuovo ruolo che consenta l'accesso solo a un cmdlet (il cmdlet <strong>Export-CsArchivingData</strong>), utilizzare una sintassi simile alla seguente:</p>
<p>-Cmdlets &quot;Export-CsArchivingData&quot;</p>
<p>Per consentire l'accesso a più cmdlet, separare i nomi dei cmdlet con le virgole:</p>
<p>-Cmdlets &quot;Export-CsArchivingData&quot;,&quot;Invoke-CsArchivingDatabasePurge&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ConfigScopes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Utilizzato per limitare l'ambito del cmdlet alle impostazioni di configurazione del sito specificato. Per limitare l'ambito del cmdlet a un singolo sito, utilizzare una sintassi simile alla seguente: -ConfigScopes site:Redmond. È possibile specificare più siti separandoli con una virgola: -ConfigScopes &quot;site:Redmond, &quot;site:Dublin&quot;. È altresì possibile impostare la proprietà ConfigScopes su &quot;global&quot;.</p>
<p>Quando si assegna un valore al parametro ConfigScopes, è necessario utilizzare il prefisso &quot;site:&quot; seguito dal valore della proprietà SiteId del sito. Si noti che SiteID non ha necessariamente lo stesso valore del parametro Identity o DisplayName del sito. Per stabilire il valore di SiteId per un determinato sito, utilizzare un comando simile al seguente:</p>
<p>Get-CsSite &quot;Redmond&quot; | Select-Object SiteId</p>
<p>È necessario specificare un valore per almeno una delle proprietà ConfigScopes e UserScopes.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>ScriptModules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Consente di specificare una funzione in uno script di Windows PowerShell che sarà quindi disponibile per gli utenti a cui è assegnato il nuovo ruolo RBAC. La sintassi seguente ad esempio consente di accedere a una funzione denominata Reset in uno script denominato UpDatabase.ps1:</p>
<p>-ScriptModules &quot;UpdateDatabase.ps1:Reset&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>UserScopes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Utilizzato per limitare l'ambito del cmdlet alle attività di gestione degli utenti per l'unità organizzativa specificata. Per limitare l'ambito del cmdlet a una singola unità organizzativa (OU), utilizzare una sintassi simile alla seguente: -UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;. È possibile specificare più unità organizzative separandole con una virgola: -UserScopes &quot;OU:ou=Redmond,dc=litwareinc,dc=com&quot;, &quot;OU:ou=Dublin,dc=litwareinc,dc=com&quot;. Per aggiungere nuovi ambiti o rimuovere ambiti esistenti da un ruolo, utilizzare la sintassi dei modificatori di elenco di Windows PowerShell. Per informazioni dettagliate, vedere la sezione Esempi in questo argomento.</p>
<p>È necessario specificare un valore per almeno una delle proprietà ConfigScopes e UserScopes.</p></td>
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

Nessuno.

## Tipi restituiti

Il cmdlet **New-CsAdminRole** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Roles.Role.

