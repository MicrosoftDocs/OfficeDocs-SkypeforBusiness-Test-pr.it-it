---
title: Set-CsCallParkServiceMusicOnHoldFile
TOCTitle: Set-CsCallParkServiceMusicOnHoldFile
ms:assetid: af5e7573-4bfd-47b1-a92b-83b06a537158
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412836(v=OCS.15)
ms:contentKeyID: 49301672
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCallParkServiceMusicOnHoldFile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica il file audio riprodotto ai chiamanti in attesa per una chiamata parcheggiata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsCallParkServiceMusicOnHoldFile -Content <Byte[]> -Service <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene impostato il file SoothingMusic.wma come file audio riprodotto ai chiamanti le cui chiamate vengono parcheggiate. La prima riga dell'esempio è una chiamata al cmdlet **Get-Content**. Questo cmdlet legge semplicemente il contenuto di un file e lo assegna in questo caso alla variabile $a. Poiché viene passato un valore di 0 al parametro ReadCount, il cmdlet **Get-Content** legge l'intero file in una sola volta anziché tentare di leggerlo riga per riga, operazione non applicabile a un file audio. Il parametro Encoding viene impostato su byte. In questo modo si comunica al cmdlet **Get-Content** che il contenuto da leggere nella variabile $a è una matrice di byte, anziché un file audio in formato wma.

Nella riga 2 dell'esempio viene effettivamente assegnato il file audio. Viene chiamato il cmdlet **Set-CsCallParkServiceMusicOnHoldFile** e viene specificato l'ID di servizio in cui è in esecuzione il servizio di parcheggio di chiamata. Viene quindi passato al parametro Content il contenuto del file audio letto nella variabile $a. Questo contenuto deve essere nel formato byte.

    $a = Get-Content -ReadCount 0 -Encoding byte "C:\MoHFiles\soothingmusic.wma"
    Set-CsCallParkServiceMusicOnHoldFile -Service ApplicationServer:pool0.litwareinc.com -Content $a

## Descrizione dettagliata

Il parcheggio di chiamata è un servizio che consente a un utente di "parcheggiare" una telefonata in arrivo. Il parcheggio trasferisce una chiamata a un numero in un intervallo specificato e lo mette immediatamente in attesa. A seconda delle impostazioni di configurazione del servizio di parcheggio di chiamata, è possibile che mentre la chiamata è parcheggiata il chiamante ascolti una musica di attesa. Utilizzare questo cmdlet per cambiare il file audio (musica di attesa) riprodotto a un chiamante parcheggiato in attesa.

La musica di attesa viene riprodotta solo se la proprietà EnableMusicOnHold del servizio di parcheggio di chiamata è stata impostata su True. Per controllare questa proprietà, è possibile chiamare il cmdlet **Get-CsCpsConfiguration**. La proprietà può essere impostata sia durante la creazione della configurazione di parcheggio di chiamata con il cmdlet **New-CsCpsConfiguration** sia dopo aver creato la configurazione di parcheggio di chiamata chiamando il cmdlet **Set-CsCpsConfiguration**. Il valore di questa proprietà è True per impostazione predefinita.

Lync Server viene fornito con un file predefinito per la musica di attesa del servizio di parcheggio di chiamata. Se non si assegna un file audio, viene utilizzato il file predefinito.

I file audio devono essere nel formato seguente: Windows Media Audio 9, 44 kHz, 16 bit, Mono, CBR o 32 kbps.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsCallParkServiceMusicOnHoldFile** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCallParkServiceMusicOnHoldFile"}

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
<td><p>Il contenuto del file audio in formato byte.</p>
<p>Utilizzare il cmdlet <strong>Get-Content</strong> per recuperare il contenuto del file audio in formato byte. Per informazioni dettagliate, vedere la sezione relativa agli esempi in questo argomento.</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>ID del servizio in cui si trova il servizio di parcheggio di chiamata, ad esempio ApplicationServer:pool0.litwareinc.com.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Byte\[\]. Accetta l'input da pipeline di una matrice di byte contenente il file della musica di attesa.

## Tipi restituiti

Questo cmdlet non restituisce un valore.

## Vedere anche

#### Ulteriori risorse

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Remove-CsCpsConfiguration](remove-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)

