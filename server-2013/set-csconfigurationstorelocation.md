---
title: Set-CsConfigurationStoreLocation
TOCTitle: Set-CsConfigurationStoreLocation
ms:assetid: 1c69a872-8e78-4c78-ba27-f20f04dce59f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398258(v=OCS.15)
ms:contentKeyID: 49299855
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsConfigurationStoreLocation

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Imposta il punto di controllo del servizio Active Directory per l'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsConfigurationStoreLocation -SqlServerFqdn <Fqdn> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-MirrorSqlInstanceName <String>] [-MirrorSqlServerFqdn <Fqdn>] [-Report <String>] [-SkipLookup <SwitchParameter>] [-SqlInstanceName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di impostare il punto di controllo del servizio Active Directory per Lync Server archivio di gestione centrale. In questo esempio, il punto di controllo del servizio indica il computer atl-sql-001.litwareinc.com e l'istanza di SQL Server Rtc.

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc

## ESEMPIO 2

Il comando riportato nell'Esempio 2 è una variante del comando riportato nell'Esempio 1. Anche questo comando consente di impostare il punto di controllo del servizio Active Directory per Lync Server archivio di gestione centrale. Inoltre, le informazioni riguardanti l'esito di questa operazione vengono registrate nel file C:\\Logs\\Store\_Location.html. Questo file di log viene creato aggiungendo il parametro Report seguito dal percorso completo del file.

    Set-CsConfigurationStoreLocation -SqlServerFqdn atl-sql-001.litwareinc.com -SqlInstanceName Rtc -Report C:\Logs\Store_Location.html

## Descrizione dettagliata

Servizi di dominio Active Directory utilizza i punti di controllo del servizio per consentire ai computer di individuare i servizi. Quando ad esempio si installa Lync Server, viene creato un punto di controllo del servizio che fornisce informazioni sulla posizione dell'archivio di gestione centrale utilizzato per i dati di Lync Server. I computer che devono accedere al database vengono connessi ad Active Directory, che utilizza le informazioni contenute nel punto di controllo del servizio per consentire loro di individuare il computer corretto e l'istanza di SQL Server appropriata.

Come già osservato, quando si installa Lync Server, viene automaticamente creato un punto di controllo del servizio per l'archivio di gestione centrale. Se si deve spostare tale database in un altro computer oppure in un'altra istanza di SQL Server, sarà necessario aggiornare il punto di controllo del servizio corrispondente. Questa operazione può essere eseguita utilizzando il cmdlet **Set-CsConfigurationStoreLocation**. Quando viene eseguito, il cmdlet **Set-CsConfigurationStoreLocation** ricerca in Active Directory il computer specificato nel parametro SqlServer. Il cmdlet quindi imposta come percorso di archiviazione il nome di dominio completo del computer.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsConfigurationStoreLocation** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins.

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
<td><p><em>SqlServerFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del computer su cui è installato archivio di gestione centrale. Ad esempio: -SqlServer atl-sql-001.litwareinc.com.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del controller di dominio dove sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema di Active Directory, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore di configurazione, è possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>MirrorSqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'istanza di SQL Server contenente i dati e le tabelle del database mirror di Lync Server, ad esempio: -SqlInstanceName &quot;rtc&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>MirrorSqlServerFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del computer in cui è stato installato il database mirror di archivio di gestione centrale, ad esempio: -SqlServer atl-mirror-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipLookup</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se questo parametro è incluso, il cmdlet <strong>Set-CsConfigurationStoreLocation</strong> non verifica la disponibilità del computer e dell'istanza di SQL Server specificati. Il cmdlet modifica semplicemente il punto di controllo del servizio.</p>
<p>Se questo parametro non è incluso, il computer e l'istanza di SQL Server specificati devono essere disponibili perché sia possibile modificare il punto di controllo del servizio.</p></td>
</tr>
<tr class="odd">
<td><p><em>SqlInstanceName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'istanza di SQL Server che contiene i dati e le tabelle di Lync Server. Ad esempio: -SqlInstanceName &quot;rtc&quot;.</p></td>
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

Nessuno. Il cmdlet **Set-CsConfigurationStoreLocation** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Set-CsConfigurationStoreLocation** non restituisce oggetti o valori.

## Vedere anche

#### Ulteriori risorse

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

