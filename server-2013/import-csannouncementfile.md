---
title: Import-CsAnnouncementFile
TOCTitle: Import-CsAnnouncementFile
ms:assetid: 66da2361-e325-4085-8b6f-47a8423edaab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398472(v=OCS.15)
ms:contentKeyID: 49300819
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsAnnouncementFile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa un file di annuncio nel catalogo audio del servizio annunci. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CSAnnouncementFile -Content <Byte[]> -FileName <String> -Parent <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questi comandi importano un file audio nell'Archivio file del servizio annunci. Poiché i file audio devono essere importati sotto forma di matrici di byte, è necessario innanzitutto chiamare il cmdlet **Get-Content** per recuperare il file audio come matrice di singoli byte. **Get-Content** è un cmdlet predefinito di Windows PowerShell a cui viene passato il nome, incluso il percorso, del file che si desidera utilizzare per l'annuncio. Viene quindi passato il valore 0 al parametro ReadCount per indicare che si desidera leggere il file tutto insieme. Viene quindi passato il valore Byte al parametro Encoding per indicare a **Get-Content** che si desidera avere il contenuto del file sotto forma di matrice di byte. La matrice viene assegnata alla variabile $a.

Nella seconda riga viene chiamato il cmdlet **Import-CsAnnouncementFile** per eseguire effettivamente l'importazione del file. Al parametro Parent viene passata l'identità del servizio ApplicationServer:redmond.litwareinc.com, quindi viene passato un nome al parametro FileName (WelcomeMessage.wav). Questo nome può essere un qualsiasi nome di file valido del sistema operativo Microsoft Windows, ma deve terminare con l'estensione wav o wma. Viene infine passata la variabile $a come valore al parametro Content per leggere la matrice di byte.

    $a = Get-Content ".\GreetingFile.wav" -ReadCount 0 -Encoding Byte
    Import-CsAnnouncementFile -Parent ApplicationServer:redmond.litwareinc.com -FileName "WelcomeMessage.wav" -Content $a

## ESEMPIO 2

L'esempio 2 è identico all'esempio 1, fatta eccezione per il fatto che il comando **Get-Content** è stato incluso tra parentesi come valore del parametro Content invece di essere chiamato separatamente ed essere assegnato a una variabile.

    Import-CsAnnouncementFile -Parent ApplicationServer:redmond.litwareinc.com -FileName "WelcomeMessage.wav" -Content (Get-Content ".\GreetingFile.wav" -ReadCount 0 -Encoding Byte)

## ESEMPIO 3

L'esempio 3 è ancora un'ulteriore variante dell'esempio 1. La differenza è rappresentata dal fatto che in questo caso, anziché utilizzare il parametro Content, viene innanzitutto chiamato il cmdlet **Get-Content** e quindi i risultati vengono inviati tramite pipe a **Import-CsAnnouncementFile**. Questo è il modo più affidabile per importare un file di annuncio da una sessione remota.

    Get-Content ".\GreetingFile.wav" -ReadCount 0 -Encoding Byte | Import-CsAnnouncementFile -Parent ApplicationServer:redmond.litwareinc.com -FileName "WelcomeMessage.wav"

## Descrizione dettagliata

Questo cmdlet importa un file audio sotto forma di matrice di byte nel catalogo audio del servizio annunci. In questo modo il file diventa disponibile per la riproduzione come annuncio per i numeri non assegnati.

Eseguendo questo cmdlet viene importato il file audio nel catalogo. Dopo l'importazione, il file può essere utilizzato in un annuncio chiamando il cmdlet **New-CsAnnouncement** o **Set-CsAnnouncement** e passando il nome del file e il servizio associato come parametri. A questo punto, è possibile chiamare il cmdlet **New-CsUnassignedNumber** o **Set-CsUnassignedNumber** per assegnare l'annuncio a un intervallo di numeri specifico.

I file importati devono essere file WAV o WMA.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Import-CsAnnouncementFile** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Il cmdlet può comunque essere eseguito anche da chiunque disponga dell'accesso in scrittura all'Archivio file del computer di destinazione. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsAnnouncementFile"}

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
<td><p><em>Content</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Il contenuto del file audio sotto forma di matrice di byte.</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome che si desidera assegnare al file nell'Archivio file. Questo nome dovrà essere utilizzato nel parametro AudioFilePrompt nella chiamata al cmdlet <strong>New-CsAnnouncement</strong> o <strong>Set-CsAnnouncement</strong> per assegnare il file a un annuncio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'ID servizio del server applicazioni nel quale è in esecuzione il servizio annunci associato.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, verrebbe visualizzata prima di effettuare modifiche.</p></td>
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

Byte\[\]. Accetta una matrice di byte da un file audio. Tale matrice deve essere inviata tramite pipe come record singolo. Vedere l'esempio 3.

## Tipi restituiti

Questo cmdlet non restituisce un valore.

