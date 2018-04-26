---
title: Get-CsClientVersionPolicyRule
TOCTitle: Get-CsClientVersionPolicyRule
ms:assetid: f81f4f6c-5201-46c5-89f6-da859ce99b2e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413048(v=OCS.15)
ms:contentKeyID: 49302527
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientVersionPolicyRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le regole dei criteri di versione client configurate per l'utilizzo nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsClientVersionPolicyRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientVersionPolicyRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite le informazioni su tutte le regole dei criteri di versione client attualmente in uso nell'organizzazione.

    Get-CsClientVersionPolicyRule

## ESEMPIO 2

Nell'esempio 2 vengono restituite le informazioni su una singola regola dei criteri di versione client: la regola con identità Global/2336c611-a243-4c5d-994b-eea8a524d0e4.

    Get-CsClientVersionPolicyRule -Identity "Global/2336c611-a243-4c5d-994b-eea8a524d0e4"

## ESEMPIO 3

Nell'esempio 3 vengono restituite tutte le regole dei criteri di versione client che sono state configurate nell'ambito globale. A tale scopo, il comando utilizza il parametro Filter e il valore del filtro "Global/\*". Tale valore del filtro restituisce solamente quelle regole con identità che inizia con il valore stringa "Global/".

    Get-CsClientVersionPolicyRule -Filter "Global/*"

## ESEMPIO 4

Il comando indicato nell'esempio 4 restituisce tutte le regole dei criteri di versione client che sono attualmente disabilitate. Per eseguire questa operazione, il comando effettua per prima cosa la chiamata del cmdlet **Get-CsClientVersionPolicy** per restituire la raccolta di tutte le regole dei criteri di versione client disponibili. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà Enabled è uguale a False.

    Get-CsClientVersionPolicyRule | Where-Object {$_.Enabled -eq $False}

## ESEMPIO 5

Nell'esempio 5 vengono restituite tutte le regole dei criteri di versione client che bloccano l'accesso a un'applicazione client. A tale scopo, il comando effettua per prima cosa la chiamata del cmdlet **Get-CsClientVersionPolicy** senza alcun parametro. In questo modo viene restituita la raccolta delle regole attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le regole in cui la proprietà Action è uguale a Block.

    Get-CsClientVersionPolicyRule | Where-Object {$_.Action -eq "Block"}

## Descrizione dettagliata

Le regole di criteri di versione client vengono utilizzate per determinare a quali applicazioni client è consentito effettuare l'accesso a Lync Server. Quando un utente tenta di accedere a Lync Server, la sua applicazione client invia un'intestazione SIP al server; questa intestazione contiene informazioni dettagliate sull'applicazione, inclusi versione principale, versione secondaria e numero di build. Le informazioni sulla versione vengono quindi confrontate con una raccolta di regole versione client per verificare se esiste una regola da applicare all'applicazione specifica. Si supponga, ad esempio, che un utente tenti di effettuare l'accesso utilizzando Microsoft Office Communicator 2007 R2. Prima che possa essere effettuato l'accesso a Lync Server, il sistema controllerà se esiste una regola di versione client valida per Office Communicator 2007 R2. Se tale regola esiste, Lync Server eseguirà l'azione specificata dalla regola. L'azione deve essere una tra quelle riportate di seguito:

Allow. All'utente sarà consentito effettuare l'accesso.

AllowAndUpgrade. All'utente sarà consentito effettuare l'accesso e la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

AllowWithUrl. All'utente sarà consentito effettuare l'accesso e verrà visualizzato un messaggio che lo indirizzerà a un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Block. All'utente non sarà consentito effettuare l'accesso.

BlockAndUpgrade. All'utente non sarà consentito effettuare l'accesso, ma la relativa copia di Communicator 2007 R2 verrà aggiornata automaticamente all'ultima versione di Lync. L'utente potrà quindi tentare di effettuare l'accesso utilizzando la nuova applicazione client. Gli aggiornamenti vengono eseguiti tramite Microsoft Update o Windows Server Update Services, in base alla configurazione del sistema.

BlockWithUrl. All'utente non sarà consentito effettuare l'accesso, ma verrà visualizzato un messaggio che lo indirizzerà ad un URL da cui sarà possibile scaricare e installare l'ultima versione di Lync. L'URL deve puntare a un sito Web creato precedentemente dall'utente, poiché tale sito non viene creato durante l'installazione di Lync Server.

Le regole di versione client vengono raccolte nei criteri di versione client che possono essere configurati nell'ambito globale, nell'ambito del sito, nell'ambito del servizio (servizio Registrar) o nell'ambito per utente. Il cmdlet **Get-CsClientVersionPolicyRule** consente agli amministratori di visualizzare informazioni dettagliate su ciascuna delle regole dei criteri configurate per l'utilizzo nell'organizzazione.

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsClientVersionPolicyRule** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientVersionPolicyRule"}

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
<td><p>Consente di utilizzare i caratteri jolly quando si specificano le regole dei criteri di versione client da restituire. Ad esempio, per restituire tutte le regole configurate per il sito di Redmond, utilizzare la seguente sintassi: -Filter &quot;site:Redmond/*&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco per la regola del criterio di versione client da recuperare. L'identità di una regola di versione client è costituita dall'ambito in cui la regola è stata configurata e da un identificatore univoco globale (GUID). La regola avrà un'identità simile a quella riportata di seguito: site:Redmond/1987d3c2-4544-489d-bbe3-59f79f530a83. Poiché i GUID sono difficili da ricordare e da utilizzare, nella sezione Esempi della Guida vengono elencati metodi alternativi che consentono di identificare le regole da restituire.</p>
<p>Se questo parametro non viene specificato, verranno restituite tutte le regole dei criteri di versione client configurate per l'utilizzo.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera la regola del criterio di versione client dalla replica locale del archivio di gestione centrale anziché dallo stesso archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClientVersionPolicyRule** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsClientVersionPolicyRule** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.Rule.

## Vedere anche

#### Ulteriori risorse

[New-CsClientVersionPolicyRule](new-csclientversionpolicyrule.md)  
[Remove-CsClientVersionPolicyRule](remove-csclientversionpolicyrule.md)  
[Set-CsClientVersionPolicyRule](set-csclientversionpolicyrule.md)

