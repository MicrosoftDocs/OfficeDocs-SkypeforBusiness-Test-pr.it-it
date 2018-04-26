---
title: New-CsTrustedApplicationPool
TOCTitle: New-CsTrustedApplicationPool
ms:assetid: 30117225-d82b-494b-8bc2-da5d539bdd6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425804(v=OCS.15)
ms:contentKeyID: 49300074
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplicationPool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo pool in cui saranno contenuti i computer che ospitano le applicazioni attendibili. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsTrustedApplicationPool -Identity <XdsGlobalRelativeIdentity> [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-ComputerFqdn <Fqdn>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-OutboundOnly <$true | $false>] [-Registrar <String>] [-RequiresReplication <$true | $false>] [-Site <String>] [-ThrottleAsServer <$true | $false>] [-TreatAsAuthenticated <$true | $false>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene creato un nuovo pool con FQDN TrustPool.litwareinc.com. Per specificare il nuovo nome FQDN, viene utilizzato il parametro Identity. Viene utilizzato il parametro Registrar con il valore pool0.litwareinc.com, per associare il nuovo pool con servizio di registrazione a tale FQDN. Infine, viene utilizzato il parametro Site con valore Redmond, per indicare che il pool fa parte del sito Redmond.

Si noti che il valore Site corrisponde all'ID del sito, che può essere recuperato chiamando il cmdlet **Get-CsSite**. L'identità del sito tuttavia verrà archiviata con il nuovo pool di applicazioni attendibili. Se ad esempio il valore Identity di un sito è site:Redmond1 e il valore SiteId è NA, sarà necessario utilizzare NA come valore del parametro Site nella chiamata al cmdlet **New-CsTrustedApplicationPool**. Se però in un secondo momento si desidera trovare tutti i pool di applicazioni attendibili per il sito NA, sarà necessario utilizzare il valore Identity nella clausola where, come indicato di seguito:

Get-CsTrustedApplicationPool | Where-Object {$\_.SiteId –eq "site:Redmond1"}

    New-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com -Registrar pool0.litwareinc.com -Site Redmond

## ESEMPIO 2

l'esempio 2 è identico all'esempio 1, con la differenza che anziché specificare un nome di dominio completo (FQDN) per il servizio di registrazione, viene utilizzato l'ID servizio Registrar:redmond.litwareinc.com. È stato specificato inoltre un valore per il parametro ComputerFqdn. Quando si crea un pool, all'interno del pool viene creato anche un computer. Per impostazione predefinita al computer viene assegnato lo stesso FQDN del pool. Per il computer di questo pool è stato specificato un FQDN differente, AppServer.litwareinc.com.

    New-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com -Registrar Registrar:redmond.litwareinc.com -Site Redmond -ComputerFqdn AppServer.litwareinc.com

## Descrizione dettagliata

È consigliabile che i computer che eseguono applicazioni attendibili all'interno di una distribuzione di Lync Server vengano aggiunti a un pool distinto, destinato unicamente a questo tipo di applicazioni. È tuttavia possibile aggiungere i computer con applicazioni attendibili a un pool esistente già utilizzato anche per altri scopi. Se il pool è già presente nella topologia, questo cmdlet crea il servizio esterno associato a tale pool (con un ruolo del servizio ExternalServer). Se il pool non esiste, questo cmdlet crea il pool e il servizio corrispondente. È possibile visualizzare un elenco di tutti i pool esistenti chiamando il cmdlet **Get-CsPool**.

Se si crea un nuovo pool di applicazioni attendibili, un nuovo servizio esterno, si crea anche un nuovo computer con applicazioni attendibili assegnato a tale pool. Per impostazione predefinita al computer viene assegnato lo stesso nome di dominio completo (FQDN) del pool. Tuttavia, è possibile specificare un proprio valore per il nome FQDN, utilizzando il parametro ComputerFqdn di questo cmdlet. Se si desidera aggiungere più computer al pool, è necessario specificare un valore ComputerFqdn differente rispetto al nome FQDN del pool. Per aggiungere più computer al pool, chiamare il cmdlet **New-CsTrustedApplicationComputer**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsTrustedApplicationPool** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplicationPool"}

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
<td><p>FQDN del nuovo pool. Si noti che, sebbene il valore Identity per la creazione di un pool sia il nome FQDN del pool, il valore che verrà archiviato come Identity per il nuovo pool è un ID servizio del pool che viene generato automaticamente. l'identità immessa qui viene salvata come PoolFqdn.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero di porte disponibili nell'intervallo delle porte per le connessioni di condivisione delle applicazioni.</p>
<p>Valore predefinito: 0</p></td>
</tr>
<tr class="odd">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero della prima porta, nell'intervallo delle porte, disponibile per le connessioni di condivisione delle applicazioni.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero di porte disponibili nell'intervallo delle porte per le connessioni audio.</p>
<p>Valore predefinito: 0</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero della prima porta, nell'intervallo delle porte, disponibile per le connessioni audio.</p></td>
</tr>
<tr class="even">
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Se si crea un pool di applicazioni attendibili, viene creato automaticamente un computer con applicazioni attendibili che fa parte di tale pool. Per impostazione predefinita al computer viene assegnato lo stesso FQDN del pool. Immettere un valore in questo parametro, per specificare un nome FQDN per il computer distinto dall'FQDN del pool. Se si desidera aggiungere più computer al pool, è necessario immettere un valore per questo parametro, differente rispetto al nome FQDN del pool.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundOnly</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Specifica se a un'applicazione attendibile è consentito avviare la connessione a un server del pool. Impostare il valore su True, se si desidera che tutte le connessioni vengano avviate dal server anziché dall'applicazione.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>Registrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>ID servizio o FQDN del servizio di registrazione del pool.</p>
<p>Sebbene questo parametro sia facoltativo, nel caso si tenti di creare un nuovo endpoint applicazioni attendibili tramite il cmdlet <strong>New-CsTrustedApplicationEndpoint</strong> e di assegnarlo a un pool che non dipende da un servizio di registrazione, verrà restituito un messaggio di errore e l'endpoint non verrà creato. Inoltre, non è possibile rimuovere un pool di applicazioni attendibili che non è associato a un servizio Registrar.</p></td>
</tr>
<tr class="odd">
<td><p><em>RequiresReplication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Determina se per il pool è richiesta la replica. Impostare il valore su False, se non è richiesta la replica. Il parametro in genere viene impostato su False per Microsoft Outlook Web Access e per le applicazioni di cui viene eseguito manualmente il provisioning.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>Site</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>ID del sito che ospita il pool. Chiamare il cmdlet <strong>Get-CsSite</strong> per recuperare la proprietà SiteId di un sito. Tenere presente che è necessario utilizzare la proprietà SiteId anziché il valore Identity del sito. Si noti inoltre che il valore SiteId non deve essere preceduto dalla stringa &quot;site:&quot;. È necessario immettere solo il valore SiteId. Benché inoltre si immetta il valore SiteId recuperato dal cmdlet <strong>Get-CsSite</strong>, la proprietà SiteId del nuovo pool di applicazioni attendibili includerà il valore Identity del sito. Se ad esempio il valore SiteId del sito è Main e il valore Identity del sito è site:Redmond1, sarà necessario immettere -Site Main nella chiamata al cmdlet <strong>New-CsTrustedApplicationPool</strong>, ma in una chiamata successiva al cmdlet <strong>Get-CsTrustedApplicationPool</strong> il valore SiteId sarà site:Redmond1.</p>
<p>Se il pool specificato nell'identità esiste già, non è necessario specificare una proprietà Site. Se il pool non esiste, questo parametro è obbligatorio.</p></td>
</tr>
<tr class="odd">
<td><p><em>ThrottleAsServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare il parametro su False per limitare le connessioni fra i server all'interno del pool e le applicazioni attendibili come client. Questa impostazione impone maggiori limitazioni sulla connessione rispetto al valore predefinito True, che limita le connessioni come server. Limitare una connessione significa imporre restrizioni per il numero di transazioni che è possibile eseguire contemporaneamente.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="even">
<td><p><em>TreatAsAuthenticated</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Determina se è richiesta l'autenticazione per le applicazioni attendibili che si collegano ai server presenti nel pool. Impostare questo parametro su False, se si desidera richiedere l'autenticazione delle applicazioni attendibili. Il valore predefinito True consente la connessione delle applicazioni attendibili, benché solo se già autenticate.</p>
<p>Valore predefinito: True</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero di porte disponibili nell'intervallo delle porte per le connessioni video.</p>
<p>Valore predefinito: 0</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero della prima porta, nell'intervallo delle porte, disponibile per le connessioni video.</p></td>
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

Crea un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayExternalServer.

## Vedere anche

#### Ulteriori risorse

[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Set-CsTrustedApplicationPool](set-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)  
[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)  
[Get-CsSite](get-cssite.md)

