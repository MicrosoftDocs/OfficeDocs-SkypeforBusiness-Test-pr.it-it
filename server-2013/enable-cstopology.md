---
title: Enable-CsTopology
TOCTitle: Enable-CsTopology
ms:assetid: 5aedffa0-9ca1-4aec-b4ad-c3e409c0ffb2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398398(v=OCS.15)
ms:contentKeyID: 49300678
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsTopology

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di abilitare la topologia di Lync Server pubblicata più recentemente. Dopo aver apportato modifiche alla topologia, queste non saranno effettive finché non verranno pubblicate e abilitate. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsTopology [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-SkipPrepareCheck <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'Esempio 1 consente di abilitare la topologia pubblicata di recente.

    Enable-CsTopology

## Descrizione dettagliata

Dopo aver installato Lync Server, potrebbe essere necessario apportare modifiche all'infrastruttura, aggiungendo ad esempio un nuovo sito, eliminando un pool di registrazione o aggiungendo un ulteriore server di archiviazione. Queste modifiche all'infrastruttura possono essere effettuate utilizzando Generatore di topologie. Dopo aver apportato modifiche in Generatore di topologie, è possibile pubblicarle e abilitarle utilizzando lo stesso strumento. Questi ultimi due passaggi sono molto importanti: anche se è possibile apportare tutte le modifiche che si desidera utilizzando Generatore di topologie, tali modifiche non saranno effettive e l'infrastruttura non verrà modificata finché le modifiche non verranno pubblicate e non verrà abilitata la nuova topologia.

Dopo aver pubblicato le modifiche, le nuove informazioni (ad esempio, un nuovo sito o un nuovo ruolo del server) vengono scritte nell'archivio di gestione centrale. Questi oggetti nuovi (o appena modificati) non entrano tuttavia subito a far parte della topologia. Ciò si verifica solo dopo che la topologia aggiornata viene abilitata. Se si seleziona l'opzione Pubblica in Generatore di topologie, questi due passaggi verranno eseguiti contemporaneamente: le modifiche verranno pubblicate (scritte nell'archivio di gestione centrale) e la nuova topologia verrà abilitata.

Tuttavia, si potrebbe desiderare di pubblicare le modifiche e di abilitare la topologia in momenti diversi. In questo modo si potrebbe verificare il corretto completamento della distribuzione prima di inserire i nuovi oggetti nella topologia. Per pubblicare e abilitare le modifiche alla topologia in momenti diversi, è necessario fare quanto segue:

Pubblicare la topologia modificata in Generatore di topologie. A causa di recenti modifiche al prodotto, è consigliabile che la pubblicazione avvenga sempre mediante Generatore di topologie.

Utilizzare il cmdlet **Enable-CsTopology** per rendere effettive le modifiche pubblicate.

Di volta in volta potrebbe essere necessario utilizzare il cmdlet **Enable-CsTopology** per abilitare modifiche apportate al di fuori di Generatore di topologie. Ad esempio, il cmdlet deve essere utilizzato dopo i cmdlet CsKerberosAccountAssignment per modificare l'autentificazione Web Kerberos.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Enable-CsTopology** i membri dei gruppi seguenti: RTCUniversalServerAdmins. Se tuttavia le autorizzazioni di installazione non sono state delegate, è necessario essere amministratore di dominio per poter utilizzare il cmdlet. Per concedere ai membri di RTCUniversalServerAdmins il diritto di utilizzare effettivamente il cmdlet **Enable-CsTopology**, è necessario eseguire il cmdlet **Grant-CsSetupPermission** per ogni contenitore di Active Directory nel quale siano presenti computer che eseguono servizi di Lync Server. Si noti che queste restrizioni si applicano anche per abilitare una topologia per mezzo di Generatore di topologie. Se non si dispone di autorizzazioni delegate utilizzando **Grant-CsSetupPermission**, solo gli amministratori di dominio saranno in grado di abilitare una topologia tramite Generatore di topologie.

È necessario inoltre essere amministratore locale dei computer in cui devono essere create condivisioni di file di Lync Server, poiché devono essere impostate le autorizzazioni di sicurezza necessarie per le cartelle condivise. In alternativa, se si si dispone del pieno controllo delle condivisioni di file, è possibile eseguire il cmdlet **Enable-CsTopology**. In questo modo il cmdlet può creare le cartelle condivise e impostare le autorizzazioni di sicurezza a livello di condivisione. Un amministratore locale dovrà tuttavia aggiungere le autorizzazioni di sicurezza a livello di condivisione.

Per verificare che siano state delegate le autorizzazioni all'installazione, eseguire il cmdlet **Test-CsSetupPermission** per ogni contenitore di Active Directory nel quale siano presenti computer che eseguono servizi di Lync Server.

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
<td><p>Nome di dominio completo (FQDN) del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Enable-CsTopology</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del controller di dominio dove sono archiviate le impostazioni globali. Se le impostazioni globali vengono archiviate nel contenitore di sistema in Servizi di dominio Active Directory, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore di configurazione, è possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\Enable_Topology.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>SkipPrepareCheck</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se è impostato True ($True), il cmdlet <strong>Enable-CsTopology</strong> ignorerà il controllo di preparazione iniziale.</p></td>
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

Nessuno. Il cmdlet **Enable-CsTopology** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Enable-CsTopology** abilita invece le istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology.

## Vedere anche

#### Ulteriori risorse

[Get-CsTopology](get-cstopology.md)  
[Grant-CsSetupPermission](grant-cssetuppermission.md)  
[Publish-CsTopology](publish-cstopology.md)  
[Test-CsSetupPermission](test-cssetuppermission.md)  
[Test-CsTopology](test-cstopology.md)

