---
title: Move-CsLegacyUser
TOCTitle: Move-CsLegacyUser
ms:assetid: f4b36fc8-17a7-490d-a147-6d77abab0f92
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413025(v=OCS.15)
ms:contentKeyID: 49302487
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsLegacyUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esegue la migrazione di uno o più account da Microsoft Office Communications Server 2007 R2 a Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsLegacyUser -Identity <UserIdParameter> -Target <Fqdn> [-Confirm [<SwitchParameter>]] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-ExcludeArchivingPolicy <SwitchParameter>] [-ExcludeConferencingPolicy <SwitchParameter>] [-ExcludeDialPlan <SwitchParameter>] [-ExcludeExternalAccessPolicy <SwitchParameter>] [-ExcludePresencePolicy <SwitchParameter>] [-ExcludeVoicePolicy <SwitchParameter>] [-Force <SwitchParameter>] [-HostedMigrationOverrideUrl <String>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-ProxyPool <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, il cmdlet **Move-CsLegacyUser** è utilizzato per eseguire la migrazione dell'account utente con identità Pilar Ackerman al pool di registrazione atl-cs-001.litwareinc. Poiché non sono inclusi altri parametri, verrà eseguita la migrazione anche di tutti i criteri o di tutte le impostazioni precedentemente assegnate all'account. Questo significa che se un criterio precedente (ad esempio un dial plan) era stato assegnato a Pilar Ackerman, a questa stessa persona verrà assegnato il criterio equivalente in Lync Server 2013 quando verrà spostato l'account.

    Move-CsLegacyUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com"

## ESEMPIO 2

Il comando riportato nell'esempio 2 mostra la migrazione dell'account utente di Pilar Ackerman, ma non esegue la migrazione dei dial plan precedentemente assegnati al suo account. Al termine della migrazione dell'account, Pilar non disporrà di un dial plan assegnato.

    Move-CsLegacyUser -Identity "Pilar Ackerman" -Target "atl-cs-001.litwareinc.com" -ExcludeDialPlan 

## ESEMPIO 3

Nell'esempio 3 tutti gli account utente nell'unità organizzativa Finance vengono spostati nel pool di registrazione atl-cs-001.litwareinc.com. Per eseguire questa attività, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsUser** e il parametro OU per recuperare una raccolta di tutti gli account utente nell'unità organizzativa Finance. Dopo aver recuperato gli account, la raccolta viene inviata tramite pipe al cmdlet **Move-CsLegacyUser**, che sposta ciascun account nel nuovo pool di registrazione. Nel comando si presuppone che tutti gli utenti dell'unità organizzativa Finance siano utenti precedenti.

    Get-CsUser -OU "ou=Finance,dc=litwareinc,dc=com" | Move-CsLegacyUser -Target "atl-cs-001.litwareinc.com"

## ESEMPIO 4

Nell'esempio 4, Move-CsLegacyUser viene utilizzato per assegnare un pool di registrazione a tutti gli utenti abilitati per Lync Server ma non attualmente assegnati a un pool di registrazione. In questo comando, il cmdlet **Get-CsUser** viene utilizzato insieme al parametro UnassignedUser per restituire una raccolta di tutti gli utenti che attualmente non sono assegnati a un pool di registrazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Move-CsLegacyUser**, che assegna ciascun utente al pool atl-cs-001.litwareinc.com. Questo esempio presuppone che tutti gli utenti non assegnati siano utenti legacy.

    Get-CsUser -UnassignedUser | Move-CsLegacyUser -Target "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

In molte organizzazioni che installano Lync Server 2013 sono in esecuzione anche versioni precedenti del software. Questo fatto comunque non rappresenta un problema: è possibile eseguire contemporaneamente entrambe le versioni del software. Nel tempo è possibile iniziare la migrazione delle impostazioni di configurazione, dei criteri ed infine degli account utente verso Lync Server 2013.

Il cmdlet **Move-CsLegacyUser** non solo consente di eseguire la migrazione degli utenti a Lync Server 2013, ma offre anche la possibilità di esercitare un notevole controllo sul processo di migrazione. Ad esempio, nella forma più semplice, è possibile assegnare al cmdlet **Move-CsLegacyUser** l'identità dell'utente di cui si intende eseguire la migrazione e il nome di dominio completo del pool di registrazione di Lync Server in cui verrà inserito l'account utente. A sua volta, il cmdlet **Move-CsLegacyUser** sposterà l'account utente e manterrà tutti i criteri e le impostazioni esistenti applicati all'account. Ad esempio, si supponga che a Davide Garghentini sia stato assegnato un dial plan in Communications Server 2007 R2. Per impostazione predefinita, quando si esegue la migrazione dell'account di Davide, la migrazione riguarda anche il rispettivo dial plan: ciò significa che il cmdlet **Move-CsLegacyUser** assegnerà automaticamente a Davide Garghentini il dial plan di Lync Server 2013 equivalente a quello che gli era stato assegnato in precedenza.

Ovviamente, questo si verifica solo se è stata eseguita la migrazione dei dial plan e se esiste un dial plan in Lync Server 2013 equivalente a quello precedentemente assegnato a Davide Garghentini. In alternativa, sarebbe stato possibile scegliere di non eseguire la migrazione dei dial plan. In quel caso, è possibile chiamare il cmdlet **Move-CsLegacyUser** insieme al parametro ExcludeDialPlan. Quando si utilizza questo parametro, non viene eseguita la migrazione di dial plan insieme all'account utente: ciò significa che l'account utente di Davide Garghentini verrà spostato ma non gli verrà assegnato un dial plan. Ciò si verificherà anche se si esegue la migrazione dei dial plan. Il parametro ExcludeDialPlan impedisce che a un account utente sottoposto a migrazione venga assegnato un dial plan. Gli altri parametri consentono di escludere criteri vocali, criteri di conferenza, criteri di archiviazione, criteri di accesso esterno e/o criteri di presenza quando si esegue la migrazione di un account utente.

Prima di eseguire il cmdlet **Merge-CsLegacyTopology**, è necessario installare il pacchetto di interfacce per la compatibilità con le versioni precedenti di Strumentazione gestione Windows (WMI). Questa applicazione viene installata eseguendo OCSWMIBC.msi, disponibile sul DVD di installazione nella cartella di installazione. Dopo aver installato il pacchetto di interfacce per la compatibilità, è possibile chiamare il cmdlet **Merge-CsLegacyUser** per spostare uno o più account utente.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Move-CsLegacyUser** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsLegacyUser"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente di cui eseguire la migrazione. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Servizi di dominio Active Directory dell'utente (ad esempio, Davide Garghentini). Alle identità utente è anche possibile fare riferimento utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti con un nome visualizzato che termina con la stringa &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Target</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del pool di registrazione dove l'account utente deve essere domiciliato. Ad esempio: -Target atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet Move-CsLegacyUser con credenziali alternative. Questo potrebbe essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari per l'utilizzo degli oggetti utente.</p>
<p>Per utilizzare il parametro Credential, è innanzitutto necessario creare un oggetto PSCredential tramite il cmdlet Get-Credential. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet Get-Credential.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di connettersi al controller di dominio specificato per spostare un account utente. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-cs-001) o dal suo FQDN (ad esempio, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presenti, tutti i criteri di archiviazione assegnati all'account utente non verranno mantenuti durante la migrazione dell'account.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeConferencingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presenti, tutti i criteri di conferenza assegnati all'account utente non verranno mantenuti durante la migrazione dell'account.</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeDialPlan</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, qualsiasi dial plan assegnato all'account utente non verrà mantenuto durante la migrazione dell'account.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeExternalAccessPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, qualsiasi criterio di accesso esterno assegnato all'account utente non verrà mantenuto durante la migrazione dell'account.</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludePresencePolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se disponibili, tutti i criteri di presenza assegnati all'account utente non verranno mantenuti durante la migrazione dell'account.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeVoicePolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presenti, tutti i criteri vocali assegnati all'account utente non verranno mantenuti durante la migrazione dell'account.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedMigrationOverrideUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL del servizio di migrazione ospitato utilizzato per lo spostamento di un utente nella versione Office 365 di Lync Server 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, indica al computer di ignorare eventuali errori che potrebbero verificarsi con il database back-end e tenta di spostare il telefono area comune malgrado questi errori.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di specificare attraverso la pipeline un oggetto utente che rappresenta l'account utente che si sta spostando. Per impostazione predefinita, il cmdlet <strong>Move-CsLegacyUser</strong> non passa oggetti attraverso la pipeline.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyPool</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Questo parametro è utilizzato solo per Communications Server 2007 R2. Non deve essere utilizzato con un'implementazione locale di Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Move-CsLegacyUser** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Move-CsLegacyUser** non restituisce valori o oggetti. Invece, il cmdlet sposta le istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser.

## Vedere anche

#### Ulteriori risorse

[Import-CsLegacyConfiguration](import-cslegacyconfiguration.md)  
[Import-CsLegacyConferenceDirectory](import-cslegacyconferencedirectory.md)  
[Merge-CsLegacyTopology](merge-cslegacytopology.md)  
[Move-CsUser](move-csuser.md)  
[Set-CsUser](set-csuser.md)

