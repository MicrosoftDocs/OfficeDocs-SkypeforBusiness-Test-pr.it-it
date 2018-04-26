---
title: Set-CsCertificate
TOCTitle: Set-CsCertificate
ms:assetid: 6da0be05-b257-4258-9d6d-7ddf283f1038
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398518(v=OCS.15)
ms:contentKeyID: 49300903
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di assegnare un certificato a un ruolo del server o a un server Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsCertificate -Reference <CertificateReference> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCertificate -Identity <XdsIdentity> -Path <String> -Type <CertType[]> [-Password <String>] <COMMON PARAMETERS>

    Set-CsCertificate -Thumbprint <String> -Type <CertType[]> [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di assegnare il certificato con Thumbprint B142918E463981A76503828BB1278391B716280987B al ruolo WebServicesExternal sul computer locale.

    Set-CsCertificate -Type WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## ESEMPIO 2

Nell'esempio 2 viene assegnato il certificato con Thumbprint B142918E463981A76503828BB1278391B716280987B a tre diversi ruoli nel computer locale: Default, WebServicesInternal e WebServicesExternal.

    Set-CsCertificate -Type Default, WebServicesInternal, WebServicesExternal -Thumbprint "B142918E463981A76503828BB1278391B716280987B"

## Descrizione dettagliata

In Lync Server i certificati vengono utilizzati come mezzo per verificare le identità di server e ruoli del server. Un server perimetrale (server perimetrale) ad esempio si basa sui certificati per verificare che il computer con cui sta comunicando sia realmente un Front End Server e viceversa. Per implementare completamente Lync Server, è necessario che ai ruoli del server appropriati siano assegnati i certificati appropriati.

Il cmdlet **Set-CsCertificate** consente agli amministratori di assegnare un certificato ad un server o ruolo del server. Si noti che è possibile assegnare solo i certificati già configurati per l'utilizzo con Lync Server. Per identificare i certificati disponibili per l'assegnazione, utilizzare il cmdlet **Get-CsCertificate**.

Utenti autorizzati a utilizzare questo cmdlet: È necessario essere amministratori locali per poter utilizzare localmente il cmdlet **Set-CsCertificate**. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCertificate"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Se impostato su Global, consente al certificato di funzionare nell'ambito globale. I certificati globali verranno copiati e distribuiti automaticamente ai computer appropriati.</p></td>
</tr>
<tr class="even">
<td><p><em>Path</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file di certificato PFX.</p></td>
</tr>
<tr class="odd">
<td><p><em>Reference</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertificateReference</p></td>
<td><p>Riferimento oggetto ad un certificato configurato per l'utilizzo con Lync Server. Il comando seguente restituisce un riferimento oggetto (la variabile $x) che rappresenta un certificato con l'identificazione personale (Thumbprint) B142918E463981A76503828BB1278391B716280987B:</p>
<p>$x = Get-CsCertificate | Where-Object {$_.Thumbprint –eq &quot;B142918E463981A76503828BB1278391B716280987B&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco del certificato. L'identificazione personale (Thumbprint) di un certificato è simile a quella seguente: B142918E463981A76503828BB1278391B716280987B.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo di certificato da assegnare. Di seguito sono elencati alcuni, non tutti i tipi di certificati:</p>
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
<p>Ad esempio, con questa sintassi si assegna il certificato Default: -Type Default.</p>
<p>È possibile specificare più tipi in un singolo comando separando i tipi di certificato con virgole:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EffectiveDate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data e ora in cui è possibile iniziare a utilizzare il certificato. Per configurare ad esempio un certificato in modo che inizi a essere utilizzato alle 8.00 del 31 luglio 2012, utilizzare la sintassi seguente in un server in cui viene utilizzato l'inglese (Stati Uniti) come impostazione del paese e della lingua:</p>
<p>-EffectiveTime &quot;7/31/2012 8:00 AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Password</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Password del certificato.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di registrare informazioni dettagliate sulle procedure eseguite dal cmdlet <strong>Set-CsCertificate</strong>. Il valore del parametro deve essere il percorso completo del file HTML da generare, ad esempio: -Report C:\Logs\Certificates.html. Se il file specificato esiste già, verrà automaticamente sovrascritto con le nuove informazioni.</p></td>
</tr>
<tr class="odd">
<td><p><em>Roll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di aggiornare nella data e nell'ora indicate dal parametro EffectiveDate il certificato specificato. In questo modo è possibile specificare la data e l'ora in cui il nuovo certificato diventerà il certificato principale. Si noti che il comando avrà esito negativo se si specifica il parametro Roll senza includere il parametro EffectiveDate.</p></td>
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

Microsoft.Rtc.Management.Deployment.CertificateReference

## Tipi restituiti

Il cmdlet **Set-CsCertificate** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)

