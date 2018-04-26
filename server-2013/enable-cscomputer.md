---
title: Enable-CsComputer
TOCTitle: Enable-CsComputer
ms:assetid: ac014030-4cd0-4503-b70e-12ab5b0ec34b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412815(v=OCS.15)
ms:contentKeyID: 49301633
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsComputer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Abilita servizi o ruoli del server nuovi o aggiornati recentemente in un computer che esegue Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsComputer [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 attiva qualsiasi nuovo servizio o ruolo del server di Lync Server installato nel computer locale.

    Enable-CsComputer

## ESEMPIO 2

Anche nell'esempio 2 viene attivato qualsiasi nuovo servizio o ruolo del server di Lync Server installato nel computer locale. In questo caso l'aggiunta del parametro Verbose assicura però che vengano visualizzate in modo dettagliato le attività eseguite dal cmdlet **Enable-CsComputer**.

    Enable-CsComputer -Verbose

## Descrizione dettagliata

L'installazione del software richiesto non causa automaticamente l'adozione da parte di un computer di un nuovo ruolo di servizio; tale computer, viceversa, deve essere abilitato per poter funzionare effettivamente nel nuovo ruolo. Il cmdlet **Enable-CsComputer** consente agli amministratori di abilitare sul computer locale servizi o ruoli del server aggiornati recentemente.

Utenti autorizzati a eseguire il cmdlet: possono eseguire localmente il cmdlet **Enable-CsComputer** solo gli amministratori locali e i membri del dominio.

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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Enable-CsComputer</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome FQDN di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema in Active Directory, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, è possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\EnableComputer.html&quot;</p></td>
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

Nessuno. Il cmdlet **Enable-CsComputer** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Enable-CsComputer** invece abilita le istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.Machine.

## Vedere anche

#### Ulteriori risorse

[Disable-CsComputer](disable-cscomputer.md)  
[Get-CsComputer](get-cscomputer.md)  
[Test-CsComputer](test-cscomputer.md)

