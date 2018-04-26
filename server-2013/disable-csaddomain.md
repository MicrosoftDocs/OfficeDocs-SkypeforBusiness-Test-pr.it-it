---
title: Disable-CsAdDomain
TOCTitle: Disable-CsAdDomain
ms:assetid: 98a4982c-7d8d-460d-bff9-243373b20290
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398785(v=OCS.15)
ms:contentKeyID: 49301407
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsAdDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Annulla le attività di preparazione del dominio eseguite dal cmdlet **Enable-CsAdDomain**. Questo cmdlet in genere viene utilizzato solo se si disinstalla Lync Server da un dominio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Disable-CsAdDomain [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 esegue il rollback del processo di preparazione del dominio nel dominio locale. Poiché il parametro Force non è incluso, il comando ha esito negativo se il cmdlet **Disable-CsAdDomain** determina che almeno un Front End Server, un A/V Conferencing Server o un server di servizi Web è ancora attivo nel dominio.

    Disable-CsAdDomain

## ESEMPIO 2

Nell'esempio 2 viene eseguito il rollback del processo di preparazione del dominio per il dominio asia.litwareinc.com.

    Disable-CsAdDomain -Domain asia.litwareinc.com

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 viene utilizzato il parametro Force per forzare il rollback del processo di preparazione del dominio nel dominio locale. Il rollback viene eseguito anche se il cmdlet **Disable-CsAdDomain** determina che almeno un Front End Server, un A/V Conferencing Server o un server di servizi Web è ancora attivo nel dominio.

    Disable-CsAdDomain -Force

## Descrizione dettagliata

Quando si installa Lync Server in un dominio, il dominio deve essere preparato in modo corretto con un processo che estende lo schema di Active Directory per consentire l'aggiunta di attributi specifici di Lync Server e che assegna le voci di controllo di accesso richieste ai gruppi universali necessari per la gestione e il funzionamento di Lync Server. Se in seguito si decide di disinstallare Lync Server (o se si riscontrano problemi durante il processo di installazione), potrebbe essere necessario eseguire il rollback di queste modifiche a livello di dominio. Il cmdlet **Disable-CsAdDomain** consente di annullare tutte le modifiche a livello di dominio apportate dal cmdlet **Enable-CsAdDomain**.

Le operazioni eseguite dal cmdlet **Disable-CsAdDomain** sono simili a quelle effettuate dal comando di Microsoft Office Communications Server 2007 R2 seguente:

Lcscmd.exe /domain /action:DomainUnprep

Utenti che possono eseguire questo cmdlet: il cmdlet **Disable-CsAdDomain** può essere eseguito in locale solo dagli amministratori del dominio.

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
<td><p><em>Domain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del dominio per cui eseguire il rollback della preparazione (ad esempio -Domain asia.litwareinc.com). Se questo parametro non è incluso, il rollback avverrà sul dominio locale.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome di dominio completo del controller di dominio da utilizzare per l'esecuzione di <strong>Disable-CsAdDomain</strong>. Se non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se è specificato, il rollback verrà eseguito anche se il cmdlet <strong>Disable-CsAdDomain</strong> determina che almeno un Front End Server, un server di conferenze o un server di servizi Web è ancora attivo nel dominio. Se non è presente, il comando avrà esito negativo se un Front End Server, un server di conferenze o un server di servizi Web è ancora attivo nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Disable-CsAdDomain</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore Sistema in Servizi di dominio Active Directory, questo parametro deve fare riferimento al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, è possibile utilizzare qualsiasi dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\DisableDomain.html&quot;</p></td>
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

Nessuno. Il cmdlet **Disable-CsAdDomain** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Enable-CsAdDomain](enable-csaddomain.md)  
[Get-CsAdDomain](get-csaddomain.md)

