---
title: Get-CsClientVersionPolicy
TOCTitle: Get-CsClientVersionPolicy
ms:assetid: d99bfa89-01a7-4dd4-8f6e-96e0a84ab1ce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398957(v=OCS.15)
ms:contentKeyID: 49302142
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientVersionPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui client, ad esempio Microsoft Office Communicator 2007 R2, supportati nell'ambiente Lync Server in uso. I criteri di versione client consentono di specificare quali client, ad esempio Office Communicator 2007 R2, saranno in grado di accedere al sistema Lync Server in uso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsClientVersionPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientVersionPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nel primo esempio il cmdlet **Get-CsClientVersionPolicy** viene chiamato senza specificare ulteriori parametri. In questo modo, il cmdlet **Get-CsClientVersionPolicy** restituirà una raccolta di tutti i criteri delle versioni client configurati per l'utilizzo nell'organizzazione.

    Get-CsClientVersionPolicy

## ESEMPIO 2

Nell'esempio 2 il cmdlet **Get-CsClientVersionPolicy** restituisce tutti i criteri delle versioni client con valore Identity site:Redmond. Poiché le identità devono essere univoche, il comando non restituirà mai più di un elemento.

    Get-CsClientVersionPolicy -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 vengono restituiti tutti i criteri delle versioni client configurati in ambito sito. A tale scopo, vengono inclusi il parametro Filter e il valore di filtro "site:\*". Tale valore indica al cmdlet **Get-CsClientVersionPolicy** di restituire solo i criteri il cui parametro Identity inizia con il valore stringa "site:".

    Get-CsClientVersionPolicy -Filter site:*

## ESEMPIO 4

Il comando utilizzato nell'esempio 4 visualizza le informazioni dettagliate sulle singole regole configurate per i criteri delle versioni client. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsClientVersionPolicy** per recuperare una raccolta di tutti i criteri delle versioni client configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che utilizza il filtro ExpandProperty per espandere i valori della proprietà Rules. Quando tale proprietà è espansa, vengono visualizzate informazioni dettagliate su ogni regola, tra cui valori di proprietà come il numero di build, la versione principale e la versione secondaria.

    Get-CsClientVersionPolicy | Select-Object -ExpandProperty Rules

## Descrizione dettagliata

I criteri di versione client rappresentano una raccolta di regole di versione client. Tali regole, a loro volta, vengono utilizzate per stabilire a quali applicazioni client è consentito l'accesso a Lync Server. Quando un utente tenta di accedere a Lync Server, la sua applicazione client invia un'intestazione SIP al server. In questa intestazione sono contenute informazioni dettagliate sull'applicazione, inclusi versione principale, versione secondaria e numero di build del software. In seguito, le informazioni sulla versione contenute nell'intestazione SIP vengono controllate a fronte di una raccolta di regole della versione client per verificare se alcune di queste regole si riferiscono a quella particolare applicazione. Se tale regola esiste, Lync Server eseguirà l'azione specificata dalla regola. La regola ad esempio potrebbe indicare a Lync Server di consentire l'accesso, di bloccarlo o di autorizzarlo e quindi di aggiornare l'applicazione client all'ultima versione, ad esempio da Communicator 2007 R2 a Lync, senza intervento dell'utente.

I criteri delle versioni client possono essere applicati nell'ambito globale, nell'ambito del sito, nell'ambito del servizio (solo servizio di registrazione) o nell'ambito per utente e offrono una notevole flessibilità nello stabilire quali applicazioni client possono essere utilizzate per accedere al sistema. È ad esempio possibile decidere di impedire agli utenti di accedere a Lync Server utilizzando Communicator 2007 R2 perché non supporta le stesse caratteristiche e funzionalità di Lync 2013. A causa di conflitti hardware o software, può tuttavia accadere che un gruppo di utenti non possa eseguire l'aggiornamento a Lync. In questo caso, è possibile creare una regola separata e un criterio delle versioni client distinto per consentire a tali utenti di accedere da Communicator 2007 R2.

Il cmdlet **Get-CsClientVersionPolicy** consente di recuperare tutti i criteri di versione client attualmente in uso nell'organizzazione, nonché di visualizzare le singole regole che costituiscono ognuno di questi criteri.

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsClientVersionPolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientVersionPolicy\\b"}

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
<td><p>Consente di utilizzare i caratteri jolly quando si specificano i criteri da recuperare. Ad esempio, questa sintassi restituisce tutti i criteri configurati in ambito sito: -Filter &quot;site:*&quot;. Questa sintassi restituisce tutti i criteri configurati in ambito per utente: -Filter &quot;tag:*&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il criterio da restituire. Per restituire il criterio globale, utilizzare la sintassi seguente: -Identity global. Per restituire un criterio configurato nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per restituire un criterio configurato nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;. Il servizio Registrar è l'unico servizio che può ospitare un criterio di versione client.</p>
<p>I criteri possono essere configurati anche in ambito per utente. Per restituire uno di questi criteri, utilizzare una sintassi simile alla seguente: -Identity &quot;SalesDepartmentPolicy&quot;.</p>
<p>Se questo parametro non viene incluso, verranno restituiti tutti i criteri di versione client configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati relativi ai criteri di versione client dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClientVersionPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsClientVersionPolicy** restituisce istanze dell'oggetto criteri Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersion.

## Vedere anche

#### Ulteriori risorse

[Grant-CsClientVersionPolicy](grant-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

