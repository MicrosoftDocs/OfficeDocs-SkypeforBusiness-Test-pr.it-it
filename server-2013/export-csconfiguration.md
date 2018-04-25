---
title: Export-CsConfiguration
TOCTitle: Export-CsConfiguration
ms:assetid: 7da7e133-e405-466c-a852-06a4fb678c59
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398627(v=OCS.15)
ms:contentKeyID: 49301098
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esporta in un file la topologia, i criteri e le impostazioni di configurazione di Lync Server. Tra l'altro, tale file può quindi essere utilizzato per ripristinare queste informazioni nell'archivio di gestione centrale dopo un aggiornamento, un malfunzionamento hardware o altri problemi che hanno causato la perdita di dati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Export-CsConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    Export-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 esporta i dati di Lync Server dal archivio di gestione centrale in un file denominato C:\\Config.zip.

    Export-CsConfiguration -FileName "C:\Config.zip"

## Descrizione dettagliata

I computer che eseguono ruoli del server o servizi di Lync Server devono disporre di una copia della topologia corrente, delle impostazioni di configurazione correnti e dei criteri correnti prima di poter funzionare nel ruolo loro assegnato. Lync Server è responsabile di assicurare che queste informazioni vengano fornite a tutti i computer a cui siano necessarie.

I cmdlet **Export-CsConfiguration** e **Import-CsConfiguration** vengono utilizzati per il backup e il ripristino di topologia, impostazioni di configurazione e criteri di Lync Server durante l'aggiornamento dell'archivio di gestione centrale. Il cmdlet **Export-CsConfiguration** consente di esportare dati in un file ZIP. È quindi possibile utilizzare il cmdlet **Import-CsConfiguration** per leggere il file ZIP e ripristinare la topologia, le impostazioni di configurazione e i criteri nell'archivio di gestione centrale. Al termine, i servizi di replica di Lync Server replicheranno le informazioni ripristinate negli altri computer che eseguono servizi di Lync Server.

La possibilità di esportare e importare dati di configurazione viene utilizzata anche nella configurazione iniziale di computer che si trovano nella rete perimetrale, ad esempio i server perimetrali. Quando si configura un computer che si trova nella rete perimetrale, è necessario innanzitutto eseguire una replica manuale utilizzando i cmdlet CsConfiguration: sarà necessario esportare i dati di configurazione utilizzando il cmdlet **Export-CsConfiguration** e quindi copiare il file ZIP nel computer della rete perimetrale. Sarà possibile infine utilizzare il cmdlet **Import-CsConfiguration** e il parametro LocalStore per importare i dati. È sufficiente effettuare questa operazione solo una volta e successivamente la replica verrà eseguita automaticamente.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Export-CsConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsConfiguration"}

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
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso dl file ZIP che viene creato quando si esegue il cmdlet <strong>Export-CsConfiguration</strong>, ad esempio: -FileName &quot;C:\Config.zip&quot;. Si noti che è necessario includere il parametro FileName o il parametro AsBytes, ma non entrambi quando si utilizza il cmdlet <strong>Export-CsConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce le informazioni sulla topologia nel formato matrice di byte, i dati devono poi essere memorizzati in una variabile per poter essere utilizzati dal cmdlet <strong>Import-CsConfiguration</strong>. Non è possibile utilizzare entrambi i parametri AsBytes e FileName nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando. Per impostare il parametro Force su True, utilizzare la seguente sintassi:</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione dal computer locale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Export-CsConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Se viene utilizzato con il parametro AsBytes, il cmdlet **Export-CsConfiguration** restituisce le informazioni di configurazione nel formato matrice di byte.

## Vedere anche

#### Ulteriori risorse

[Import-CsConfiguration](import-csconfiguration.md)

