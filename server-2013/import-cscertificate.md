---
title: Import-CsCertificate
TOCTitle: Import-CsCertificate
ms:assetid: 87bdafce-f4b9-4c44-ad8f-86c2deb680a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398688(v=OCS.15)
ms:contentKeyID: 49301220
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsCertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa un certificato da utilizzare con Lync Server. Se il certificato non viene acquisito mediante il cmdlet **Request-CsCertificate**, è necessario importarlo prima di poterlo assegnare a un ruolo del server di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CsCertificate -Identity <XdsIdentity> -Type <CertType[]> <COMMON PARAMETERS>

    Import-CsCertificate [-PrivateKeyExportable <$true | $false>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -Path <String> [-Confirm [<SwitchParameter>]] [-EffectiveDate <DateTime>] [-Force <SwitchParameter>] [-Password <String>] [-Report <String>] [-Roll <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 importa il certificato C:\\Certificates\\WebServer.pfx. Al completamento del comando, il certificato diventa disponibile per l'assegnazione a un ruolo del server.

    Import-CsCertificate -Path "C:\Certificates\WebServer.pfx" -PrivateKeyExportable $True

## Descrizione dettagliata

Lync Server utilizza i certificati come mezzo per verificare le identità di server e ruoli del server. Ad esempio, un server perimetrale (server perimetrale) utilizza i certificati per verificare che il computer con cui sta comunicando sia realmente un Front End Server e viceversa. Per implementare completamente Lync Server, è necessario assegnare i certificati appropriati ai ruoli del server appropriati.

Per poter assegnare i certificati a un ruolo di Lync Server, è necessario che i certificati siano noti a Lync Server. Il cmdlet **Request-CsCertificate** consente di effettuare richieste online e offline di nuovi certificati. Se viene effettuata una richiesta online, il certificato verrà automaticamente scaricato e salvato nell'archivio certificati locale e diventerà immediatamente disponibile per l'utilizzo da parte di Lync Server. Se viene effettuata una richiesta offline, si riceverà un file di certificato. Sarà quindi possibile utilizzare il cmdlet **Import-CsCertificate** per importare il certificato, affinché sia disponibile per l'assegnazione a un ruolo del server di Lync Server.

Utenti che possono eseguire questo cmdlet: il cmdlet **Import-CsCertificate** può essere eseguito in locale solo dagli amministratori locali. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsCertificate"}

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
<td><p>Percorso completo del file di certificato da importare. Ad esempio: -Path &quot;C:\Certificates\WebServer.cer&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Type</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo di certificato richiesto. Di seguito sono elencati alcuni tipi di certificati:</p>
<p>* AccessEdgeExternal</p>
<p>* AudioVideoAuthentication</p>
<p>* DataEdgeExternal</p>
<p>* Default</p>
<p>* External</p>
<p>* Internal</p>
<p>* iPadAPNService</p>
<p></p>
<p>* iPhoneAPNService</p>
<p>* LogRetentionService</p>
<p>* MPNService</p>
<p>* OAuthTokenIssuer</p>
<p>* PICWebService</p>
<p>* ProvisionService</p>
<p>* SMPDNSWebService</p>
<p>* TenantAdmin</p>
<p>* UpgradeEngineService</p>
<p>* WebServicesExternal</p>
<p>* WebServicesInternal</p>
<p>* WsFedTokenTransfer</p>
<p>* XMPPServer</p></td>
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
<td><p>Password associata al file di certificato.</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateKeyExportable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se l'impostazione è True, consente di garantire che la parte relativa alla chiave privata del certificato possa essere letta dall'account Servizio di rete.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\Certificates.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Roll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di aggiornare nella data e nell'ora indicate dal parametro EffectiveDate il certificato specificato. In questo modo è possibile specificare la data e l'ora in cui il nuovo certificato diventerà il certificato principale. Si noti che il comando avrà esito negativo se si specifica il parametro Roll senza includere il parametro EffectiveDate.</p></td>
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

Nessuno. Il cmdlet **Import-CsCertificate** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsCertificate](get-cscertificate.md)  
[Remove-CsCertificate](remove-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

