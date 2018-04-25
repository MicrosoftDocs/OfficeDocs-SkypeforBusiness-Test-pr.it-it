---
title: Import-CsLegacyConferenceDirectory
TOCTitle: Import-CsLegacyConferenceDirectory
ms:assetid: 5ecb9bf9-cbce-48a6-966c-ecbdac59cb3a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398418(v=OCS.15)
ms:contentKeyID: 49300710
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsLegacyConferenceDirectory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Import-CsLegacyConferenceDirectory** consente di importare le directory conferenze da Microsoft Office Communications Server 2007 R2 a Lync Server. In questo modo viene garantita l'interoperabilità tra Lync Server e Office Communications Server 2007 R2. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CsLegacyConferenceDirectory [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di importare le directory conferenze da Communications Server 2007 R2 a Lync Server.

    Import-CsLegacyConferenceDirectory

## Descrizione dettagliata

Il cmdlet **Import-CsLegacyConferenceDirectory** viene utilizzato insieme al cmdlet **Merge-CsLegacyTopology** per consentire alle organizzazioni di eseguire la migrazione da Office Communications Server 2007 R2 a Lync Server. Il cmdlet **Import-CsLegacyConfiguration** importa le directory conferenze da Communications Server 2007 R2 a Lync Server.

Per poter utilizzare il cmdlet **Import-CsLegacyConferenceDirectory**, è necessario installare il pacchetto delle interfacce utente per la compatibilità con le versioni precedenti di Strumentazione gestione Windows (WMI). Per installare questa applicazione, eseguire il file OCSWMIBC.msi, disponibile sul DVD di installazione di Lync Server nella cartella di installazione. Dopo aver installato il pacchetto delle interfacce utente per la compatibilità con le versioni precedenti, eseguire il cmdlet **Merge-CsLegacyTopology**.

Al termine dell'esecuzione del cmdlet **Merge-CsLegacyTopology**, è possibile utilizzare il cmdlet **Import-CsLegacyConferenceDirectory**. Il cmdlet **Import-CsLegacyConferenceDirectory** utilizza innanzitutto Strumentazione gestione Windows per leggere i dati legacy da Communications Server 2007 R2 e quindi utilizza i dati recuperati e crea in Lync Server gli oggetti corrispondenti. Per ogni directory conferenze trovata nell'installazione di Communications Server 2007 R2 verrà creata una directory corrispondente nella nuova installazione di Lync Server.

È opportuno utilizzare il cmdlet **Import-CsLegacyConferenceDirectory** ogni volta che si aggiungono, eliminano o spostano directory conferenze nell'ambiente Communications Server 2007 R2. È opportuno utilizzare il cmdlet **Import-CsLegacyConferenceDirectory** anche ogni volta che si utilizza il cmdlet **Merge-CsLegacyTopology**, in modo che le directory conferenze e la topologia restino sempre sincronizzate.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Import-CsLegacyConferenceDirectory** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets \\endash match "Import-CsLegacyConferenceDirectory"}

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
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\ImportDirectories.html&quot;</p></td>
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

Nessuno. Il cmdlet **Import-CsLegacyConferenceDirectory** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Import-CsLegacyConferenceDirectory** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Import-CsLegacyConfiguration](import-cslegacyconfiguration.md)  
[Merge-CsLegacyTopology](merge-cslegacytopology.md)  
[Move-CsLegacyUser](move-cslegacyuser.md)

