---
title: Remove-CsConfigurationStoreLocation
TOCTitle: Remove-CsConfigurationStoreLocation
ms:assetid: 141be225-c6e4-4377-913b-ba61528929d4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398214(v=OCS.15)
ms:contentKeyID: 49299762
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConfigurationStoreLocation

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il punto di controllo del servizio Active Directory per l'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsConfigurationStoreLocation [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene rimosso il punto di controllo del servizio Active Directory per il archivio di gestione centrale. Per ripristinare questo punto SCP (o per crearne uno nuovo), eseguire il cmdlet **Set-CsConfigurationStoreLocation**.

    Remove-CsConfigurationStoreLocation

## ESEMPIO 2

Anche con l'esempio 2 viene rimosso il punto di controllo del servizio Active Directory per il archivio di gestione centrale. Oltre a eliminare il punto SCP, questo comando consente di registrare le informazioni sull'esito positivo o negativo dell'operazione nel file di log C:\\Logs\\Store\_Location.html. Per creare questo file di log, il comando utilizza il parametro Report seguito dal percorso al file di log in cui dovrebbero essere registrate le informazioni. Se il file è già esistente, il suo contenuto viene sovrascritto durante l'esecuzione del comando. Se non esiste, viene creato durante l'esecuzione del comando.

    Remove-CsConfigurationStoreLocation -Report C:\Logs\Store_Location.html

## Descrizione dettagliata

Servizi di dominio Active Directory utilizza i punti di controllo del servizio per consentire ai computer di individuare i servizi. Quando ad esempio si installa Lync Server, viene creato un punto di controllo del servizio che fornisce informazioni sulla posizione per l'archivio di gestione centrale utilizzato per gestire i dati di Lync Server. I computer che devono accedere al database vengono connessi ad Active Directory, che utilizza le informazioni contenute nel punto di controllo del servizio per consentire loro di individuare il computer corretto e l'istanza di SQL Server appropriata.

Come osservato, durante l'installazione di Lync Server viene creato automaticamente un punto SCP per l'archivio di gestione centrale. Non è in genere opportuno eliminare tale punto SCP, perché altrimenti i computer non saranno in grado di individuare il database. Possono tuttavia verificarsi casi (ad esempio durante la risoluzione di un problema) in cui è richiesta l'eliminazione del punto SCP. A tale scopo, utilizzare il cmdlet **Remove-CsConfigurationStoreLocation**. Dopo aver eliminato il punto SCP, è possibile ricrearlo (o creare un nuovo punto di controllo del servizio) con il cmdlet **Set-CsConfigurationStoreLocation**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsConfigurationStoreLocation**: RTCUniversalServerAdmins.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore Sistema in Active Directory, questo parametro deve fare riferimento al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, è possibile utilizzare qualsiasi dominio e omettere questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\ConfigurationStore.html&quot;</p></td>
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

Nessuno. Il cmdlet **Remove-CsConfigurationStoreLocation** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Remove-CsConfigurationStoreLocation** non restituisce oggetti o valori.

## Vedere anche

#### Ulteriori risorse

[Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

