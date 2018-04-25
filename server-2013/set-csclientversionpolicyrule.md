---
title: Set-CsClientVersionPolicyRule
TOCTitle: Set-CsClientVersionPolicyRule
ms:assetid: 2e061fa8-bb1a-4382-bb0d-298f81aefb3d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425790(v=OCS.15)
ms:contentKeyID: 49300056
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionPolicyRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una o più regole dei criteri di versione client configurate per l'utilizzo nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsClientVersionPolicyRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionPolicyRule [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | AllowAndUpgrade | AllowWithUrl | Block | BlockAndUpgrade | BlockWithUrl>] [-ActionUrl <String>] [-BuildNumber <UInt16>] [-CompareOp <EQL | NEQ | GTR | GEQ | LSS | LEQ>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-MajorVersion <UInt16>] [-MinorVersion <UInt16>] [-Priority <Int32>] [-QfeNumber <UInt16>] [-UserAgent <String>] [-UserAgentFullName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di disabilitare la regola per i criteri della versione client con Identity site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820. Per disabilitare la regola, il comando include il parametro Enabled e il valore del parametro $False.

    Set-CsClientVersionPolicyRule -Identity site:Redmond/74ba9211-8610-42f9-91ba-846cdee98820 -Enabled $False

## ESEMPIO 2

Nell'esempio 2 viene aggiunta una descrizione generica a tutte le regole dei criteri di versione client assegnate al sito Redmond. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsClientVersionPolicyRule** con il parametro Filter. Il valore di filtro "site:Redmond\*" restituisce solo i dati relativi alle regole dei criteri assegnate al sito Redmond. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsClientVersionPolicyRule**, che assegna la descrizione "Client policy rules for Redmond" a ogni elemento della raccolta.

    Get-CsClientVersionPolicyRule -Filter "site:Redmond*" | Set-CsClientVersionPolicyRule -Description "Client policy rules for Redmond"

## ESEMPIO 3

Nell'esempio 3 viene bloccato l'utilizzo dei client UCCP (Unified Communications Client Platform) per qualsiasi regola dei criteri di versione client che fa riferimento a UCCP come agente utente. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsClientVersionPolicyRule** per restituire una raccolta di tutte le regole dei criteri client attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà UserAgent è uguale a (-eq) UCCP. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsClientVersionPolicyRule**, che imposta su Block la proprietà Action di ogni elemento della raccolta.

    Get-CsClientVersionPolicyRule | Where-Object {$_.UserAgent -eq "UCCP"} | Set-CsClientVersionPolicyRule -Action "Block"

## Descrizione dettagliata

Le regole della versione client vengono utilizzate per stabilire quali applicazioni client sono autorizzate ad accedere a Lync Server. Quando un utente tenta di accedere a Lync Server, la relativa applicazione client invia un'intestazione SIP al server. Questa intestazione include informazioni dettagliate sull'applicazione, tra cui versione principale, versione secondaria e numero di build del software. Le informazioni sulla versione vengono quindi verificate in base a una raccolta di regole della versione client per valutare se qualcuna delle regole sia applicabile a quella particolare applicazione. Si supponga ad esempio che un utente tenti di accedere utilizzando Microsoft Office Communicator 2007 R2. Prima che l'accesso a Lync Server possa avere luogo, il sistema verifica l'eventuale presenza di una regola della versione client applicabile a Office Communicator 2007 R2. Se tale regola esiste, Lync Server eseguirà l'azione specificata dalla regola. L'azione deve essere una delle seguenti:

Allow. All'utente sarà consentito effettuare l'accesso.

AllowAndUpgrade. All'utente sarà consentito effettuare l'accesso e la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

AllowWithUrl. All'utente sarà consentito effettuare l'accesso e verrà visualizzato un messaggio che lo indirizzerà a un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Block. All'utente non sarà consentito effettuare l'accesso.

BlockAndUpgrade. All'utente non sarà consentito effettuare l'accesso, ma la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. L'utente potrà quindi tentare di effettuare l'accesso utilizzando la nuova applicazione client. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

