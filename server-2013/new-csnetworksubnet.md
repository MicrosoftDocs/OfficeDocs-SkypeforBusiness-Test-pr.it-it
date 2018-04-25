---
title: New-CsNetworkSubnet
TOCTitle: New-CsNetworkSubnet
ms:assetid: 15af44bd-d798-435c-9c27-df47ab475023
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398226(v=OCS.15)
ms:contentKeyID: 49299783
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkSubnet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova subnet di rete. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkSubnet -SubnetID <String> <COMMON PARAMETERS>

    New-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -MaskBits <Int32> [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio dimostra come creare un nuovo oggetto subnet che rappresenta la subnet 172.11.15.0/24. L'identità della subnet è impostata su 172.11.15.0. Questo valore verrà automaticamente assegnato anche al parametro SubnetID. È necessario definire una maschera di bit per la subnet. Per ottenere questo risultato, si specifica un valore (in questo caso 24) per il parametro MaskBits. Infine, per il parametro NetworkSiteID viene specificato l'ID sito Vancouver in modo da associare la subnet a questo sito.

    New-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 24 -NetworkSiteID Vancouver

## ESEMPIO 2

Nell'Esempio 2 si leggono i dati da un file CSV per creare una serie di subnet. Il file CSV in questo esempio sarà simile al seguente:

Identity, Mask, SiteID

172.11.12.0, 24, Redmond

172.11.13.0, 24, Chicago

172.11.14.0, 25, Vancouver

172.11.15.0, 31, Paris

...

Nell'esempio, si inizia utilizzando il cmdlet **Import-CSV** e specificando il percorso di un file CSV. Il cmdlet legge e memorizza il contenuto del file. Questi contenuti vengono poi inviati tramite pipe alla funzione Foreach. La funzione Foreach esamina il contenuto una riga alla volta. Come risulta evidente dal file di esempio, la prima riga è un elenco di intestazioni che definiscono il resto del contenuto; la funzione Foreach utilizza queste intestazioni per accedere ai file CSV per nome.

Nell'istruzione Foreach, viene utilizzato il cmdlet **New-CsNetworkSubnet**. Mentre la funzione Foreach esamina tutte le singole righe del contenuto del file, la riga in questione viene specificata come valore per i parametri del cmdlet **New-CsNetworkSubnet**. Ad esempio, la prima volta che esamina l'istruzione Foreach, il cmdlet **New-CsNetworkSubnet** crea una subnet con Identity 172.11.12.0: questo è il valore del parametro Identity nella prima riga di valori CSV. Il simbolo $\_ indica il valore corrente nel ciclo Foreach. Viene quindi importato dal file il valore della maschera (24) per il parametro MaskBits e il valore dell'ID sito (Redmond) per il parametro NetworkSiteID.

Questo processo prosegue fino a quando non sono state lette tutte le righe del file e i loro valori non sono stati utilizzati per creare nuove subnet.

    Import-CSV C:\subnet.csv | foreach {New-CsNetworkSubnet -Identity $_.Identity -MaskBits $_.Mask -NetworkSiteID $_.SiteID}

## Descrizione dettagliata

Ciascuna subnet deve essere associata ad un sito di rete per stabilire la località geografica dell'host che appartiene a questa subnet. Utilizzando questo cmdlet, è possibile creare una nuova subnet e (facoltativamente) assegnarla contemporaneamente a un nuovo sito di rete.

Nella maggior parte delle distribuzioni di Lync Server che implementano il servizio Controllo di ammissione di chiamata generalmente sarà presente un numero elevato di subnet. Di conseguenza, spesso è consigliabile utilizzare il cmdlet **New-CsNetworkSubnet** insieme al cmdlet **Import-CSV**. L'abbinamento di questi due cmdlet consente di leggere le impostazioni delle subnet da un file CSV e di creare più subnet contemporaneamente. Per ulteriori informazioni, vedere la sezione Esempi per questo cmdlet.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsNetworkSubnet** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkSubnet"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>L'ID univoco della subnet da creare. Questo valore deve essere il primo indirizzo IP (ad esempio, 174.11.12.0) nell'intervallo di indirizzi IP definito dalla subnet.</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>La maschera di bit da applicare alla subnet da creare.</p>
<p>Valori validi: Da 1 a 32</p></td>
</tr>
<tr class="odd">
<td><p><em>SubnetID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Questo valore è uguale all'identità. È necessario specificare un'identità o un ID della subnet (SubnetID), ma non è possibile specificarli entrambi. Il valore fornito per un parametro verrà automaticamente applicato anche all'altro.</p></td>
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
<td><p>Una descrizione della subnet da creare.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'ID del sito a cui appartiene la subnet. È possibile ottenere gli ID dei siti per la propria distribuzione utilizzando il cmdlet <strong>Get-CsNetworkSite</strong>.</p></td>
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

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

