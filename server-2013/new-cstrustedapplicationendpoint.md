---
title: New-CsTrustedApplicationEndpoint
TOCTitle: New-CsTrustedApplicationEndpoint
ms:assetid: 78b34ba4-4c31-4f68-9069-3c7e7c162fbf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398594(v=OCS.15)
ms:contentKeyID: 49301048
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsTrustedApplicationEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo contatto endpoint per un'applicazione attendibile. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsTrustedApplicationEndpoint -ApplicationId <String> -TrustedApplicationPoolFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-DisplayName <String>] [-DisplayNumber <String>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrimaryLanguage <String>] [-SecondaryLanguages <MultiValuedProperty>] [-SipAddress <String>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene creato un endpoint applicazione attendibile per l'applicazione con ID tapp1 residente nel pool TrustPool.litwareinc.com. ApplicationID e TrustedApplicationPoolFqdn sono i soli parametri richiesti per creare un endpoint applicazione attendibile. Tuttavia, è importante ricordare che l'assegnazione dei valori a questi due soli parametri consente di generare un indirizzo SIP per il contatto. Per garantire che l'indirizzo SIP sia univoco, l'indirizzo generato automaticamente contiene un identificatore univoco globale (GUID) ed è simile a quello riportato di seguito: sip:RtcApplication-fbf9e2d1-c6aa-45a3-a045-b92d4ef961b2@litwareinc.com. Se si desidera un indirizzo SIP più leggibile, vedere l'esempio 2.

    New-CsTrustedApplicationEndpoint -ApplicationId tapp1 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com

## ESEMPIO 2

L'esempio 2 è identico all'esempio 1 in quanto crea un endpoint applicazione attendibile per l'applicazione con ID tapp1 nel pool TrustPool.litwareinc.com. A differenza dell'esempio 1, è stato incluso un altro parametro nella creazione dell'endpoint, SipAddress. Invece di lasciare che sia il sistema a generare un indirizzo SIP, è stato specificato l'indirizzo endpoint1@litwareinc.com.

    New-CsTrustedApplicationEndpoint -ApplicationId tapp1 -TrustedApplicationPoolFqdn TrustPool.litwareinc.com -SipAddress sip:endpoint1@litwareinc.com

## Descrizione dettagliata

Un endpoint applicazione attendibile è un oggetto contatto di Active Directory che consente il routing delle chiamate verso un'applicazione attendibile. Questo cmdlet consente di creare un nuovo oggetto contatto endpoint in Servizi di dominio Active Directory per un'applicazione specificata.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsTrustedApplicationEndpoint** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsTrustedApplicationEndpoint"}

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
<td><p><em>ApplicationId</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'ID dell'applicazione attendibile per cui deve essere creato il contatto endpoint. Deve esistere un'applicazione con questo ID. È possibile includere solo la parte del nome dell'ID dell'applicazione; non è necessario (ma è possibile) includere le informazioni del prefisso. Ad esempio, se l'ID dell'applicazione è urn:application:TrustedApp1, è sufficiente passare la stringa TrustedApp1 a questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo del pool di applicazioni attendibili associato all'applicazione. Per creare l'endpoint è necessario che l'applicazione sia già associata a questo pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome visualizzato dell'oggetto contatto endpoint.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono del contatto come sarà visualizzato nella Rubrica.</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono del contatto. Deve essere nel formato TEL:&lt;numero&gt;, ad esempio TEL:+14255551212.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce i risultati di questo comando. Con l'esecuzione del cmdlet viene visualizzato l'oggetto appena creato; se si include questo parametro tale output viene ripetuto, pertanto l'uso del parametro si rivela ridondante.</p></td>
</tr>
<tr class="even">
<td><p><em>PrimaryLanguage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>La lingua principale utilizzate per l'applicazione attendibile. La lingua deve essere configurata utilizzando un codice di lingua valido, ad esempio en-US (inglese americano), fr-FR (francese), ecc.</p></td>
</tr>
<tr class="odd">
<td><p><em>SecondaryLanguages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.MultiValuedProperty</p></td>
<td><p>Una raccolta delle lingue utilizzabili per le applicazioni attendibili. I valori devono essere configurati in un elenco separato da virgole di codici di lingua. Ad esempio, la sintassi riportata di seguito consente di impostare il francese canadese e il francese come lingue secondarie: -SecondaryLanguages &quot;fr-CA&quot;,&quot;fr-FR&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un indirizzo SIP per il nuovo oggetto contatto. Se non si include un valore per questo parametro, viene generato automaticamente un indirizzo SIP nel formato sip:RtcApplication-&lt;GUID&gt;.&lt;dominio&gt;, ad esempio sip:RtcApplication-fbf9e2d1-c6aa-45a3-a045-b92d4ef961b2@litwareinc.com. Il dominio sarà il dominio SIP predefinito.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Office 365 per il quale viene creato il nuovo endpoint del pool di applicazioni attendibili. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Vedere anche

#### Ulteriori risorse

[Remove-CsTrustedApplicationEndpoint](remove-cstrustedapplicationendpoint.md)  
[Set-CsTrustedApplicationEndpoint](set-cstrustedapplicationendpoint.md)  
[Get-CsTrustedApplicationEndpoint](get-cstrustedapplicationendpoint.md)

