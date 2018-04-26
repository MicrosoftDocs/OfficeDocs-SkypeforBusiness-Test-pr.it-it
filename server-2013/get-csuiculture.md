---
title: Get-CsUICulture
TOCTitle: Get-CsUICulture
ms:assetid: b8df7083-068b-4d5e-a9b4-448602de6586
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412900(v=OCS.15)
ms:contentKeyID: 49301779
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUICulture

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni cultura (ovvero sulle impostazioni internazionali e della lingua) utilizzate da Lync Server Management Shell. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUICulture

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce le informazioni di base sulle impostazioni cultura attualmente utilizzate da Lync Server Management Shell.

    Get-CsUICulture

## Descrizione dettagliata

Sebbene Lync Server sia disponibile in diverse lingue, questo software non può essere definito un'applicazione MUI (Multilingual User Interface, interfaccia utente multilingue) vera e propria. Tra l'altro, questo significa che l'interfaccia utente di Lync Server Management Shell non cambia la lingua ogni volta che si cambia la lingua del sistema operativo. Si supponga ad esempio di aver installato la versione in inglese americano di Lync Server e che anche il sistema operativo Windows sia nella stessa lingua. Se nel sistema operativo si modificano le impostazioni cultura, ovvero le impostazioni internazionali e della lingua, applicando il danese, la modifica non verrà estesa automaticamente a Lync Server Management Shell. L'interfaccia utente di Lync Server Management Shell, inclusi i messaggi di errore e il testo della Guida, continuerà a essere visualizzata in inglese americano. Per modificare le impostazioni cultura di Lync Server Management Shell, è necessario eseguire il cmdlet **Set-CsUICulture**.

Il cmdlet **Get-CsUICulture** consente di determinare le impostazioni cultura attualmente in uso in Lync Server Management Shell.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsUICulture** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Questo cmdlet fornisce unicamente parametri comuni di Windows PowerShell.</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsUICulture** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsUICulture** restituisce istanze della classe System.Globalization.CultureInfo.

## Vedere anche

#### Ulteriori risorse

[Set-CsUICulture](set-csuiculture.md)

