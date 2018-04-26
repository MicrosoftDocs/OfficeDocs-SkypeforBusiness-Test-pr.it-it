---
title: Convert-CsUserData
TOCTitle: Convert-CsUserData
ms:assetid: e52f8037-19f3-49c9-8dfc-79b0c27d8b94
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205337(v=OCS.15)
ms:contentKeyID: 49302295
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Convert-CsUserData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Converte i dati utenti esportati nel formato dati utilizzato da Microsoft Lync Server 2010 o da Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Convert-CsUserData -InputFile <String> -OutputFile <String> -TargetVersion <Lync2010 | Current> [-ConfDirectoryFilter <String>] [-Force <SwitchParameter>] [-UserFilter <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 converte i dati utente archiviati nel file C:\\Logs\\Lync2013Data.zip al formato dati utente utilizzato in Lync Server 2010. I dati convertiti vengono archiviati nel file XML C:\\Logs\\Lync2010Data.xml.

    Convert-CsUserData -InputFile "C:\Logs\Lync2013Data.Zip" -OutputFile "C:\Logs\Lync2010Data.xml" -TargetVersion Lync2010

## Esempio 2

Nell'esempio 2 viene illustrato come è possibile convertire i dati per un solo utente, nell'esempio l'utente con l'indirizzo SIP kenmyer@litwareinc.com. A tal fine, viene incluso il parametro UserFilter seguito dall'indirizzo SIP dell'utente (senza il prefisso sip:).

    Convert-CsUserData -InputFile "C:\Logs\Lync2013Data.Zip" -OutputFile "C:\Logs\Lync2010data.xml" -TargetVersion Lync2010 -UserFilter "kenmyer@litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Convert-CsUserData** accetta i dati esportati utilizzando il cmdlet [Export-CsUserData](export-csuserdata.md) e quindi li converte nel formato utilizzato da Microsoft Lync Server 2010 o da Lync Server 2013. Questo consente inoltre al cmdlet **Import-CsUserData** di importare tali dati nella versione appropriata di Lync Server.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Convert-CsUserData"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Convert-CsUserData** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>InputFile</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file ZIP o XML contenente i dati utente da convertire. Ad esempio:</p>
<p>-InputFile “C:\Data\Lync2010.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>OutputFile</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file in cui verranno archiviati i dati convertiti. Se si emettono i dati utilizzando il formato Microsoft Lync Server 2010, il file di output deve utilizzare un'estensione di file XML, ad esempio:</p>
<p>-OutputFile &quot;C:\Data\ConvertedLync2010Data.xml&quot;</p>
<p>Se si utilizza il formato Lync Server 2013, il file di output deve utilizzare un'estensione di file ZIP:</p>
<p>-OutputFile &quot;C:\Data\ConvertedLyncData.zip&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetVersion</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.BlobStore.Cmdlets.ConvertTarget</p></td>
<td><p>Indica il formato per i dati convertiti. I valori consentiti sono:</p>
<p>Lync2010</p>
<p>Corrente</p></td>
</tr>
<tr class="even">
<td><p><em>ConfDirectoryFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di convertire i dati della directory conferenze. A tal fine, includere il parametro ConfDirectoryFilter e specificare l'identità della directory conferenze:</p>
<p>-ConfDirectoryFilter 13</p>
<p>È possibile recuperare le identità della directory conferenze utilizzando il comando seguente:</p>
<p>Get-CsConferenceDirectory | Select-Object Identity, ServiceId</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>UserFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di convertire i dati per un solo utente. Tale utente viene specificato mediante il relativo indirizzo SIP, senza prefisso sip:. Ad esempio:</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Convert-CsUserData** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Convert-CsUserData** crea file XML o ZIP, a seconda che i dati convertiti siano utilizzati con Lync Server 2010 o con Lync Server 2013.

## Vedere anche

#### Ulteriori risorse

[Export-CsUserData](export-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

