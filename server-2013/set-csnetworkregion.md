---
title: Set-CsNetworkRegion
TOCTitle: Set-CsNetworkRegion
ms:assetid: ffa1774b-ac60-4392-ad55-07bb887bf945
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413089(v=OCS.15)
ms:contentKeyID: 49302591
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un'area di rete esistente. Le aree di rete rappresentano hub di rete o backbone in una rete aziendale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkRegion [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkRegion [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-CentralSite <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene modificata l'area di rete denominata NorthAmerica. Al parametro Description viene assegnato il valore "North American Region". Se esiste già una descrizione per l'area NorthAmerica, con questo comando se ne sovrascriverà il valore, in caso contrario il valore verrà impostato.

    Set-CsNetworkRegion -Identity NorthAmerica -Description "North American Region"

## ESEMPIO 2

Con questo esempio viene modificata l'area di rete denominata EMEA e viene assegnata a tale area una nuova impostazione di percorso alternativo video. A tal scopo viene chiamato il cmdlet **Set-CsNetworkRegion**, passando un'identità EMEA. Viene quindi specificato il parametro VideoAlternatePath passando il valore $False. Se si imposta VideoAlternatePath su False si indica che qualora non sia disponibile una larghezza di banda adeguata, la videochiamata non verrà instradata a un percorso alternativo e non verrà completata.

    Set-CsNetworkRegion -Identity EMEA -VideoAlternatePath $False

## ESEMPIO 3

Con l'esempio 3 si assegna all'area di rete Asia lo stesso set di impostazioni di percorso alternativo che è stato impostato per l'area NorthAmerica. La prima riga di questo esempio consente di recuperare un'istanza dell'area di rete NorthAmerica e di assegnarla alla variabile $a. Con la seconda riga si recupera il contenuto della proprietà BWAlternatePaths o dell'area NorthAmerica, memorizzata nella variabile $a: $a.BWAlternatePaths. Si otterrà una raccolta di tutte le impostazioni di percorso alternativo nell'area NorthAmerica.

L'operazione successiva consiste nell'inviare tramite pipe tale raccolta di impostazioni alla funzione foreach, che esegue ciclicamente la raccolta, un elemento per volta, eseguendo le azioni indicate nelle seguenti parentesi graffe. In questo caso l'azione consiste nel chiamare il cmdlet **Set-CsNetworkRegion** con l'identità Asia per impostare le proprietà dell'area Asia. Il parametro successivo è BWAlternatePaths. A questo parametro viene passato il valore @{add=$\_}. La variabile $\_ rappresenta l'elemento corrente nella raccolta, che in questo caso corrisponde al percorso alternativo corrente. La parte @{add=} del valore aggiunge tale elemento alla raccolta di BWAlternatePaths per l'area Asia.

    $a = Get-CsNetworkRegion -Identity NorthAmerica
    $a.BWAlternatePaths | foreach {Set-CsNetworkRegion -Identity Asia -BWAlternatePaths @{add=$_}}

## Descrizione dettagliata

Un'area di rete collega varie parti di una rete dislocate su diverse aree geografiche. Ogni area di rete deve essere associata a un sito centrale. Il sito centrale è il sito del data center in cui è in esecuzione il servizio dei criteri della larghezza di banda Controllo di ammissione di chiamata (CAC). Utilizzare questo cmdlet per modificare un'area di rete esistente, incluse le impostazioni che determinano se sono consentiti percorsi alternativi per le connessioni audio e video e che associano i siti nell'area a una configurazione di bypass multimediale.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsNetworkRegion** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkRegion\\b"}

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
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Questo parametro determina se le chiamate audio verranno instradate tramite un percorso alternativo se non è disponibile una larghezza di banda adeguata nel percorso principale.</p>
<p>Questo parametro popola la proprietà BWAlternatePaths. Il valore fornito a questo parametro è memorizzato nella proprietà AlternatePath per l'elemento percorso alternativo con un valore Audio per BWPolicyModality.</p>
<p>Se si fornisce un valore per questo parametro, non è possibile specificare un valore per il parametro BWAlternatePaths.</p>
<p>Se alcune delle chiamate vengono effettuate via Internet, questo valore deve essere True, indipendentemente dalle impostazioni della larghezza di banda.</p></td>
</tr>
<tr class="even">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Elenco di oggetti in cui è specificato se sono consentiti percorsi di connessione alternativi qualora una richiesta multimediale non possa essere completata con il percorso preferito, ad esempio se sono stati superati i limiti impostati per tale percorso. Gli oggetti percorso alternativo devono essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWAlternatePathType. È possibile creare oggetti di questo tipo chiamando il cmdlet <strong>New-CsNetworkBWAlternatePath</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identificatore univoco globale (GUID) utilizzato per mappare le aree di rete alle impostazioni di bypass multimediale in un Controllo di ammissione di chiamata o in una configurazione di rete E9-1-1 (Enhanced 9-1-1). Utilizzare questo valore BypassID nella chiamata al cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>.</p>
<p>Questo parametro può essere generato automaticamente quando l'area è stata creata chiamando il cmdlet <strong>New-CsNetworkRegion</strong>. Non è consigliabile modificare questo valore. Se tuttavia si specifica un valore, deve avere il formato di un GUID, ad esempio 3b24a047-dce6-48b2-9f20-9fbff17ed62a. Verrà visualizzato un messaggio in cui si chiede di confermare di voler effettivamente impostare manualmente questo valore.</p></td>
</tr>
<tr class="even">
<td><p><em>CentralSite</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il sito centrale che esegue il servizio dei criteri della larghezza di banda. Per poter utilizzare Controllo di ammissione di chiamata, è necessario che questo servizio sia abilitato. Questo servizio viene eseguito sul Front End Server o sul server Standard Edition.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Stringa che descrive l'area. Questo parametro può essere utilizzato per fornire una descrizione più dettagliata dello scopo a cui è destinata l'area rispetto a quella che può essere fornita dalla sola identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco dell'area di rete da modificare. L'identità sarà rappresentata da una stringa che identifica in modo univoco tale area.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSObject</p></td>
<td><p>Riferimento a un oggetto area di rete. Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType e può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkRegion</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Questo parametro determina se le chiamate video verranno instradate tramite un percorso alternativo qualora non sia disponibile una larghezza di banda adeguata nel percorso primario.</p>
<p>Questo parametro popola la proprietà BWAlternatePaths. Il valore fornito a questo parametro è memorizzato nella proprietà AlternatePath per l'elemento percorso alternativo con un valore Video per BWPolicyModality.</p>
<p>Se si fornisce un valore per questo parametro, non è possibile specificare un valore per il parametro BWAlternatePaths.</p>
<p>Se alcune delle chiamate vengono effettuate via Internet, questo valore deve essere True, indipendentemente dalle impostazioni della larghezza di banda.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType. Accetta l'invio tramite pipe di oggetti dell'area di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Modifica un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

