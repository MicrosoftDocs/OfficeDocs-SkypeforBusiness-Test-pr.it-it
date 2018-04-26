---
title: Import-CsConfiguration
TOCTitle: Import-CsConfiguration
ms:assetid: 9a9c27f2-313c-4327-aeed-c47852a831ec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398800(v=OCS.15)
ms:contentKeyID: 49301451
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa la topologia, i criteri e le impostazioni di configurazione di Lync Server nell'archivio di gestione centrale o nel computer locale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CsConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    Import-CsConfiguration -FileName <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 importa la topologia, le impostazioni di configurazione e i criteri correnti da un file denominato C:\\Config.zip nell'archivio di gestione centrale.

    Import-CsConfiguration -FileName "C:\Config.zip"

## ESEMPIO 2

L'Esempio 2 illustra il modo in cui è possibile replicare inizialmente i dati su un computer locale che si trova nella rete perimetrale. In questo esempio, i dati di configurazione sono stati esportati in un file denominato Config.zip; questo file è stato quindi copiato nella cartella C:\\ sul computer che si trova nella rete perimetrale. Viene quindi utilizzato il cmdlet Import-CsConfiguration per importare quei dati, specificando il parametro LocalStore per fare in modo che i dati siano importati sul computer locale invece che in archivio di gestione centrale.

    Import-CsConfiguration -FileName "C:\Config.zip" -LocalStore

## ESEMPIO 3

I due comandi riportati nell'esempio 3 consentono di esportare la topologia, le impostazioni di configurazione e i criteri correnti e quindi di importarli nel computer locale senza dover utilizzare un file ZIP. A tale scopo, il primo comando utilizza il cmdlet **Export-CsConfiguration** e il parametro AsBytes per esportare la topologia, le impostazioni di configurazione e i criteri correnti sotto forma di matrice di byte. Questa matrice di byte viene archiviata in una variabile denominata $x. Nel secondo comando vengono utilizzati il cmdlet **Import-CsConfiguration** e il parametro ByteInput per importare le informazioni archiviate nella variabile $x. Il parametro LocalStore fa in modo che i dati siano importati nel computer locale anziché nell'archivio di gestione centrale. Come risultato i dati vengono copiati dall'archivio di gestione centrale nel computer locale.

    $x = Export-CsConfiguration -AsBytes
    Import-CsConfiguration -ByteInput $x -LocalStore

## Descrizione dettagliata

I computer che eseguono ruoli del server o servizi di Lync Server devono avere una copia della topologia corrente, una copia delle impostazioni di configurazione correnti, una copia dei criteri correnti e così via prima che possano funzionare nel ruolo loro assegnato. Lync Server è responsabile di garantire che queste informazioni vengano passate a tutti i computer a cui sono necessarie.

I cmdlet Import-CsConfiguration ed Export-CsConfiguration vengono utilizzati per il backup e il ripristino della topologia, delle impostazioni di configurazione e dei criteri di Lync Server durante un aggiornamento dell'archivio di gestione centrale. Il cmdlet **Export-CsConfiguration** consente di esportare dati in un file ZIP. È possibile quindi utilizzare il cmdlet **Import-CsConfiguration** per leggere il file ZIP e ripristinare la topologia, le impostazioni di configurazione e i criteri nell'archivio di gestione centrale. I servizi di replica di Lync Server replicheranno quindi le informazioni ripristinate nei computer nei quali sono in esecuzione i servizi.

La possibilità di esportare e importare dati di configurazione viene anche utilizzata nella configurazione iniziale di computer che si trovano nella rete perimetrale, ad esempio un server perimetrale. Quando si configura un computer che si trova nella rete perimetrale, è necessario innanzitutto eseguire una replica manuale utilizzando i cmdlet CsConfiguration: sarà necessario esportare i dati di configurazione utilizzando il cmdlet **Export-CsConfiguration** e quindi copiare il file ZIP nel computer nella rete perimetrale. Sarà quindi possibile utilizzare il cmdlet **Import-CsConfiguration** e il parametro LocalStore per importare i dati. È sufficiente effettuare questa operazione una volta e successivamente la replica verrà eseguita automaticamente.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Import-CsConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Oltre a essere un membro di RTCUniversalServerAdmins, per poter eseguire questo cmdlet è altresì necessario essere un amministratore locale oppure avere le autorizzazioni di replicatore della configurazione locale. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsConfiguration"}

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
<td><p><em>ByteInput</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Legge le informazioni della topologia da una matrice di byte archiviata in una variabile. Questa matrice di byte viene creata utilizzando il parametro ByteInput quando si chiama il cmdlet <strong>Export-CsConfiguration</strong>.</p>
<p>Non è possibile utilizzare i parametri ByteInput e FileName nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file ZIP creato da Export-CsConfiguration, ad esempio: -FileName &quot;C:\Config.zip&quot;. Si noti che è necessario includere il parametro FileName o ByteInput, ma non entrambi, quando si chiama il cmdlet <strong>Import-CsConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste che altrimenti verrebbero visualizzate in caso di errore non grave durante l'esecuzione del comando. Per impostare il parametro Force su True, utilizzare la seguente sintassi:</p>
<p>-Force:$True</p></td>
</tr>
<tr class="even">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di copiare i dati di configurazione sul computer locale invece che in archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Import-CsConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Import-CsConfiguration** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Export-CsConfiguration](export-csconfiguration.md)

