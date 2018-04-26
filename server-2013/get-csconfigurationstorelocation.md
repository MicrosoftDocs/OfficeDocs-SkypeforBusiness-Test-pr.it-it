---
title: Get-CsConfigurationStoreLocation
TOCTitle: Get-CsConfigurationStoreLocation
ms:assetid: abfda147-02fa-46a5-a988-d83daf4cc455
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412814(v=OCS.15)
ms:contentKeyID: 49301632
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConfigurationStoreLocation

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce la posizione del punto di controllo del servizio Active Directory per l'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsConfigurationStoreLocation [-GlobalSettingsDomainController <Fqdn>] [-Report <String>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce il percorso di SQL Server al computer o al pool che ospita l'archivio di gestione centrale.

    Get-CsConfigurationStoreLocation

## ESEMPIO 2

L'esempio 2 è una variante del comando riportato nell'esempio 1. In questo caso tuttavia viene incluso il parametro Report per specificare un percorso per il report generato quando si esegue il cmdlet **Get-CsConfigurationStoreLocation**.

    Get-CsConfigurationStoreLocation -Report "C:\Logs\ConfigurationStore.html"

## Descrizione dettagliata

In Servizi di dominio Active Directory vengono utilizzati punti di controllo del servizio per consentire ai computer di individuare i servizi. Quando ad esempio si installa Lync Server, viene creato un punto di controllo del servizio che fornisce informazioni sulla posizione per l'archivio di gestione centrale utilizzato per la gestione dei dati di Lync Server. I computer che devono accedere al database si connettono ad Active Directory e utilizzano le informazioni incluse nel punto di controllo del servizio per individuare il computer appropriato e l'istanza di SQL Server corretta.

Il cmdlet **Get-CsConfigurationStoreLocation** viene utilizzato per restituire il percorso di SQL Server (ad esempio atl-sql-001.litwareinc.com/rtc) al computer che esegue l'archivio di gestione centrale.

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
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema in Active Directory, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, è possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet, ad esempio -Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsConfigurationStoreLocation** non accetta input tramite pipeline.

## Tipi restituiti

Stringa. Il cmdlet **Get-CsConfigurationStoreLocation** restituisce la posizione dell'archivio di configurazione.

## Vedere anche

#### Ulteriori risorse

[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

