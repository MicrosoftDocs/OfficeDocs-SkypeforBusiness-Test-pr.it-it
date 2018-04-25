---
title: Publish-CsTopology
TOCTitle: Publish-CsTopology
ms:assetid: d8f5dfd9-0ab6-4703-9d50-2fa50b3fd58b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398953(v=OCS.15)
ms:contentKeyID: 49302139
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Publish-CsTopology

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Pubblica la topologia di Lync Server recuperata utilizzando il cmdlet **Get-CsTopology**. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Publish-CsTopology -FileName <String> <COMMON PARAMETERS>

    Publish-CsTopology -Document <XElement> <COMMON PARAMETERS>

    Publish-CsTopology -FinalizeUninstall <SwitchParameter> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BackupFileName <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 recuperano e quindi ripubblicano la topologia corrente. Per eseguire queste attività, nel primo comando dell'esempio vengono utilizzati il cmdlet **Get-CsTopology** e il parametro AsXml per recuperare la topologia corrente. Il simbolo di reindirizzamento di Windows PowerShell \> viene quindi utilizzato per salvare i dati recuperati in un file denominato C:\\Topologies\\Topology.xml. Si noti inoltre che viene utilizzato il metodo ToString per convertire la topologia recuperata in un valore stringa. Nel secondo comando dell'esempio viene quindi utilizzato il cmdlet **Publish-CsTopology** per ripubblicare la topologia appena recuperata.

    (Get-CsTopology -AsXml).ToString() > C:\Topologies\Topology.xml 
    Publish-CsTopology -FileName "C:\Topologies\Topology.xml"

## Descrizione dettagliata

Dopo aver installato Lync Server, può accadere di dover apportare modifiche all'infrastruttura di Lync Server, ad esempio allo scopo di aggiungere un nuovo sito, eliminare un pool di registrazione esistente o aggiungere un ulteriore server di archiviazione. Tali modifiche relative all'infrastruttura devono essere apportate mediante lo Generatore di topologie. Dopo aver effettuato le modifiche nello Generatore di topologie, è possibile pubblicarle e abilitarle utilizzando lo stesso strumento. Questi ultimi due passaggi sono molto importanti. Sebbene con lo Generatore di topologie sia possibile apportare tutte le modifiche desiderate, l'infrastruttura di Lync Server verrà modificata e le modifiche diventeranno effettive solo dopo la pubblicazione delle stesse e l'abilitazione della nuova topologia.

Con la pubblicazione delle modifiche, le nuove informazioni, ad esempio un nuovo sito o un nuovo ruolo del server, vengono scritte nell'archivio di gestione centrale. Questi oggetti nuovi, o appena modificati, tuttavia non vengono aggiunti immediatamente alla topologia, ma solo dopo l'abilitazione della topologia aggiornata. Se si seleziona l'opzione Pubblicazione nello Generatore di topologie, verranno effettuate le due operazioni seguenti: le modifiche verranno pubblicate, ovvero scritte nell'archivio di gestione centrale, e la nuova topologia verrà abilitata.

Il cmdlet **Publish-CsTopology** non rappresenta più il metodo consigliato per pubblicare le topologie create utilizzando lo Generatore di topologie. È invece preferibile effettuare la pubblicazione all'interno dello Generatore di topologie eseguendo le operazioni descritte nel paragrafo precedente. Ciò è dovuto al fatto che lo Generatore di topologie ora utilizza il formato di file XML (con estensione tbxml) specifico dello Generatore di topologieche non può essere pubblicato mediante **Publish-CsTopology**. L'unica operazione consentita con il cmdlet **Publish-CsTopology** è la ripubblicazione di una topologia recuperata utilizzando il cmdlet **Get-CsTopology**. Dopo avere pubblicato la topologia in questo modo, sarà necessario riconfigurare gli URL semplici.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Publish-CsTopology** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Se però le autorizzazioni di installazione non sono state delegate, sarà possibile eseguire il cmdlet **Publish-CsTopology** solo se si è amministratori di dominio. Per conferire al gruppo RTCUniversalServerAdmins il diritto di utilizzare effettivamente il cmdlet **Publish-CsTopology**, è necessario eseguire il cmdlet **Grant-CsSetupPermission** per ogni contenitore di Active Directory con computer che eseguono servizi di Lync Server. Tale restrizione si applica anche all'abilitazione di una topologia mediante lo Generatore di topologie. Se le autorizzazioni non sono state delegate utilizzando il cmdlet **Set-CsSetupPermission**, solo un amministratore di dominio potrà pubblicare una topologia mediante lo Generatore di topologie.

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
<td><p><em>Document</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Xml.Linq.XElement</p></td>
<td><p>Consente di pubblicare un elemento XML anziché un file XML. Questo elemento XML deve essere configurato come oggetto System.XML.Linq.XElement.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file XML contenente le informazioni della nuova topologia.</p></td>
</tr>
<tr class="odd">
<td><p><em>FinalizeUninstall</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Utilizzato solo quando si disinstalla Lync Server. Dopo la rimozione del server di gestione centrale, utilizzare Publish-CsTopology e il parametro FinalizeUninstall per pubblicare una topologia vuota. Tra le altre cose, questa operazione comporta la rimozione di tutte le voci di Active Directory per il server di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>BackupFileName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file di backup creato automaticamente quando si esegue il cmdlet <strong>Publish-CsTopology</strong>. Se questo parametro non viene specificato, il cmdlet <strong>Publish-CsTopology</strong> creerà nella cartella Temp (%temp%) un file di backup simile al seguente: Publish-CsTopology-Backup-[2010_10_01][08_30_00]. Nel nome del file 2010_10_01 rappresenta la data in cui è avvenuta la pubblicazione: anno (2010), mese (10) e giorno (01). Inoltre, 08_30_00 rappresenta l'ora del giorno in cui è avvenuta la pubblicazione: ore (08), minuti (30) e secondi (00).</p></td>
</tr>
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
<td><p>Il nome di dominio completo (FQDN) di un server di catalogo globale nel dominio in uso. Questo parametro non è necessario se si esegue il cmdlet <strong>Publish-CsTopology</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un controller di dominio in cui sono archiviate le impostazioni globali. Se le impostazioni globali sono archiviate nel contenitore di sistema in Servizi di dominio Active Directory, questo parametro dovrà puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore della configurazione, sarà possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\Publish_Topology.html&quot;</p></td>
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

Nessuno. Il cmdlet **Publish-CsTopology** non accetta input inviato tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Publish-CsTopology** pubblica invece le istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.DefaultTopology.

## Vedere anche

#### Ulteriori risorse

[Enable-CsTopology](enable-cstopology.md)  
[Get-CsTopology](get-cstopology.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[Test-CsTopology](test-cstopology.md)

