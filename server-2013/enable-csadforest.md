---
title: Enable-CsAdForest
TOCTitle: Enable-CsAdForest
ms:assetid: 2381fca7-294b-486d-919d-e8626cef6fea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425713(v=OCS.15)
ms:contentKeyID: 49299935
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsAdForest

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Definisce le modifiche di Active Directory come obbligatorie per poter installare Lync Server. Sono incluse le modifiche globali ai contenitori Configuration o System, la creazione di gruppi universali e la creazione di specificatori di visualizzazione e insiemi di proprietà specifici di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsAdForest [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-GroupDomain <Fqdn>] [-GroupDomainController <Fqdn>] [-Report <String>] [-RootDomainController <Fqdn>] [-SkipPrepareCheck <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando prepara la foresta di Active Directory per l'installazione di Lync Server. Dal momento che non viene utilizzato il parametro GroupDomain, i gruppi di sicurezza universali generati quando si esegue il cmdlet **Enable-CsAdForest** verranno creati nel dominio locale.

    Enable-CsAdForest

## ESEMPIO 2

Questo comando prepara la foresta di Active Directory per l'installazione di Lync Server. Il parametro GroupDomain viene utilizzato per garantire che i gruppi di sicurezza universali creati eseguendo il cmdlet **Enable-CsAdForest** vengano creati nel dominio northamerica.litwareinc.com.

    Enable-CsAdForest -GroupDomain northamerica.litwareinc.com

## Descrizione dettagliata

Prima di installare Lync Server, è necessario apportare diverse modifiche a livello di foresta in Servizi di dominio Active Directory. Tra queste sono incluse la creazione di specificatori di visualizzazione e oggetti specifici di Lync Server, la creazione dei gruppi di sicurezza universali necessari per la gestione di Lync Server e l'assegnazione a questi gruppi dei diritti di accesso agli oggetti delle impostazioni globali. La preparazione della foresta viene generalmente eseguita con l'Installazione guidata di Lync Server. Gli amministratori dell'organizzazione possono tuttavia eseguire la preparazione della foresta in qualsiasi momento eseguendo il cmdlet **Enable-CsAdForest**.

Al termine dell'esecuzione del cmdlet **Enable-CsAdForest**, è possibile utilizzare il cmdlet **Get-CsAdForest** per verificare che la foresta sia pronta per il passaggio successivo del processo di installazione.

Questo cmdlet esegue le stesse operazioni eseguite dal comando di Microsoft Office Communications Server 2007 R2 seguente:

Lcscmd.exe /forest /action:ForestPrep

Utenti che possono eseguire questo cmdlet: il cmdlet **Enable-CsAdForest** può essere eseguito in locale solo dagli amministratori dell'organizzazione.

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
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Enable-CsAdForest</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore Sistema in Active Directory, questo parametro deve fare riferimento al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore Configurazione, è possibile utilizzare qualsiasi dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupDomain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio in cui devono essere creati i nuovi gruppi di sicurezza universali. Se questo parametro non è incluso, i gruppi saranno creati nel dominio locale.</p></td>
</tr>
<tr class="even">
<td><p><em>GroupDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio in cui sono archiviate le informazioni sui gruppi universali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\ForestPrep.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>RootDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del controller di dominio radice utilizzato per creare i percorsi di attendibilità per i client che devono accedere alle risorse in domini diversi dal proprio.</p></td>
</tr>
<tr class="odd">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se il parametro è impostato su True ($True), Enable-CsAdForest viene eseguito senza svolgere i controlli di preparazione iniziali.</p></td>
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

Nessuno.

## Tipi restituiti

Nessuno.

