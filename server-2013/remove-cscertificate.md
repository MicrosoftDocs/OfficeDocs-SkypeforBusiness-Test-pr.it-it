---
title: Remove-CsCertificate
TOCTitle: Remove-CsCertificate
ms:assetid: b7a83a58-9d3f-458a-867e-44466c9817dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412895(v=OCS.15)
ms:contentKeyID: 49301763
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un certificato precedentemente contrassegnato come disponibile per l'utilizzo da parte di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsCertificate -Type <CertType[]> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Identity <XdsIdentity>] [-Previous <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 elimina tutti i certificati WebServicesExternal disponibili per Lync Server. Se uno di questi certificati è attualmente in uso, il cmdlet **Remove-CsCertificate** visualizzerà un messaggio di conferma di rimozione del certificato. Il comando verrà eseguito solo dopo che l'utente avrà risposto al messaggio di richiesta. Per disabilitare la visualizzazione della richiesta di conferma, utilizzare il parametro Force:

Remove-CsCertificate –Type WebServicesExternal -Force

    Remove-CsCertificate -Type WebServicesExternal

## Descrizione dettagliata

In Lync Server i certificati vengono utilizzati come mezzo per verificare le identità di server e ruoli del server. Un server perimetrale (server perimetrale) ad esempio si basa sui certificati per verificare che il computer con cui sta comunicando sia realmente un Front End Server e viceversa. Per implementare completamente Lync Server, è necessario che ai ruoli del server appropriati siano assegnati i certificati appropriati.

Il cmdlet **Remove-CsCertificate** consente di rimuovere i certificati attualmente in uso da parte di Lync Server. Il cmdlet **Remove-CsCertificate** non elimina effettivamente il certificato stesso, ma lo contrassegna come non più disponibile per l'utilizzo da parte di Lync Server. Rimuove inoltre gli eventuali binding del certificato e revoca le autorizzazioni di accesso al certificato, presupponendo che il certificato non sia utilizzato da altri servizi. Il certificato tra l'altro non viene più visualizzato quando si esegue il cmdlet **Get-CsCertificate**.

Per utilizzare nuovamente il certificato con Lync Server, sarà necessario riassegnarlo a Lync Server utilizzando il cmdlet **Set-CsCertificate**.

Se si tenta di rimuovere un certificato attualmente in uso, il cmdlet **Remove-CsCertificate** visualizzerà un messaggio in cui viene chiesto di confermare la rimozione. Il certificato non verrà rimosso se non si fornirà una risposta al messaggio visualizzato. Per disabilitare la visualizzazione del messaggio di conferma ed eliminare un certificato automaticamente, anche se in uso, aggiungere il parametro Force al comando:

Remove-CsCertificate –Type WebServicesExternal -Force

Utenti autorizzati a eseguire il cmdlet: possono eseguire localmente il cmdlet **Remove-CsCertificate** solo gli amministratori locali e i membri del dominio. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCertificate"}

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
<td><p><em>Type</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.CertType[]</p></td>
<td><p>Tipo di certificato da eliminare. I tipi di certificato includono (in via esemplificativa):</p>
<p>AccessEdgeExternal</p>
<p>AudioVideoAuthentication</p>
<p>DataEdgeExternal</p>
<p>Default</p>
<p>External</p>
<p>Internal</p>
<p>PICWebService (solo Microsoft Lync Online 2010)</p>
<p>ProvisionService (solo Microsoft Lync Online 2010)</p>
<p>WebServicesExternal</p>
<p>WebServicesInternal</p>
<p>WsFedTokenTransfer</p>
<p>La seguenti sintassi ad esempio elimina il certificato Default: -Type Default.</p>
<p>È possibile eliminare più tipi di certificati con un unico comando separandoli con le virgole:</p>
<p>-Type Internal,External,Default</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Disabilita la visualizzazione della richiesta di conferma che viene generalmente visualizzata quando si tenta di eliminare un certificato attualmente in uso.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Se impostato su Global, questo parametro rimuove il certificato dall'ambito globale. Se invece non si specifica questo parametro, i certificati vengono rimossi dal computer locale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Previous</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro rimuove il certificato precedentemente assegnato anziché quello corrente.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di registrare informazioni dettagliate sulle procedure eseguite dal cmdlet <strong>Remove-CsCertificate</strong>. Il valore del parametro deve essere il percorso completo del file HTML da generare, ad esempio: -Report C:\Logs\Certificates.html. Se il file specificato esiste già, verrà automaticamente sovrascritto con le nuove informazioni.</p></td>
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

Nessuno. Il cmdlet Remove-CsCertificate non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsCertificate** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.Deployment.CertificateReference.

## Vedere anche

#### Ulteriori risorse

[Get-CsCertificate](get-cscertificate.md)  
[Import-CsCertificate](import-cscertificate.md)  
[Request-CsCertificate](request-cscertificate.md)  
[Set-CsCertificate](set-cscertificate.md)