BlockWithUrl. All'utente non sarà consentito effettuare l'accesso, ma verrà visualizzato un messaggio che lo indirizzerà ad un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Le regole della versione client sono raccolte nei criteri della versione client; questi criteri possono essere configurati nell'ambito globale, nell'ambito del sito, nell'ambito del servizio (servizio di registrazione) o nell'ambito del singolo utente. Il cmdlet **Set-CsClientVersionPolicyRule** offre la possibilità di modificare le proprietà di una regola per la versione client.

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsClientVersionPolicyRule** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionPolicyRule"}

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
<td><p><em>Action</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Action</p></td>
<td><p>Azione da intraprendere ogni volta che viene attivata la regola, ovvero ogni volta che qualcuno tenta di effettuare l'accesso utilizzando il software specificato. I valori validi sono:</p>
<p>Allow. All'utente sarà consentito effettuare l'accesso.</p>
<p>AllowWithUrl. All'utente sarà consentito effettuare l'accesso e verrà visualizzato un messaggio che lo indirizzerà a un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync.</p>
<p>AllowAndUpgrade. All'utente sarà consentito effettuare l'accesso e la relativa copia di Communicator verrà aggiornata automaticamente all'ultima versione di Lync.</p>
<p>Block. All'utente non sarà consentito effettuare l'accesso.</p>
<p>BlockWithUrl. All'utente non sarà consentito effettuare l'accesso, ma verrà visualizzato un messaggio che lo indirizzerà a un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync.</p>
<p>BlockAndUpgrade. All'utente non sarà consentito effettuare l'accesso, ma la relativa copia di Communicator verrà aggiornata automaticamente all'ultima versione di Lync. L'utente potrà quindi tentare di effettuare l'accesso utilizzando la nuova applicazione client.</p></td>
</tr>
<tr class="even">
<td><p><em>ActionUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL da cui gli utenti possono scaricare la versione più recente di Lync. Questa proprietà è obbligatoria se il parametro Action è impostato su BlockWithUrl o AllowWithUrl.</p></td>
</tr>
<tr class="odd">
<td><p><em>BuildNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero build del software. Se ad esempio la versione della copia di Communicator è 2.0.6362.111, il parametro BuildNumber sarà 6362. I numeri di build rappresentano le versioni interne del software durante il processo di sviluppo e garantiscono che venga utilizzata la versione finale anziché una versione non definitiva.</p></td>
</tr>
<tr class="even">
<td><p><em>CompareOp</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.CompareOp</p></td>
<td><p>Operatore di confronto utilizzato per determinare se il software client che sta tentando di effettuare l'accesso è stato rilasciato prima, dopo o contemporaneamente alla versione specificata nella regola. I valori validi sono:</p>
<p>EQL (uguale a)</p>
<p>NEQ (non uguale a)</p>
<p>GTR (maggiore di)</p>
<p>GEQ (maggiore o uguale a)</p>
<p>LSS (minore di)</p>
<p>LEQ (minore o uguale a)</p></td>
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
<td><p>Consente agli amministratori di fornire informazioni aggiuntive sulla regola versione client. Ad esempio, il parametro Description potrebbe includere le informazioni sulla persona da contattare nel caso in cui si ritenga che la regola debba essere modificata.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se deve essere utilizzata la regola della versione client. Se la proprietà Enabled è impostata su False, la regola verrà ignorata ogni volta che un utente tenterà di connettersi con il software specificato. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della regola per i criteri della versione client da modificare. L'identità di una regola della versione client è costituita dall'ambito in cui la regola è stata configurata più un identificatore univoco globale (GUID). Ciò significa che una regola avrà un'identità simile alla seguente: site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto regola</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MajorVersion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Versione principale del software. Ad esempio, se la copia di Communicator è versione 2.0.6362.111, MajorVersion è 2. Le versioni principali corrispondono al rilascio primario del software.</p></td>
</tr>
<tr class="even">
<td><p><em>MinorVersion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Versione secondaria del software. Se ad esempio la versione della copia di Communicator è 2.0.6362.111, il parametro MinorVersion sarà 0. Le versioni secondarie corrispondono alle versioni intermedie del software.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Priorità relativa della regola. Le regole sono elaborate secondo l'ordine di priorità; la regola con priorità 0 è elaborata per prima, la regola con priorità 1 è elaborata per seconda e così via. Se si assegna una priorità già utilizzata, alla nuova regola verrà applicata quella priorità e le altre regole verranno rinumerate di conseguenza.</p></td>
</tr>
<tr class="even">
<td><p><em>QfeNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero QFE (Quick Fix Engineering) del software. Se ad esempio la versione della copia di Communicator è 2.0.6362.111, il parametro QfeNumber sarà 111. I numeri QFE rappresentano gli aggiornamenti pianificati per un'applicazione resi disponibili dopo la distribuzione della versione ufficiale del software.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAgent</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indicatore utilizzato per identificare il client software. Ad esempio, OC è l'indicatore dell'agente utente per Communicator. Il cmdlet <strong>Get-CsClientVersionConfiguration</strong> fornisce nome descrittivi corrispondenti per ogni indicazione di agente utente.</p></td>
</tr>
<tr class="even">
<td><p><em>UserAgentFullName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire un nome descrittivo per l'agente utente. Anziché, ad esempio, fare affidamento sulla piattaforma UCCP (Unified Communications Client Platform) dell'agente utente per identificare l'agente, gli amministratori possono specificare il nome per intero: Microsoft Unified Communications Client.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule. Il cmdlet **Set-CsClientVersionPolicyRule** accetta istanze dell'oggetto regola versione client inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsClientVersionPolicyRule** invece modifica le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionPolicyRule](get-csclientversionpolicyrule.md)  
[New-CsClientVersionPolicyRule](new-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

