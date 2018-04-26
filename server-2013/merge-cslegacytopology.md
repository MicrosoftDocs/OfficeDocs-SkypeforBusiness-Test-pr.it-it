---
title: Merge-CsLegacyTopology
TOCTitle: Merge-CsLegacyTopology
ms:assetid: 396d6c84-7b38-41ae-9273-665f76cdd9ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425870(v=OCS.15)
ms:contentKeyID: 49300228
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Merge-CsLegacyTopology

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Merge-CsLegacyTopology** consente di eseguire la migrazione delle informazioni sulla topologia da Microsoft Office Communications Server 2007 R2 o Microsoft Office Communications Server 2007 a Lync Server. In questo modo si garantisce l'interoperabilità tra Lync Server e le versioni precedenti del software. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Merge-CsLegacyTopology -TopologyXmlFileName <String> <COMMON PARAMETERS>

    Merge-CsLegacyTopology -Reserved <PSObject> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-UserInputFileName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 unisce le informazioni della topologia e le voci dei servizi trusted di Communications Server 2007 R2 o Communications Server 2007 a una nuova installazione di Lync Server. Il parametro obbligatorio TopologyXmlFileName consente di indicare il percorso del file di output generato durante l'esecuzione del cmdlet **Merge-CsLegacyTopology**.

    Merge-CsLegacyTopology -TopologyXmlFileName C:\New_Topology.xml

## ESEMPIO 2

L'esempio 2 rappresenta una variazione del comando utilizzato nell'esempio 1. Con l'esempio 2, viene incluso il parametro UserInputFileName per unire le informazioni degli Edge Server nella topologia. Il valore del parametro C:\\EdgeServers.xml punta a un file XML personalizzato contenente le informazioni di Edge Server per Office Communications Server.

    Merge-CsLegacyTopology -TopologyXmlFileName C:\New_Topology.xml -UserInputFileName C:\EdgeServers.xml

## Descrizione dettagliata

Il cmdlet **Merge-CsLegacyTopology** è il primo strumento da utilizzare per eseguire la migrazione da una versione precedente di Office Communications Server (Office Communications Server 2007 R2 o Office Communications Server 2007) a Lync Server. Il cmdlet **Merge-CsLegacyTopology** consente di eseguire la migrazione delle voci dei servizi trusted e delle informazioni della topologia per i componenti seguenti: domini, servizi utente, funzione di registrazione, Mediation Server e server perimetrale. Il cmdlet inoltre esegue la migrazione delle voci dei servizi trusted per l'applicazione Operatore Conferenza, Communicator Web Access e le directory conferenze. Una voce di servizio trusted è un record di Active Directory che rappresenta un server ritenuto attendibile da Lync Server. L'unione delle informazioni della topologia consente agli utenti situati in Lync Server di comunicare con gli utenti situati in Communications Server 2007 o Communications Server 2007 R2.

Prima di poter eseguire il cmdlet **Merge-CsLegacyTopology**, è necessario installare il pacchetto di interfacce di compatibilità con le versioni precedenti di Strumentazione gestione Windows (WMI). Questa applicazione viene installata eseguendo OCSWMIBC.msi, presente nel DVD di installazione. Dopo aver installato il pacchetto di interfacce di compatibilità, è possibile chiamare il cmdlet **Merge-CsLegacyTopology**. Il cmdlet **Merge-CsLegacyTopology** utilizza WMI per leggere i dati legacy dalla versione precedente di Office Communications Server. Recupera quindi i dati e crea oggetti corrispondenti in Lync Server. Per ogni dominio SIP individuato nell'installazione di Office Communications Server, viene ad esempio creato un dominio SIP corrispondente nella nuova installazione di Lync Server.

Dopo aver eseguito il cmdlet **Merge-CsLegacyTopology**, è consigliabile eseguire i cmdlet **Import-CsLegacyConfiguration** e **Import-CsLegacyConferenceDirectory**.

