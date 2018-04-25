---
title: New-CsNetworkRegion
TOCTitle: New-CsNetworkRegion
ms:assetid: 33a8efed-23d3-4a03-bede-80f649eaa7b9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425829(v=OCS.15)
ms:contentKeyID: 49300134
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova area di rete. Le aree di rete rappresentano hub di rete o backbone in una rete aziendale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkRegion -NetworkRegionID <String> <COMMON PARAMETERS>

    New-CsNetworkRegion -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -CentralSite <String> [-AudioAlternatePath <$true | $false>] [-BWAlternatePaths <PSListModifier>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoAlternatePath <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene creata una nuova area di rete denominata NorthAmerica. Il nome dell'area viene specificato come valore del parametro Identity. Viene inoltre specificato un valore per il parametro facoltativo Description, che descrive quest'area come composta da tutte le regioni del Nord America ("All North American Locations"). Infine, il parametro CentralSite riceve un valore corrispondente al nome del sito centrale per quest'area, Redmond-NA-MCS.

    New-CsNetworkRegion -Identity NorthAmerica -Description "All North American Locations" -CentralSite Redmond-NA-MLS

## ESEMPIO 2

Questo esempio crea una nuova area di rete chiamata EMEA che include le impostazioni per un percorso alternativo audio. Per ottenere questo risultato, viene utilizzato il cmdlet **New-CsNetworkRegion** e definita l'identità EMEA. Viene poi assegnato un valore per il parametro obbligatorio CentralSite (in questo esempio, il nome di sito centrale per questa area è Dublin-EU-Site) e specificato il valore $False per il parametro AudioAlternatePath. Impostando AudioAlternatePath su False si indica che, se non è disponibile una larghezza di banda adeguata, le chiamate audio non verranno instradate su un percorso alternativo e non verranno completate.

    New-CsNetworkRegion -Identity EMEA -CentralSite Dublin-EU-Site -AudioAlternatePath $False

## ESEMPIO 3

In questo esempio viene creata la stessa area di rete dell'esempio 2. Tuttavia, in questo caso verrà utilizzato il parametro BWAlternatePaths anziché il parametro AudioAlternatePath per definire le impostazioni del percorso alternativo. Nella prima riga dell'esempio viene utilizzato il cmdlet **New-CsNetworkBWAlternatePath** per creare un nuovo percorso alternativo. Un percorso alternativo ha solo due proprietà: BWPolicyModality, impostata su Audio o Video (in questo esempio, Audio) e AlternatePath, impostata su True o False (in questo esempio, False). Viene assegnato l'output di questo cmdlet, un riferimento all'oggetto percorso alternativo appena creato, alla variabile $a.

Nella riga 2 di questo esempio viene utilizzato questo percorso alternativo appena creato quando si crea una nuova area di rete. Per ottenere questo risultato, viene utilizzato il cmdlet **New-CsNetworkRegion** e definita l'identità EMEA. Viene poi assegnato un valore per il parametro obbligatorio CentralSite (in questo esempio, il nome di sito centrale per questa area è Dublin-EU-Site) e il parametro BWAlternatePaths viene impostato sulla variabile ($a) che contiene il percorso alternativo appena creato.

    $a = New-CsNetworkBWAlternatePath -BWPolicyModality "audio" -AlternatePath $False
    New-CsNetworkRegion -Identity EMEA -CentralSite Dublin-EU-Site -BWAlternatePaths $a

## Descrizione dettagliata

Un'area di rete crea una connessione tra diverse parti di una rete in più aree geografiche. Ogni area di rete deve essere associata a un sito centrale. Il sito centrale è il data center in cui viene eseguito il servizio dei criteri di larghezza di banda per Controllo di ammissione di chiamata (CAC). Utilizzare questo cmdlet per creare una nuova area di rete. I parametri di questo cmdlet consentono di specificare le impostazioni per indicare se è consentito un percorso alternativo tramite Internet per connessioni audio e video e per generare automaticamente il valore del parametro BypassID.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsNetworkRegion** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegion"}

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
<td><p><em>CentralSite</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il sito centrale che esegue il servizio dei criteri della larghezza di banda. Per poter utilizzare Controllo di ammissione di chiamata, è necessario che questo servizio sia abilitato. Questo servizio viene eseguito sul Front End Server o sul server Standard Edition.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per le aree di rete appena create. Le aree di rete vengono create solo nell'ambito globale, per cui questo identificatore non specifica un ambito, ma contiene invece una stringa che costituisce il nome univoco della specifica area.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Questo valore è identico e Identity. Non è possibile specificare un valore sia per Identity sia per NetworkRegionID; il valore immesso per l'uno verrà automaticamente utilizzato anche per l'altro.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioAlternatePath</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Questo parametro determina se le chiamate audio verranno instradate tramite un percorso alternativo se non è disponibile una larghezza di banda adeguata nel percorso principale.</p>
<p>Questo parametro popola la proprietà BWAlternatePaths. Il valore fornito a questo parametro è memorizzato nella proprietà AlternatePath per l'elemento percorso alternativo con un valore Audio per BWPolicyModality.</p>
<p>Se si specifica un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWAlternatePaths.</p>
<p>Valore predefinito: True. Impostare questo parametro su False solo se è necessario disattivare la ripartizione del carico di lavoro in Internet. Se alcune delle chiamate vengono effettuate via Internet, questo valore deve essere True, indipendentemente dalle impostazioni della larghezza di banda.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWAlternatePaths</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Elenco di oggetti in cui è specificato se sono consentiti percorsi di connessione Internet alternativi qualora una richiesta multimediale non possa essere completata con il percorso preferito, ad esempio se sono stati superati i limiti impostati per tale percorso. Gli oggetti percorso alternativo devono essere creati utilizzando il cmdlet <strong>New-CsNetworkBWAlternatePath</strong>.</p>
<p>Se si fornisce un valore per questo parametro non sarà possibile specificare un valore sia per il parametro AudioAlternatePath sia per VideoAlternatePath.</p>
<p>Per impostazione predefinita, i percorsi alternativi per audio e video sono abilitati (AlternatePath = True).</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco globale (GUID). Questo GUID è utilizzato per mappare le aree di rete alle impostazioni di bypass multimediale in un Controllo di ammissione di chiamata o in una configurazione di rete E99-1 (Enhanced 9-1-1). Utilizzare questo valore BypassID nella chiamata al cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>.</p>
<p>Se per questo parametro non si specifica alcun valore, ne verrà generato uno automaticamente. Se si specifica un valore, deve essere nel formato di un GUID, ad esempio 3b24a047-dce6-48b2-9f20-9fbff17ed62a. La generazione automatica è la scelta consigliata. Se si specifica un valore, verrà visualizzato un messaggio in cui si richiede di confermare che si intende specificare un valore anziché consentirne la generazione automatica.</p></td>
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
<td><p>Stringa che descrive l'area. Questo parametro può essere utilizzato per fornire una descrizione più dettagliata dello scopo a cui è destinata l'area rispetto a quella che può essere fornita dalla sola identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche. Ad esempio, se si fornisce un valore per il parametro BypassID, non verrà richiesta nessuna conferma.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoAlternatePath</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Questo parametro determina se le chiamate video verranno instradate tramite un percorso alternativo qualora non sia disponibile una larghezza di banda adeguata nel percorso primario.</p>
<p>Questo parametro popola la proprietà BWAlternatePaths. Il valore fornito a questo parametro è memorizzato nella proprietà AlternatePath per l'elemento percorso alternativo con un valore Video per BWPolicyModality.</p>
<p>Se si fornisce un valore per questo parametro, non è possibile specificare un valore per il parametro BWAlternatePaths.</p>
<p>Valore predefinito: True. Impostare questo parametro su False solo se è necessario disattivare la ripartizione del carico di lavoro in Internet. Se alcune delle chiamate vengono effettuate via Internet, questo valore deve essere True, indipendentemente dalle impostazioni della larghezza di banda.</p></td>
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

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionType.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[New-CsNetworkBWAlternatePath](new-csnetworkbwalternatepath.md)

