---
title: Import-CsLegacyConfiguration
TOCTitle: Import-CsLegacyConfiguration
ms:assetid: bd688c08-abb8-4c78-8e1b-b330412d4422
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412923(v=OCS.15)
ms:contentKeyID: 49301813
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsLegacyConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Import-CsLegacyConfiguration** consente di importare in Lync Server diverse impostazioni di configurazione da Microsoft Office Communications Server 2007 R2 o Microsoft Office Communications Server 2007. In questo modo viene garantita l'interoperabilità tra Lync Server e l'installazione precedente di Office Communications Server 2007 R2 o di Office Communications Server 2007. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CsLegacyConfiguration [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-ReplaceExisting <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 unisce i criteri vocali e altre impostazioni di Communications Server 2007 o Communications Server 2007 R2 con un'installazione di Lync Server.

    Import-CsLegacyConfiguration

## ESEMPIO 2

Il comando riportato nell'esempio 2 è una variante del comando illustrato nell'esempio 1. In questo caso tuttavia è incluso il parametro ReplaceExisting. Questo parametro indica al cmdlet di utilizzare i dati importati per risolvere conflitti di nomi. Ad esempio, si supponga di provare a importare una route vocale denominata LocalRoute e che nell'installazione Lync Server in uso esista già una route vocale con lo stesso nome. Poiché si è incluso il parametro ReplaceExisting, la route di Lync Server verrà sostituita dalla route vocale importata.

    Import-CsLegacyConfiguration -ReplaceExisting

## Descrizione dettagliata

Il cmdlet **Import-CsLegacyConfiguration** viene utilizzato insieme al cmdlet **Merge-CsLegacyTopology** per consentire alle organizzazioni di eseguire la migrazione da una versione precedente di Office Communications Server (Office Communications Server 2007 R2 oppure Office Communications Server 2007) a Lync Server. Il cmdlet **Import-CsLegacyConfiguration** viene utilizzato per importare i criteri vocali, i profili località (ad esempio i dial plan), le route vocali, le regole di normalizzazione vocale, i criteri di riunione, i criteri di accesso esterno, i criteri di archiviazione, i criteri di presenza, le impostazioni degli URL di Communicator Web Access e i numeri di accesso per le conferenze telefoniche con accesso esterno.

Prima di eseguire il cmdlet **Import-CsLegacyConfiguration**, è necessario installare il pacchetto di interfacce per la compatibilità con le versioni precedenti di Strumentazione gestione Windows (WMI). Questa applicazione viene installata eseguendo OCSWMIBC.msi. Dopo aver installato il pacchetto di interfacce per la compatibilità, eseguire il cmdlet **Merge-CsLegacyTopology**. Dopo aver eseguito il cmdlet **Merge-CsLegacyTopology**, utilizzare Generatore di topologie per pubblicare la topologia unita. Dopo aver pubblicato la topologia unita, è possibile chiamare il cmdlet **Import-CsLegacyConfiguration**. Il cmdlet **Import-CsLegacyConfiguration** utilizza WMI per leggere i dati legacy dalla versione precedente di Office Communications Server. Il cmdlet **Import-CsLegacyConfiguration** utilizza quindi i dati recuperati e crea gli oggetti corrispondenti in Lync Server. Per ognuno dei criteri vocali rilevati nell'installazione di Office Communications Server, viene ad esempio creato un criterio vocale corrispondente nella nuova installazione di Lync Server.

È consigliabile rieseguire il cmdlet **Import-CsLegacyConfiguration** ogni volta che si apportano modifiche a uno degli elementi di Office Communications Server seguenti: criteri vocali, profili località, route vocali, regole di normalizzazione vocale, criteri di riunione, criteri di accesso esterno, criteri di archiviazione, criteri di presenza, impostazioni degli URL di Communicator Web Access e numeri di accesso alle conferenze telefoniche con accesso esterno. Per impostazione predefinita, quando si riesegue il cmdlet **Import-CsLegacyConfiguration** vengono importati solo i nuovi elementi aggiunti alla topologia di Office Communications Server. Per importare gli oggetti modificati, è necessario effettuare due operazioni. Verificare innanzitutto che non siano state apportate modifiche all'elemento corrispondente, ad esempio un criterio vocale, nella copia di Lync Server della configurazione. Eseguire quindi il cmdlet **Import-CsLegacyConfiguration** con il parametro ReplaceExisting. In questo modo il cmdlet **Import-CsLegacyConfiguration** importerà gli oggetti modificati e sovrascriverà l'oggetto corrispondente attualmente presente in Lync Server. Gli oggetti eliminati dalla topologia di Communications Server 2007 R2 non vengono rimossi da Lync Server. Sarà necessario pertanto rimuoverli manualmente in Lync Server.

È importante sapere che il cmdlet **Move-CsLegacyUser** si basa sulle informazioni importate dal cmdlet **Import-CsLegacyConfiguration**. Quando si esegue il cmdlet **Move-CsLegacyUser**, è possibile pertanto che venga visualizzato un messaggio di errore in cui viene indicato che è necessario eseguire il cmdlet **Import-CsLegacyConfiguration** prima di continuare. In questo caso, sarà necessario rieseguire il cmdlet **Import-CsLegacyConfiguration** prima di poter spostare l'utente legacy.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Import-CsLegacyConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsLegacyConfiguration"}

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
<td><p><em>ReplaceExisting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, questo parametro indica al cmdlet <strong>Import-CsLegacyConfiguration</strong> di sovrascrivere eventuali impostazioni o criteri precedentemente importati che sono stati modificati rispetto all'ultima volta che è stato eseguito il cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\ImportConfiguration.html&quot;</p></td>
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

Nessuno. Il cmdlet **Import-CsLegacyConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Import-CsLegacyConfiguration** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Import-CsLegacyConferenceDirectory](import-cslegacyconferencedirectory.md)  
[Merge-CsLegacyTopology](merge-cslegacytopology.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