Il cmdlet **Merge-CsLegacyTopology** deve essere eseguito almeno due volte: una volta all'inizio di una migrazione (per introdurre la topologia di Communications Server 2007 o Communications Server 2007 R2) e una volta alla fine della migrazione, quando per il precedente ambiente Office Communications Server sono state rimosse le autorizzazioni. È inoltre necessario eseguire il cmdlet ogni volta che si apporta una modifica all'ambiente Office Communications Server legacy. Ad esempio, se si aggiunge un Mediation Server o si rimuovono le autorizzazioni per un pool della topologia di Office Communications Server, è necessario eseguire di nuovo il cmdlet **Merge-CsLegacyTopology** per importare la topologia modificata.

I cmdlet **Import-CsLegacyConfiguration** e **Import-CsLegacyConferenceDirectory** dipendono dai valori configurati dal cmdlet **Merge-CsLegacyTopology**. Di conseguenza, si potrebbero ricevere dal cmdlet **Import-CsLegacyConfiguration** o **Import-CsLegacyConferenceDirectory** messaggi di errore che invitano a eseguire il cmdlet **Merge-CsLegacyTopology** come possibile soluzione al problema verificatosi. Se non si esegue di nuovo il cmdlet **Merge-CsLegacyTopology**, potrebbero verificarsi ulteriori errori, soprattutto se si rimuove dall'ambiente Office Communications Server un elemento che è ancora in uso in Lync Server.

Per unire server perimetrali di una precedente installazione di Office Communications Server, è necessario innanzitutto creare un file XML personalizzato contenente il server perimetrale. Il file deve essere creato personalmente perché le impostazioni del server perimetrale non sono archiviate in Active Directory e di conseguenza non possono essere recuperate dal cmdlet **Merge-CsLegacyTopology**. Dopo avere creato questo file XML (vedere la guida alla distribuzione di Lync Server per informazioni sulla creazione del file), è necessario includere il percorso del file e il parametro UserInputFileName durante l'esecuzione del cmdlet **Merge-CsLegacyTopology**. Se non si esegue questa operazione, i server perimetrali non verranno inclusi nella topologia unita.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Merge-CsLegacyTopology** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Merge-CsLegacyTopology"}

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
<td><p><em>Reserved</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>PS topology object</p></td>
<td><p>Consente di unire la topologia utilizzando un oggetto topologia anziché un file XML della topologia.</p></td>
</tr>
<tr class="even">
<td><p><em>TopologyXmlFileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file di output da creare durante l'esecuzione del cmdlet <strong>Merge-CsLegacyTopology</strong>. Tale file non corrisponde al file specificato utilizzando il parametro Report. Quest'ultimo file è utilizzato per la registrazione delle informazioni di errore, mentre il file XML della topologia include la topologia di Lync Server appena creata. Questo file sarà utilizzato in seguito per pubblicare la nuova topologia.</p>
<p>Se il file specificato già esiste, verrà sovrascritto durante l'esecuzione del cmdlet <strong>Merge-CsLegacyTopology</strong>.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\MergeTopology.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>UserInputFileName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file XML utilizzato per importare i dati del server perimetrale (server perimetrale) da una precedente versione di Office Communications Server. Questo file XML (che deve essere creato attenendosi alle linee guida disponibili nella guida alla distribuzione di Lync Server) è necessario in quanto le impostazioni del server perimetrale (server perimetrale) non sono archiviate in Servizi di dominio Active Directory. Se non è necessario importare le informazioni del server perimetrale (server perimetrale), questo parametro può essere omesso.</p>
<p>Se questo parametro non viene utilizzato, le funzionalità di accesso remoto ed esterno (compresa la federazione) potrebbero non funzionare come previsto in un ambiente in cui sono in esecuzione sia Communications Server 2007 R2 sia Communications Server 2007 R2 e Lync Server.</p></td>
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

Nessuno. Il cmdlet **Merge-CsLegacyTopology** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Merge-CsLegacyTopology** non restituisce oggetti o valori.

## Vedere anche

#### Ulteriori risorse

[Import-CsLegacyConfiguration](import-cslegacyconfiguration.md)  
[Import-CsLegacyConferenceDirectory](import-cslegacyconferencedirectory.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

