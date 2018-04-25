---
title: Get-CsCertificate
TOCTitle: Get-CsCertificate
ms:assetid: 15b8f019-1d00-4389-9abe-18deb8cbf2ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398227(v=OCS.15)
ms:contentKeyID: 49299787
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsCertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui certificati presenti nei computer locali e configurati per l'utilizzo con Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsCertificate [-Identity <XdsIdentity>] [-Report <String>] [-Type <CertType[]>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce le informazioni sui certificati attualmente assegnati ai componenti di Lync Server. A tale scopo, viene chiamato il cmdlet **Get-CsCertificate** senza alcun parametro aggiuntivo.

    Get-CsCertificate

## ESEMPIO 2

Nell'esempio 2 vengono recuperati tutti i certificati di Lync Server utilizzati per i servizi Web interni. Per ottenere questo risultato, viene incluso il parametro Type insieme al valore WebServicesInternal.

    Get-CsCertificate -Type WebServicesInternal

## ESEMPIO 3

Nell'esempio 3 vengono restituiti tutti i certificati di Lync Server che scadono prima del 1° settembre 2012. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsCertificate** per restituire una raccolta di tutti i certificati di Lync Server attualmente utilizzati. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i certificati che scadono prima del 1° settembre 2012. La data specificata in questo esempio (9/1/2012) utilizza il formato inglese U.S. per i valori di data e ora. La data deve essere specificata utilizzando il formato compatibile con le proprie opzioni internazionali e della lingua.

    Get-CsCertificate | Where-Object {$_.NotAfter -lt "9/1/2012"}

## ESEMPIO 4

Nell'esempio 4 vengono restituite le informazioni su tutti i certificati di Lync Server emessi dall'autorità di certificazione (CA) MyCa. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsCertificate** senza alcun parametro per restituire una raccolta di tutti i certificati attualmente in uso. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti i certificati in cui la proprietà Issuer è uguale a (-eq) "Cn=MyCa".

    Get-CsCertificate | Where-Object {$_.Issuer -eq "Cn=MyCa"}

## ESEMPIO 5

Il comando riportato nell'esempio 5 restituisce tutti i certificati di Lync Server in cui la proprietà Subject è stata impostata su atl-cs-001.litwareinc.com. A tale scopo, viene utilizzato il cmdlet **Get-CsCertificate** per restituire una raccolta di tutti i certificati di Lync Server, che viene quindi inviata tramite pipe al cmdlet **Where-Object**. A sua volta, il cmdlet **Where-Object** seleziona solo i certificati in cui la proprietà Subject è uguale a "CN=atl-cs-001.litwareinc.com".

    Get-CsCertificate | Where-Object {$_.Subject -eq "CN=atl-cs-001.litwareinc.com"}

## Descrizione dettagliata

In Lync Server i certificati vengono utilizzati come mezzo per verificare le identità di server e ruoli del server. Un server perimetrale (server perimetrale) ad esempio si basa sui certificati per verificare che il computer con cui sta comunicando sia realmente un Front End Server e viceversa. Per implementare completamente Lync Server, è necessario che ai ruoli del server appropriati siano assegnati i certificati appropriati.

Il cmdlet **Get-CsCertificate** consente di recuperare informazioni dettagliate sui certificati configurati per l'utilizzo con Lync Server. Si noti che questo cmdlet restituisce informazioni solo sui certificati di Lync Server. Se un certificato non è stato configurato per essere utilizzato con Lync Server (tramite il cmdlet **Set-CsCertificate**), non verrà restituito quando si esegue il cmdlet **Get-CsCertificate**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsCertificate** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins.

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
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Consente di recuperare i certificati configurati nell'ambito globale (i certificati globali vengono copiati e distribuiti nei computer appropriati). Utilizzare la sintassi seguente per restituire informazioni sui certificati globali:</p>
<p>Get-CsCertificate –Identity &quot;global&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di registrare informazioni dettagliate sulle procedure eseguite dal cmdlet <strong>Get-CsCertificate</strong>. Il valore del parametro deve essere il percorso completo del file HTML che verrà generato, ad esempio -Report C:\Logs\Certificates.html. Se il file specificato esiste già, verrà automaticamente sovrascritto con le nuove informazioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo di certificato richiesto. Di seguito sono elencati alcuni, non tutti i tipi di certificati:</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>iPhoneAPNService</p>
<p>iPadAPNService</p>
<p>MPNService</p>
<p>PICWebService (solo Microsoft Lync Online 2010)</p>
<p>ProvisionService (solo Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>Ad esempio, questa sintassi restituisce informazioni relative al certificato Default: -Type Default.</p>
<p>È possibile specificare più tipi in un singolo comando separando i tipi di certificato con virgole:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsCertificate** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsCertificate** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deployment.CertificateReference.

## Vedere anche

#### Ulteriori risorse

[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

