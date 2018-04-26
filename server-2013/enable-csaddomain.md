---
title: Enable-CsAdDomain
TOCTitle: Enable-CsAdDomain
ms:assetid: a39768de-51ae-45e8-b6b7-441b5da0b3b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412764(v=OCS.15)
ms:contentKeyID: 49301530
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsAdDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni di sicurezza per i gruppi universali creati durante la preparazione della foresta. Tali modifiche forniscono le autorizzazioni necessarie per ospitare e gestire gli utenti abilitati per Lync Server all'interno del dominio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsAdDomain [-Confirm [<SwitchParameter>]] [-CrossForest <SwitchParameter>] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-SkipPrepareCheck <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 prepara il dominio locale per l'installazione di Lync Server.

    Enable-CsAdDomain

## ESEMPIO 2

Nell'esempio 2 viene preparato il dominio asia.litwarein.com per l'installazione di Lync Server.

    Enable-CsAdDomain -Domain asia.litwareinc.com

## Descrizione dettagliata

Prima di installare Lync Server in un dominio, è necessario preparare correttamente il dominio. Questo processo include l'estensione dello schema di Active Directory per consentire l'aggiunta di attributi specifici di Lync Server, nonché l'assegnazione delle voci di controllo di accesso richieste ai gruppi universali necessari per la gestione e il funzionamento di Lync Server. La preparazione del dominio in genere viene eseguita tramite l'installazione guidata di Lync Server. Gli amministratori tuttavia possono eseguire la preparazione di un dominio anche utilizzando il cmdlet **Enable-CsAdDomain**.

Dopo aver eseguito il cmdlet **Enable-CsAdDomain**, è possibile utilizzare il cmdlet **Get-CsAdDomain** per verificare che il dominio sia pronto per il passaggio successivo del processo di installazione.


> [!NOTE]
> Se viene visualizzato l'errore "Impossibile trovare l'oggetto "CrossRef" in Active Directory" quando si eseguono le attività di preparazione di un dominio figlio in un ambiente a foresta singola con più domini, potrebbe essere necessario aggiungere manualmente il gruppo RTCComponentUniversalServices dal dominio padre al gruppo di accesso autorizzazione Windows nel dominio figlio.



Questo cmdlet esegue attività simili a quelle effettuate dal seguente comando di Microsoft Office Communications Server 2007 R2:

Lcscmd.exe /domain /action:DomainPrep

Utenti autorizzati a eseguire il cmdlet: possono eseguire localmente il cmdlet **Enable-CsAdDomain** solo gli amministratori di dominio.

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
<td><p><em>CrossForest</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, indica che la preparazione del dominio viene eseguita nel dominio di una foresta differente. Questo parametro non è obbligatorio se il dominio che viene abilitato si trova nella stessa foresta del computer in cui viene eseguito il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio in cui deve essere eseguita la preparazione, ad esempio -Domain asia.litwareinc.com. Se questo parametro non viene incluso, la preparazione del dominio viene eseguita nel dominio locale.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome di dominio completo (FQDN) del controller di dominio da utilizzare quando si esegue il cmdlet <strong>Enable-CsAdDomain</strong>. Se non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Enable-CsAdDomain</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome FQDN di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema in Servizi di dominio Active Directory, questo parametro deve puntare al controller di dominio radice. Se nel contenitore Configurazione sono archiviate impostazioni globali, è possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\DomainPrep.html&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True ($True), il cmdlet <strong>Enable-CsAdDomain</strong> ignora il controllo di preparazione iniziale.</p></td>
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

Nessuno. Il cmdlet **Enable-CsAdDomain** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Disable-CsAdDomain](disable-csaddomain.md)  
[Get-CsAdDomain](get-csaddomain.md)

