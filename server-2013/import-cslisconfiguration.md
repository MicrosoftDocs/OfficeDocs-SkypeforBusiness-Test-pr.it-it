---
title: Import-CsLisConfiguration
TOCTitle: Import-CsLisConfiguration
ms:assetid: 579c0c38-311b-4961-b924-11731403d9f2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398380(v=OCS.15)
ms:contentKeyID: 49300630
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsLisConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa una configurazione del servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1) di VoIP aziendale da un file di backup. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CsLisConfiguration -FileName <String> <COMMON PARAMETERS>

    Import-CsLisConfiguration -ByteInput <Byte[]> <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

Con questo esempio la configurazione del servizio di chiamate di emergenza viene importata dal file di backup denominato E911Config.back al database di configurazione delle posizioni.

    Import-CsLisConfiguration -FileName C:\E911Config.bak

## ESEMPIO 2

Con l'esempio 2 viene dimostrato come utilizzare il parametro ByteInput del cmdlet **Import-CsLisConfiguration**. Nella riga 1 è mostrata una chiamata al cmdlet **Export-CsLisConfiguration** con il parametro AsBytes. L'output del comando è un array di byte contenente la configurazione LIS. L'array viene assegnato alla variabile $lisconfig. Nella riga 2 viene chiamato il cmdlet **Import-CsLisConfiguration**. Il parametro ByteInput riceve il valore di $lisconfig, vale a dire la variabile contenente l'array di byte esportato. Tale array di byte sarà reimportato nel database di configurazione delle posizioni.

    $lisconfig = Export-CsLisConfiguration -AsBytes 
    Import-CsLisConfiguration -ByteInput $lisconfig

## ESEMPIO 3

L'esempio 3 è una versione più completa dell'esempio 2. La prima riga è la stessa e chiama il cmdlet **Export-CsLisConfiguration** con il parametro AsBytes per archiviare la configurazione LIS come matrice di byte nella variabile $lisconfig. Nella parte rimanente dell'esempio viene mostrato come salvare tale configurazione in un file per importarla successivamente nel database di configurazione delle posizioni.

Nella riga 2 il contenuto di $lisconfig, vale a dire la matrice di byte che rappresenta la configurazione LIS, viene inviato tramite pipe al cmdlet **Set-Content** di Windows PowerShell. Vengono assegnati valori a due parametri del cmdlet **Set-Content**, ovvero Path ed Encoding. Al parametro Path vengono assegnati il percorso completo e il nome del file in cui si desidera salvare la configurazione. Il parametro Encoding invece viene utilizzato con un valore di byte per garantire che la configurazione venga archiviata come matrice di byte.

Per finire, nella riga 3, la configurazione viene importata di nuovo nel database di configurazione delle posizioni. È innanzitutto necessario chiamare il cmdlet **Get-Content** per recuperare il contenuto del file. Viene passato il valore 0 alla proprietà ReadCount, che indica al cmdlet **Get-Content** di leggere tutto il contenuto del file in una sola operazione anziché una riga per volta. Viene utilizzato nuovamente il parametro Encoding con un valore di byte per specificare il tipo di dati da leggere dal file. Viene infine passato il nome del file al parametro Path. Il contenuto del file letto con il cmdlet **Get-Content** viene inviato tramite pipe al cmdlet **Import-CsLisConfiguration**, che importa la configurazione salvata nel database di configurazione delle posizioni.

    $lisconfig = Export-CsLisConfiguration -AsBytes
    $listconfig | Set-Content -Path C:\E911Config.bak -Encoding byte
    Get-Content -ReadCount 0 -Encoding byte -Path C:\E911Config.bak | Import-CsLisConfiguration

## Descrizione dettagliata

L'implementazione del servizio per chiamate di emergenza in un'organizzazione può, a seconda delle dimensioni dell'organizzazione stessa, comportare il mapping di migliaia di subnet, porte, commutatori e punti di accesso wireless alle posizioni. Una configurazione del servizio per chiamate di emergenza include inoltre informazioni sul server Informazioni percorso fornite dal provider di routing di rete del servizio per chiamate di emergenza, sulle posizioni e sugli indirizzi civici e sulla relativa convalida. Dato il volume di informazioni e impostazioni necessarie per implementare il servizio per chiamate di emergenza, è consigliabile eseguire regolarmente il backup dell'intera configurazione. È possibile eseguire il backup dell'intera configurazione del servizio per chiamate di emergenza in un file chiamando il cmdlet **Export-CsLisConfiguration**. Con la chiamata al cmdlet **Import-CsLisConfiguration** è possibile ripristinare la configurazione da quel file.

Il ripristino della configurazione con una chiamata a questo cmdlet non sovrascrive la configurazione esistente. Inserisce le informazioni che sono state rimosse, ma non rimuove i record esistenti aggiunti dopo la creazione del file di backup.

IMPORTANTE: poiché l'importazione dal backup non sostituisce i record esistenti, gli eventuali record modificati saranno ripristinati e potrebbero risultare alcune posizioni orfane. Ad esempio, si supponga di avere definito un punto di accesso wireless (WAP) con la proprietà Location impostata sul valore Building30/Room10. Viene quindi chiamato il cmdlet **Export-CsLisConfiguration** per eseguire il backup della configurazione. In un secondo momento, la proprietà Location di tale punto di accesso wireless viene modificata in Building30/Rooms20-40. Se si chiama il cmdlet **Import-CsLisConfiguration** per ripristinare la configurazione di backup, la posizione del punto di accesso wireless sarà Building30/Room10 (quella precedente al backup), ma nel database di configurazione delle posizioni rimarrà la posizione per Building30/Rooms20-40.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Import-CsLisConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsLisConfiguration"}

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
<td><p>Il valore passato a questo parametro è una variabile contenente un array di byte della configurazione LIS creata dal cmdlet <strong>Export-CsLisConfiguration</strong> con il parametro AsBytes.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome del file di backup da cui importare la configurazione. Non è possibile specificare sia FileName sia ByteInput. In ogni chiamata a questo cmdlet è possibile utilizzare solo uno dei due parametri.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Byte\[\]. Accetta un array di byte da una configurazione LIS esportata. L'array di byte deve essere inviato tramite pipe come record singolo. Vedere l'esempio 3.

## Tipi restituiti

Questo cmdlet non restituisce un valore.

## Vedere anche

#### Ulteriori risorse

[Export-CsLisConfiguration](export-cslisconfiguration.md)  
[Publish-CsLisConfiguration](publish-cslisconfiguration.md)  
[Unpublish-CsLisConfiguration](unpublish-cslisconfiguration.md)  
[Debug-CsLisConfiguration](debug-cslisconfiguration.md)  
[Test-CsLisConfiguration](test-cslisconfiguration.md)

