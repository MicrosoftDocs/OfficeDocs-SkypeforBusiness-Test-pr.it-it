---
title: Set-CsClientVersionPolicy
TOCTitle: Set-CsClientVersionPolicy
ms:assetid: cf7c1a6c-b8a9-4609-97f4-6c8ef9e45be7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398876(v=OCS.15)
ms:contentKeyID: 49302027
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio di versione client esistente. I criteri di versione client consentono di specificare quali client (ad esempio Microsoft Office Communicator 2007 R2) saranno autorizzati ad accedere al sistema Lync Server in uso. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsClientVersionPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-Rules <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 copiano tutte le regole delle versioni client tra criteri delle versioni client. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **Set-CsClientVersionPolicy** per rimuovere tutte le regole dal criterio site:Redmond, tramite l'impostazione su Null del valore della proprietà Rules. Dopo l'eliminazione delle regole, nel secondo comando dell'esempio viene utilizzato il cmdlet **Get-CsClientVersionPolicy** per recuperare tutte le regole dei criteri delle versioni client configurate per i criteri site:Dublin. Le regole vengono archiviate in una variabile denominata $x.

Nell'ultimo comando viene richiamato di nuovo il cmdlet **Set-CsClientVersionPolicy**, questa volta con la proprietà Rules dei criteri Redmond impostata su $x. In questo modo tutte le regole vengono copiate dai criteri site:Dublin e aggiunte ai criteri site:Redmond.

    Set-CsClientVersionPolicy -Identity site:Redmond -Rules $Null
    
    $x = Get-CsClientVersionPolicy -Identity site:Dublin | Select-Object -ExpandProperty Rules
    
    Set-CsClientVersionPolicy -Identity site:Redmond -Rules $x

## Descrizione dettagliata

I criteri di versione client rappresentano una raccolta di regole di versione client. Tali regole, a loro volta, vengono utilizzate per stabilire a quali applicazioni client è consentito l'accesso a Lync Server. Quando un utente tenta di accedere a Lync Server, la sua applicazione client invia un'intestazione SIP al server. In questa intestazione sono contenute informazioni dettagliate sull'applicazione, inclusi versione principale, versione secondaria e numero di build del software. In seguito, le informazioni sulla versione contenute nell'intestazione SIP vengono controllate a fronte di una raccolta di regole della versione client per verificare se alcune di queste regole si riferiscono a quella particolare applicazione. Se tale regola esiste, Lync Server eseguirà l'azione specificata dalla regola. La regola ad esempio potrebbe indicare a Lync Server di consentire l'accesso, di bloccarlo o di autorizzarlo e quindi di aggiornare l'applicazione client all'ultima versione, ad esempio da Communicator 2007 R2 a Lync 2013, senza intervento dell'utente.

I criteri di versione client possono essere applicati nell'ambito globale, nell'ambito del sito, nell'ambito del servizio (solo servizio di registrazione) o nell'ambito per utente e offrono una notevole flessibilità nello stabilire quali applicazioni client possono essere utilizzate per accedere al sistema. È ad esempio possibile decidere di impedire agli utenti di accedere a Lync Server utilizzando Communicator 2007 R2 perché non supporta le stesse caratteristiche e funzionalità di Lync. A causa di conflitti hardware o software, può tuttavia accadere che un gruppo di utenti non possa eseguire l'aggiornamento a Lync. In questo caso, è possibile creare una regola separata e un criterio di versione client distinto per consentire a tali utenti di effettuare l'accesso da Communicator 2007 R2.

I criteri di versione client possono essere modificati in qualsiasi momento. Modificare un criterio di versione client significa in genere aggiungere nuove regole, eliminare regole esistenti o modificare le proprietà di una regola esistente, ad esempio modificando un'azione della regola da Allow a Block. Queste modifiche possono essere effettuate mediante il cmdlet **Set-CsClientVersionPolicy**. Risulterà probabilmente più semplice apportare queste modifiche utilizzando invece il cmdlet **CsClientVersionPolicyRule**.

Il cmdlet **Set-CsClientVersionPolicy** consente invece di copiare facilmente un intero set di regole tra criteri delle versioni client. Per informazioni dettagliate, vedere la sezione degli esempi in questo argomento della Guida.

È importante notare che i criteri di versione client non vengono applicati agli utenti federati, poiché essi sono vincolati dai criteri di versione client utilizzati nell'organizzazione di appartenenza. Si supponga ad esempio che un utente federato utilizzi il client A, un client consentito dall'organizzazione federata. Se l'organizzazione federata consente l'utilizzo del client A, l'utente potrà comunicare con l'organizzazione mediante tale client. Ciò si verifica anche se il criterio di versione client blocca l'uso del client A. I criteri di versione client adottati nell'organizzazione non sostituiscono i criteri di versione client utilizzati nell'organizzazione federata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsClientVersionPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionPolicy\\b"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di fornire informazioni esplicative su un criterio. È possibile ad esempio fornire informazioni che descrivano gli utenti a cui deve essere assegnato il criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il criterio da modificare. Per modificare il criterio globale, utilizzare la sintassi seguente: -Identity global. Per modificare un criterio configurato nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per modificare un criterio configurato nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;Registrar:atl-cs-001.litwareinc.com&quot;. Il servizio Registrar è l'unico servizio che può ospitare un criterio di versione client.</p>
<p>Con questo cmdlet è possibile modificare anche i criteri per utente. Per modificare un criterio per utente, utilizzare una sintassi simile alla seguente: -Identity &quot;SalesDepartmentPolicy&quot;.</p>
<p>Se questo parametro non viene incluso, il cmdlet <strong>Set-CsClientVersionPolicy</strong> modificherà i criteri globali.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto ClientVersionPolicy</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Rules</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di singole regole dei criteri client assegnate al criterio.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy. Il cmdlet **Remove-CsClientVersionPolicy** accetta le istanze da pipeline dell'oggetto criteri delle versioni client.

## Tipi restituiti

Il cmdlet **Set-CsClientVersionPolicy** non restituisce un oggetto o un valore. Il cmdlet configura invece istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionPolicy](get-csclientversionpolicy.md)  
[New-CsClientVersionPolicy](new-csclientversionpolicy.md)  
[Remove-CsClientVersionPolicy](remove-csclientversionpolicy.md)  
[Set-CsClientVersionPolicy](set-csclientversionpolicy.md)

