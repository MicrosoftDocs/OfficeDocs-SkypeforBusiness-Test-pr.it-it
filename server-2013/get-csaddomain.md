---
title: Get-CsAdDomain
TOCTitle: Get-CsAdDomain
ms:assetid: 64554035-3ba5-4aa7-b5d3-91277f107275
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398453(v=OCS.15)
ms:contentKeyID: 49300786
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni che indicano se Servizi di dominio Active Directory è stato configurato correttamente per consentire l'installazione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAdDomain [-Domain <Fqdn>] [-DomainController <Fqdn>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni sullo stato corrente del dominio Active Directory locale. Se le impostazioni del dominio in uso sono aggiornate e il dominio è pronto per ospitare Lync Server, verrà restituito il valore LC\_DOMAIN\_SETTINGS\_STATE\_READY.

    Get-CsAdDomain

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce lo stato corrente di un dominio specifico: fabrikam.com. In un ambiente multidominio è possibile restituire informazioni relative a un determinato dominio includendo il parametro Domain.

    Get-CsAdDomain -Domain "fabrikam.com" 

## ESEMPIO 3

Nell'esempio 3 viene recuperato lo stato corrente del dominio Active Directory in uso e vengono inoltre scritte le informazioni relative allo stato in un file denominato C:\\Logs\\DomainReport.html. In questo file sono descritti in modo dettagliato i passaggi eseguiti dal cmdlet **Get-CsAdDomain** per determinare lo stato di conformità del dominio. Tra questi passaggi sono incluse attività quali la verifica della presenza di gruppi Active Directory e il controllo delle impostazioni delle autorizzazioni in diversi contenitori di Active Directory.

    Get-CsAdDomain -Report "C:\Logs\DomainReport.html"

## Descrizione dettagliata

Prima dell'installazione di Lync Server, è necessario preparare correttamente il dominio. Questo processo include l'estensione dello schema di Active Directory per consentire l'aggiunta di attributi specifici di Lync Server, nonché l'assegnazione delle voci di controllo di accesso necessarie ai gruppi universali utilizzati per la gestione e l'utilizzo di Lync Server. Il cmdlet **Get-CsAdDomain** restituisce un singolo valore che indica se Lync Server può essere installato in un dominio. Se il cmdlet **Get-CsAdDomain** restituisce il valore LC\_DOMAINSETTINGS\_STATE\_READY, è possibile installare Lync Server nel dominio specificato. Se invece il cmdlet restituisce LC\_DOMAINSETTINGS\_STATE\_NOT\_READY, è necessario preparare il dominio nel modo corretto prima di tentare l'installazione di Lync Server.

Durante l'Installazione guidata viene eseguito il cmdlet **Get-CsAdDomain**. Se tramite la procedura guidata viene determinato che il dominio non è stato preparato correttamente, viene visualizzato un messaggio di errore e l'installazione si arresta. È tuttavia possibile eseguire il cmdlet **Get-CsAdDomain** indipendentemente dall'installazione guidata per verificare lo stato del dominio prima di tentare l'installazione di Lync Server.

Il cmdlet **Get-CsAdDomain** ha la stessa funzione del comando Microsoft Office Communications Server 2007 R2 seguente:

Lcscmd.exe /domain /action:CheckDomainPrepState

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, possono eseguire il cmdlet **Get-CsAdDomain** tutti gli utenti che dispongono di autorizzazioni di lettura per Active Directory. Tutti i membri di un dominio in genere dispongono di questa autorizzazione.

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdDomain"}

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
<td><p><em>Domain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio da controllare, ad esempio: -Domain &quot;litwareinc.com&quot;. Se il parametro non viene specificato, verrà controllato il dominio locale.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome di dominio completo (FQDN) del controller di dominio da utilizzare quando si esegue il cmdlet <strong>Get-CsAdDomain</strong>. Se non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Get-CsAdDomain</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome FQDN di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema in Active Directory, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, è possibile utilizzare qualsiasi dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\DomainPrep.html&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsAdDomain** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsAdDomain** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deployment.LcDomainSettingsState.

## Vedere anche

#### Ulteriori risorse

[Disable-CsAdDomain](disable-csaddomain.md)  
[Enable-CsAdDomain](enable-csaddomain.md)

