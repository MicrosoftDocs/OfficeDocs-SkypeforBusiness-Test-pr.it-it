---
title: Move-CsApplicationEndpoint
TOCTitle: Move-CsApplicationEndpoint
ms:assetid: 0f5a5b7a-aca5-4672-b712-d47683e28caf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398188(v=OCS.15)
ms:contentKeyID: 49299694
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsApplicationEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Sposta un endpoint in un altro pool di registrazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsApplicationEndpoint -Identity <UserIdParameter> -TargetApplicationPool <Fqdn> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-IgnoreBackendStoreException <SwitchParameter>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio l'oggetto contatto endpoint applicazione con indirizzo SIP endpoint1@litwareinc.com viene spostato nel pool di registrazione attendibile TrustPoolA.litwareinc.com. Utilizzare questo comando per aggiornare un'applicazione da UCMA 2.0 a Lync Server dopo la coesistenza.

    Move-CsApplicationEndpoint -Identity sip:endpoint1@litwareinc.com -TargetApplicationPool TrustPoolA.litwareinc.com

## ESEMPIO 2

In questo esempio l'oggetto contatto endpoint applicazione con indirizzo SIP endpoint2@litwareinc.com viene spostato nel pool di registrazione attendibile TrustPoolA.litwareinc.com. In questo caso, a differenza di quanto avviene nell'esempio 1, il comando include il parametro Force. Utilizzare questo comando per eseguire la migrazione sul posto di un'applicazione UCMA 2.0 o la distribuzione diretta di un'applicazione UCMA 2.0 in una distribuzione pura di Lync Server. Questa operazione aggiornerà un oggetto esistente in Active Directory con gli attributi necessari in modo che il routing possa essere eseguito tramite il servizio di registrazione di Lync Server.

    Move-CsApplicationEndpoint -Identity sip:endpoint2@litwareinc.com -TargetApplicationPool TrustPoolA.litwareinc.com -Force

## Descrizione dettagliata

Questo cmdlet sposta un oggetto contatto endpoint esistente in Servizi di dominio Active Directory da un pool di applicazioni di Microsoft Office Communications Server 2007 R2 a un pool di applicazioni di Lync Server oppure da un pool di applicazioni di Lync Server a un altro. L'applicazione associata all'endpoint specificato deve esistere nel pool di destinazione. Per stabilire quale applicazione è associata all'endpoint, eseguire il cmdlet **Get-CsTrustedApplicationEndpoint** o il cmdlet **Get-CsDialInConferencingAccessNumber**.

Questo cmdlet viene utilizzato inoltre per aggiornare le proprietà dell'oggetto contatto di Active Directory quando un'applicazione distribuita in Office Communications Server 2007 R2 viene ridistribuita in Lync Server. Si noti che in questo caso il pool di applicazioni di origine e di destinazione sarà lo stesso. Se inoltre si distribuisce direttamente in Lync Server un'applicazione originariamente sviluppata per Office Communications Server 2007 R2, questo cmdlet deve essere utilizzato con il flag Force per aggiornare le proprietà dell'oggetto contatto di Active Directory.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Move-CsApplicationEndpoint** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsApplicationEndpoint"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'indirizzo SIP o il nome distinto del contatto endpoint da spostare.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetApplicationPool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo (FQDN) del pool di destinazione dell'endpoint. Il pool di destinazione deve dipendere da un servizio di registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare un controller di dominio. Se non è specificato alcun controller di dominio, viene utilizzato il primo disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Questo flag è necessario se si sta spostando un oggetto contatto Microsoft Unified Communications Managed API (UCMA) 2.0 nello stesso pool, ma in una distribuzione di Lync Server. In questo modo, il routing dovrà essere eseguito tramite il servizio di registrazione di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>IgnoreBackendStoreException</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro indica al computer di ignorare gli eventuali errori che possono verificarsi con il database back-end e di tentare comunque di spostare l'endpoint dell'applicazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, viene restituito l'oggetto endpoint dell'applicazione dopo che l'oggetto è stato spostato.</p></td>
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

Stringa. Accetta una stringa inviata tramite pipeline che rappresenta l'identità dell'endpoint applicazione.

## Tipi restituiti

Se viene utilizzato con il parametro PassThru, questo cmdlet restituisce un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsApplicationEndpoint](get-csapplicationendpoint.md)

