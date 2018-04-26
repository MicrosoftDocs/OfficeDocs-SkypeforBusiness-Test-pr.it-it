---
title: New-CsClientVersionPolicyRule
TOCTitle: New-CsClientVersionPolicyRule
ms:assetid: d28df005-0db0-4b17-9ca0-9dc9ed063d73
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398905(v=OCS.15)
ms:contentKeyID: 49302052
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionPolicyRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova regola di criteri di versione client. Le regole di questo tipo consentono di determinare se gli utenti possono utilizzare un'applicazione client specifica per accedere a Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsClientVersionPolicyRule -Identity <XdsIdentity> <COMMON PARAMETERS>

    New-CsClientVersionPolicyRule -Parent <String> -RuleId <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Action <Allow | AllowAndUpgrade | AllowWithUrl | Block | BlockAndUpgrade | BlockWithUrl>] [-ActionUrl <String>] [-BuildNumber <UInt16>] [-CompareOp <EQL | NEQ | GTR | GEQ | LSS | LEQ>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MajorVersion <UInt16>] [-MinorVersion <UInt16>] [-Priority <Int32>] [-QfeNumber <UInt16>] [-UserAgent <String>] [-UserAgentFullName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene illustrato come creare una nuova regola di criteri di versione client. Il parametro Identity delle regole di criteri è costituito da due parti: l'ambito in cui deve essere assegnato l'annuncio e un GUID di 36 caratteri. Per creare un parametro Identity per una nuova regola di criteri di versione client, è necessario innanzitutto utilizzare il metodo NewGuid di .NET Framework al fine di creare un nuovo GUID. Questo passaggio viene eseguito nel primo comando dell'esempio, in cui il GUID risultante viene archiviato nella variabile $x.

Dopo la creazione del GUID, è possibile utilizzare il cmdlet **New-CsClientVersionPolicyRule** per creare la nuova regola. Questo comando utilizza quattro parametri: Parent, il cui valore rappresenta l'ambito (site:Redmond) della nuova regola, RuleId, il cui valore $x rappresenta il GUID appena creato, MajorVersion (4) e UserAgent (InHouse). In questo caso, il parametro UserAgent rappresenta un'applicazione client interna.

    $x = [guid]::NewGuid()
    
    New-CsClientVersionPolicyRule -Parent "site:Redmond" -RuleId $x -MajorVersion 4 -UserAgent InHouse

## ESEMPIO 2

I comandi mostrati nell'esempio 2 rappresentano una variazione dei comandi mostrati nel primo esempio. In questo caso tuttavia la nuova regola viene creata inizialmente solo in memoria e aggiunta successivamente a Lync Server. A tale scopo, il primo comando dell'esempio crea la parte GUID del parametro Identity. Con il secondo comando viene creata una nuova regola di criteri di versione client solo in memoria. Il parametro InMemory garantisce che la regola sia presente solo in memoria e che non venga aggiunta immediatamente all'infrastruttura di Lync Server. Come nell'esempio 1, i parametri Parent e RuleId vengono utilizzati per specificare l'ambito e il GUID della nuova regola, ovvero le due parti che costituiscono il parametro Identity della regola.

Dopo la creazione della regola virtuale, i due comandi successivi vengono utilizzati per assegnare rispettivamente i valori alle proprietà MajorVersion e UserAgent. Dopo aver completato queste attività, nell'ultimo comando dell'esempio viene utilizzato il cmdlet **Set-CsClientVersionPolicyRule** per creare la regola di criteri di versione client vera e propria e assegnarla al sito Redmond.

    $x = [guid]::NewGuid()
    
    $z = New-CsClientVersionPolicyRule -Parent "site:Redmond" -RuleId $x -InMemory
    $z.MajorVersion = 4 
    $z.UserAgent = "Inhouse"
    Set-CsClientVersionPolicyRule -Instance $z

## Descrizione dettagliata

Le regole di criteri di versione client vengono utilizzate per determinare a quali applicazioni client è consentito effettuare l'accesso a Lync Server. Quando un utente tenta di accedere a Lync Server, la sua applicazione client invia un'intestazione SIP al server; questa intestazione contiene informazioni dettagliate sull'applicazione, inclusi versione principale, versione secondaria e numero di build. Le informazioni sulla versione vengono quindi confrontate con una raccolta di regole versione client per verificare se esiste una regola da applicare all'applicazione specifica. Si supponga, ad esempio, che un utente tenti di effettuare l'accesso utilizzando Microsoft Office Communicator 2007 R2. Prima che possa essere effettuato l'accesso a Lync Server, il sistema controllerà se esiste una regola di versione client valida per Office Communicator 2007 R2. Se tale regola esiste, Lync Server eseguirà l'azione specificata dalla regola. L'azione deve essere una tra quelle riportate di seguito:

Allow. All'utente sarà consentito effettuare l'accesso.

AllowAndUpgrade. All'utente sarà consentito effettuare l'accesso e la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

AllowWithUrl. All'utente sarà consentito effettuare l'accesso e verrà visualizzato un messaggio che lo indirizzerà a un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Block. All'utente non sarà consentito effettuare l'accesso.

BlockAndUpgrade. All'utente non sarà consentito effettuare l'accesso, ma la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. L'utente potrà quindi tentare di effettuare l'accesso utilizzando la nuova applicazione client. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

BlockWithUrl. All'utente non sarà consentito effettuare l'accesso, ma verrà visualizzato un messaggio che lo indirizzerà ad un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Le regole per i criteri delle versioni client vengono raccolte in criteri delle versioni client, che possono essere configurati nell'ambito globale, del sito, del servizio (servizio di registrazione) o per utente. Le nuove regole delle versioni client vengono create con il cmdlet **New-CsClientVersionPolicyRule**. Quando si crea un nuova regola, è inoltre necessario specificare il parametro Identity di tale regola. Questo parametro è costituito da un ambito, ad esempio site:Redmond, e da un identificatore univoco globale (GUID). È possibile specificare direttamente un valore per il parametro Identity oppure crearlo mediante il cmdlet **New-CsClientVerisonPolicyRule** specificando l'ambito (parametro Parent) e il GUID (parametro RuleId).

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsClientVersionPolicyRule** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionPolicyRule"}

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
<td><p>Identificatore univoco per la regola di criteri di versione client creata. L'identità di una regola di criteri di versione client è costituita dall'ambito in cui la regola è stata configurata e da un identificatore univoco globale (GUID). La regola avrà un'identità simile a quella riportata di seguito: site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>Anziché utilizzare il parametro Identity, è possibile utilizzare i parametri Parent e RuleId in modo da creare l'identità tramite il cmdlet <strong>New-CsClientVerisonPolicyRule</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Informazioni sull'ambito per la nuova regola. Per utilizzare il parametro Parent e creare una nuova regola per il criterio globale, utilizzare la seguente sintassi: -Parent global. Per creare una nuova regola per un criterio di sito, utilizzare una sintassi simile alla seguente: -Parent &quot;site:Redmond&quot;. Per creare una nuova regola per un criterio di servizio, utilizzare una sintassi simile alla seguente: -parent &quot;Registrar:atl-cs-001.litwareinc.com&quot;. Per creare una nuova regola per un criterio per utente, utilizzare una sintassi simile alla seguente: -Parent &quot;RedmondClientVersionPolicy&quot;.</p>
<p>Quando si crea una nuova regola, è necessario utilizzare il parametro Identity oppure entrambi i parametri Parent e RuleId.</p></td>
</tr>
<tr class="odd">
<td><p><em>RuleId</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco globale (GUID) della regola. In Windows PowerShell è possibile creare un GUID utilizzando il seguente comando:</p>
<p>$x = [guid]::NewGuid()</p>
<p></p></td>
</tr>
<tr class="even">
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
<tr class="odd">
<td><p><em>ActionUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL da cui gli utenti possono scaricare la versione più recente di Lync. Questa proprietà è obbligatoria se il parametro Action è impostato su BlockWithUrl o AllowWithUrl.</p></td>
</tr>
<tr class="even">
<td><p><em>BuildNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Numero build del software. Se ad esempio la versione della copia di Communicator è 2.0.6362.111, il parametro BuildNumber sarà 6362. I numeri di build rappresentano le versioni interne del software durante il processo di sviluppo e garantiscono che venga utilizzata la versione finale anziché una versione non definitiva.</p></td>
</tr>
<tr class="odd">
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
<td><p>Consente agli amministratori di fornire informazioni aggiuntive sulla regola versione client. Ad esempio, il parametro Description potrebbe includere le informazioni sulla persona da contattare nel caso in cui si ritenga che la regola debba essere modificata.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se utilizzare la regola versione client. Se la proprietà Enabled è impostata su False ($False), la regola verrà ignorata ogni volta che l'utente tenta di effettuare l'accesso con il software specificato. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MajorVersion</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Versione principale del software. Se ad esempio la versione della copia di Communicator è 2.0.6362.111, il parametro MajorVersion sarà 2. Le versioni principali corrispondono alle versioni principali del software. È necessario assegnare un valore alla proprietà MajorVersion ogni volta che si crea una nuova regola.</p></td>
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
<td><p>Priorità relativa della regola. Le regole vengono elaborate in ordine di priorità, con la regola con priorità 0 elaborata per prima, la regola con priorità 1 elaborata per seconda e così via. Se si assegna una priorità già in uso, la nuova regola utilizzerà tale priorità e le altre regole verranno rinumerate di conseguenza.</p></td>
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
<td><p>Indicatore utilizzato per identificare il client software. OC ad esempio è la designazione di agente utente per Communicator.</p></td>
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

Nessuno. Il cmdlet **New-CsClientVersionPolicyRule** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsClientVersionPolicyRule** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionPolicyRule](get-csclientversionpolicyrule.md)  
[Remove-CsClientVersionPolicyRule](remove-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

