---
title: New-CsWebTrustedCACertificate
TOCTitle: New-CsWebTrustedCACertificate
ms:assetid: a0a94971-372a-401a-8ae0-9ff649a9c301
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412746(v=OCS.15)
ms:contentKeyID: 49301503
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsWebTrustedCACertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo oggetto ID certificato basato su un certificato di un'Autorità di certificazione (CA) esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsWebTrustedCACertificate -CAStore <TrustedRootCA | IntermediateCA | ThirdPartyRootCA> -Thumbprint <String>

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 crea un nuovo certificato CA attendibile, quindi lo aggiunge alla proprietà TrustedCACerts delle impostazioni di configurazione dei servizi Web del sito Redmond. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsWebTrustedCACertificate** per creare un nuovo certificato CA attendibile. Questo certificato si trova nell'archivio certificati radice attendibili e dispone dell'identificazione personale D543DFF74FEEA425162FD25F342786F1AB453BB3. L'oggetto certificato risultante viene archiviato in una variabile denominata $x.

Dopo aver creato l'oggetto certificato, con il secondo comando riportato nell'esempio tale oggetto viene aggiunto alla proprietà TrustedCACerts. A tale scopo, vengono utilizzati il cmdlet **Set-CsWebServiceConfiguration** e il parametro TrustedCACerts. Il valore del parametro ${Add=$x} indica al cmdlet di aggiungere il certificato archiviato nella variabile $x alla raccolta di certificati CA attendibili.

    $x = New-CsWebTrustedCACertificate -Thumbprint "D543DFF74FEEA425162FD25F342786F1AB453BB3" -CAStore TrustedRootCA
    
    Set-CsWebServiceConfiguration -Identity site:Redmond -TrustedCACerts @{Add=$x}

## Descrizione dettagliata

Le impostazioni di configurazione dei servizi Web vengono utilizzate per agevolare la gestione dei server Web e dei servizi Web di Lync Server. Tra i valori delle proprietà che possono essere gestiti tramite queste impostazioni è inclusa la proprietà TrustedCACerts, che rappresenta una raccolta di Autorità di certificazione considerate attendibili da Lync Phone Edition. I certificati ottenuti da Autorità di certificazione attendibili consentono a questi client di aumentare la sicurezza delle connessioni ai server che eseguono Lync Server. Per aggiungere una nuova CA alla raccolta di Autorità di certificazione attendibili, è necessario aggiungere la catena di certificati di tale CA nell'archivio certificati del computer locale. Dopo avere verificato che la catena di certificati sia stata installata, è possibile utilizzare il cmdlet **New-CsWebTrustedCACertificate** per creare un oggetto ID certificato da aggiungere a una raccolta di impostazioni di configurazione dei servizi Web.

Si noti che l'Autorità di certificazione che firma il certificato del server predefinito utilizzato per l'installazione di Lync Server viene considerato automaticamente attendibile e non deve essere aggiunto alla proprietà TrustedCACerts di una raccolta di impostazioni di configurazione dei servizi Web. In TrustedCACerts devono essere incluse solo le identità di CA che devono essere considerate attendibili oltre alla CA che ha rilasciato il certificato predefinito. Nella maggior parte dei casi la CA che ha rilasciato il certificato predefinito sarà l'unica Autorità di certificazione che deve essere considerata attendibile.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsWebTrustedCACertificate** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsWebTrustedCACertificate"}

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
<td><p><em>CAStore</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Web.CAStore</p></td>
<td><p>Indica il nome dell'archivio certificati (nel computer locale) in cui è archiviato il certificato. I valori validi sono:</p>
<p>TrustedRootCA</p>
<p>IntermediateCA</p>
<p>ThirdPartyRootCA</p></td>
</tr>
<tr class="even">
<td><p><em>Thumbprint</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identificazione digitale del certificato che deve essere considerato attendibile da Lync Phone Edition. È possibile recuperare l'autorità emittente del certificato e i valori per l'identificazione digitale eseguendo il comando seguente:</p>
<p>Get-CsCertificate | Select-Object Issuer, Thumbprint.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsWebTrustedCACertificate** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsWebTrustedCACertificate** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Web.CACertID.

## Vedere anche

#### Ulteriori risorse

[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

