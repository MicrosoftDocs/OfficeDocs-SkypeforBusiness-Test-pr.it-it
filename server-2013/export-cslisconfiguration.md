---
title: Export-CsLisConfiguration
TOCTitle: Export-CsLisConfiguration
ms:assetid: 714bd67e-4cd6-4066-a065-59f7e079b6ad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398539(v=OCS.15)
ms:contentKeyID: 49300938
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsLisConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esporta una configurazione del servizio di chiamate di emergenza (E9-1-1) di VoIP aziendale in un file in formato compresso a fini di backup. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Export-CsLisConfiguration -FileName <String> <COMMON PARAMETERS>

    Export-CsLisConfiguration [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

Con questo esempio viene esportata l'intera configurazione del servizio di chiamate di emergenza da Location Information Server (LIS) al file di backup denominato E911Config.bak.

    Export-CsLisConfiguration -FileName C:\E911Config.bak

## ESEMPIO 2

Con questo esempio la configurazione LIS viene archiviata come array di byte in una variabile, $lisconfig.

    $lisconfig = Export-CsLisConfiguration -AsBytes

## ESEMPIO 3

L'esempio 3 è una versione più completa dell'esempio 2. La prima riga è la stessa e chiama il cmdlet **Export-CsLisConfiguration** con il parametro AsBytes per archiviare la configurazione LIS come matrice di byte nella variabile $lisconfig. Nella parte rimanente dell'esempio viene mostrato come salvare tale configurazione in un file per importarla successivamente nel database di configurazione delle posizioni.

Nella riga 2 il contenuto di $lisconfig, ovvero la matrice di byte che rappresenta la configurazione LIS, viene inviato tramite pipe al cmdlet **Set-Content** di Windows PowerShell. Vengono assegnati valori ai due parametri del cmdlet **Set-Content**, Path ed Encoding. Viene assegnato il percorso completo e il nome del file in cui si desidera salvare la configurazione al parametro Path. Viene utilizzato quindi il parametro Encoding con un valore byte per garantire che la configurazione venga archiviata come matrice di byte.

Nella riga 3 infine viene importata di nuovo la configurazione nel database di configurazione delle posizioni. È necessario innanzitutto chiamare il cmdlet **Get-Content** per recuperare il contenuto dal file. Viene passato il valore 0 alla proprietà ReadCount, che comunica al cmdlet **Get-Content** di leggere tutto il contenuto del file in una sola operazione anziché una riga per volta. Viene utilizzato di nuovo il parametro Encoding con un valore byte per specificare il tipo di dati da leggere nel file. Al termine viene passato il nome del file al parametro Path. Il contenuto del file letto con il cmdlet **Get-Content** viene inviato tramite pipe al cmdlet **Import-CsLisConfiguration**, che importa la configurazione salvata nel database delle posizioni.

    $lisconfig = Export-CsLisConfiguration -AsBytes
    $lisconfig | Set-Content -Path C:\E911Config.bak -Encoding byte
    Get-Content -ReadCount 0 -Encoding byte -Path C:\E911Config.bak  | Import-CsLisConfiguration

## Descrizione dettagliata

L'implementazione del servizio di chiamate di emergenza in un'organizzazione può, a seconda delle dimensioni dell'organizzazione stessa, coinvolgere il mapping di migliaia di subnet, porte, switch e punti di accesso wireless alle posizioni. Una configurazione del servizio di chiamate di emergenza include anche informazioni sui servizi Web forniti dal provider di routing di rete del servizio di chiamate di emergenza, e sulle posizioni e sugli indirizzi civici e sulla relativa convalida. Dato il volume di informazioni e impostazioni richieste per implementare il servizio di chiamate di emergenza, è consigliabile eseguire regolarmente il backup dell'intera configurazione. È possibile utilizzare questo cmdlet per eseguire il backup della configurazione del servizio di chiamate di emergenza in un file, salvando l'intera configurazione in formato compresso. Per ripristinare la configurazione, chiamare il cmdlet **Import-CsLisConfiguration**.

Con questo cmdlet viene creato un nuovo file di backup, senza sovrascrivere un file esistente. Di conseguenza, il nome file specificato nella chiamata a questo cmdlet non può corrispondere al nome di un file esistente.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Export-CsLisConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsLisConfiguration"}

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
<td><p>Il percorso e il nome del file in cui si desidera salvare la configurazione. Non può corrispondere al nome di un file esistente.</p>
<p>Se si specifica un valore per il parametro AsBytes, non è possibile specificare un valore anche per il parametro FileName. Se si accede a questo cmdlet in remoto è necessario utilizzare AsBytes al posto di FileName.</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di restituire la configurazione come array di byte. L'output del comando dovrebbe essere assegnato a una variabile per una successiva importazione. Se non si assegna l'output a una variabile, l'array di byte che rappresenta la configurazione scorrerà nella finestra di Lync Server Management Shell. Non è possibile specificare entrambi i parametri AsBytes e FileName; è possibile utilizzarne solo uno in ogni chiamata a questo cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di restituire un array di byte (Byte\[\]) se viene utilizzato il parametro AsBytes.

## Vedere anche

#### Ulteriori risorse

[Import-CsLisConfiguration](import-cslisconfiguration.md)  
[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

