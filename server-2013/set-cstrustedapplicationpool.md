---
title: Set-CsTrustedApplicationPool
TOCTitle: Set-CsTrustedApplicationPool
ms:assetid: 0f42d12b-d09a-41fd-892f-2b7515a35344
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398187(v=OCS.15)
ms:contentKeyID: 49299698
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrustedApplicationPool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un pool contenente i computer che ospitano applicazioni attendibili. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsTrustedApplicationPool [-Identity <XdsGlobalRelativeIdentity>] [-AppSharingPortCount <UInt16>] [-AppSharingPortStart <UInt16>] [-AudioPortCount <UInt16>] [-AudioPortStart <UInt16>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-OutboundOnly <$true | $false>] [-Registrar <String>] [-RequiresReplication <$true | $false>] [-ThrottleAsServer <$true | $false>] [-TreatAsAuthenticated <$true | $false>] [-VideoPortCount <UInt16>] [-VideoPortStart <UInt16>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio, viene modificato il pool con FQDN TrustPool.litwareinc.com. Viene utilizzato il parametro Identity per specificare il nome FQDN del pool da modificare. In questo esempio viene modificata la proprietà OutboundOnly del pool specificando il valore True ($True) per il parametro OutboundOnly. Il valore predefinito è False.

    Set-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com -OutboundOnly $True

## Descrizione dettagliata

È consigliabile che i computer che eseguono applicazioni attendibili all'interno di una distribuzione di Lync Server vengano aggiunti a un pool distinto, destinato unicamente a questo tipo di applicazioni. È tuttavia possibile aggiungere i computer con applicazioni attendibili a un pool esistente utilizzato anche per altri scopi. Il cmdlet **Set-CsTrustedApplicationPool** modifica le impostazioni di un pool di applicazioni attendibili esistente. Si noti che con questo cmdlet non è possibile modificare i computer associati a un pool. A tale scopo, è necessario utilizzare i cmdlet CsTrustedApplicationComputer.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsTrustedApplicationPool** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrustedApplicationPool"}

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
<td><p><em>AppSharingPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero di porte disponibili per le connessioni di condivisione delle applicazioni nell'intervallo di porte.</p></td>
</tr>
<tr class="even">
<td><p><em>AppSharingPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero della prima porta dell'intervallo di porte disponibili per le connessioni di condivisione delle applicazioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero di porte disponibili per le connessioni audio nell'intervallo di porte.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero della prima porta dell'intervallo di porte disponibili per le connessioni audio.</p></td>
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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome di dominio completo (FQDN) o l'ID servizio del pool del quale si desidera modificare le impostazioni.</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundOnly</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di specificare se un'applicazione attendibile può attivare una connessione a un server del pool. Impostare questo valore su True, se si desidera che tutte le connessioni vengano attivate dal server e non dall'applicazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Registrar</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'ID servizio o FQDN del servizio di registrazione del pool. Si noti che la modifica del servizio di registrazione renderà orfani gli eventuali contatti associati all'applicazione. Questi contatti dovranno essere spostati utilizzando il cmdlet <strong>Move-CsApplicationEndpoint</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>RequiresReplication</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Determina se per il pool è richiesta la replica. Impostare il valore su False, se non è richiesta la replica. Il parametro in genere viene impostato su False per Microsoft Outlook Web Access e per le applicazioni di cui viene eseguito manualmente il provisioning.</p></td>
</tr>
<tr class="odd">
<td><p><em>ThrottleAsServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare questo parametro su False per applicare le limitazioni dei client alle connessioni tra i server del pool e le applicazioni attendibili. In questo caso, le limitazioni delle connessioni sono maggiori rispetto al valore predefinito True, che di fatto applica alle connessioni le limitazioni dei server. Limitare una connessione significa semplicemente imporre delle limitazioni al numero di transazioni che è possibile eseguire contemporaneamente.</p></td>
</tr>
<tr class="even">
<td><p><em>TreatAsAuthenticated</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di stabilire se per le applicazioni affidabili che si connettono ai server del pool è obbligatoria l'autenticazione. Impostare questo parametro su False, se si desidera che le applicazioni attendibili vengano obbligatoriamente autenticate. Il valore predefinito True consente alle applicazioni attendibili di connettersi considerandole già autenticate</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoPortCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero di porte disponibili per le connessioni video nell'intervallo di porte.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoPortStart</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Il numero della prima porta dell'intervallo di porte disponibili per le connessioni video.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.DisplayExternalServer. Accetta input tramite pipeline da oggetti pool applicazione attendibile.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayExternalServer.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)  
[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)

