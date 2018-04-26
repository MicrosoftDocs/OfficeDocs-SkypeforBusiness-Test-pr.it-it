---
title: Disable-CsAdForest
TOCTitle: Disable-CsAdForest
ms:assetid: 06a6117c-27da-400f-8db9-eb28fe353aae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398122(v=OCS.15)
ms:contentKeyID: 49299570
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disable-CsAdForest

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Annulla le attività di preparazione della foresta eseguite dal cmdlet **Enable-CsAdForest**. Questo cmdlet viene utilizzato in genere solo se si disinstalla Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Disable-CsAdForest [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-GroupDomain <Fqdn>] [-GroupDomainController <Fqdn>] [-Report <String>] [-RootDomainController <Fqdn>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 esegue il rollback delle attività di preparazione della foresta effettuate dal cmdlet **Enable-CsAdForest**. Dal momento che il parametro Force non è incluso, il comando avrà esito negativo se il cmdlet **Disable-CsAdForest** rileva che almeno uno dei domini della foresta è ancora preparato per Lync Server. In tal caso, sarà necessario eseguire il rollback delle attività di preparazione del dominio eseguendo il cmdlet **Disable-CsAdDomain**.

    Disable-CsAdForest

## ESEMPIO 2

Nell'esempio 2 viene eseguito il rollback della preparazione della foresta anche se il cmdlet **Disable-CsAdForest** rileva che almeno uno dei domini della foresta è ancora preparato per Lync Server. Il rollback viene imposto includendo il parametro Force.

    Disable-CsAdForest -Force

## Descrizione dettagliata

Durante l'installazione di Lync Server, vengono apportate diverse modifiche a livello di foresta in Servizi di dominio Active Directory. Queste modifiche (che possono essere eseguite utilizzando il cmdlet **Enable-CsAdForest**) includono la creazione di oggetti e di identificatori di visualizzazione specifici per Lync Server, la creazione dei gruppi di sicurezza universali necessari per gestire Lync Server e la concessione a questi gruppi delle autorizzazioni e dei diritti amministrativi per accedere all'oggetto impostazioni globali. Se in seguito si decide di disinstallare Lync Server (o se si riscontrano problemi durante il processo di installazione), potrebbe essere necessario eseguire il rollback di queste modifiche a livello di foresta. Il cmdlet **Disable-CsAdForest** consente di annullare tutte le modifiche a livello di foresta apportate dal cmdlet **Enable-CsAdForest**.

Le attività eseguite dal cmdlet **Disable-CsAdForest** sono simili a quelle svolte dal comando seguente di Microsoft Office Communications Server 2007 R2:

Lcscmd.exe /forest /action:ForestUnprep

Utenti autorizzati a utilizzare questo cmdlet: È necessario essere amministratori dell'organizzazione per poter utilizzare localmente il cmdlet **Disable-CsAdForest**.

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
<td><p>Se presente, impone il rollback delle operazioni di preparazione della foresta anche se il cmdlet <strong>Disable-CsAdForest</strong> rileva che almeno uno dei domini della foresta è ancora preparato per Lync Server. Se non presente, il comando avrà esito negativo quando il cmdlet <strong>Disable-CsAdForest</strong> rileva che almeno uno dei domini della foresta è ancora preparato per Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Disable-CsComputer</strong> su un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del controller di dominio dove sono archiviate le impostazioni globali. Se le impostazioni globali vengono archiviate nel contenitore di sistema in Servizi di dominio Active Directory, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore di configurazione, è possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupDomain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio in cui sono stati creati i gruppi universali di Lync Server, ad esempio -GroupDomain asia.litwareinc.com. Se questo parametro non è incluso, il cmdlet <strong>Disable-CsAdForest</strong> cercherà i gruppi universali nel dominio locale.</p></td>
</tr>
<tr class="even">
<td><p><em>GroupDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del controller di dominio in cui vengono archiviate le informazioni del gruppo universale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\DisableForest.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>RootDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del controller di dominio radice utilizzato per creare percorsi di trust per i client che devono accedere alle risorse nei domini diversi dai propri.</p></td>
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

Nessuno.

## Tipi restituiti

Nessuno.

