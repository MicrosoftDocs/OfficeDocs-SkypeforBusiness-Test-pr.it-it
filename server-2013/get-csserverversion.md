---
title: Get-CsServerVersion
TOCTitle: Get-CsServerVersion
ms:assetid: 66af07c0-fdfe-491a-ad48-b8821fb58904
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398470(v=OCS.15)
ms:contentKeyID: 49300815
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsServerVersion

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle licenze server per un computer in cui è in esecuzione Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsServerVersion

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono restituite le informazioni sulla licenza per il computer locale. Questo è l'unico modo in cui è possibile usare il cmdlet **Get-CsServerVersion**.

    Get-CsServerVersion

## Descrizione dettagliata

Lync Server è disponibile in due versioni diverse: una versione di valutazione (con scadenza) e una versione con licenza completa. Il cmdlet **Get-CsServerVersion** consente agli amministratori di determinare la versione di Lync Server in esecuzione in un computer. Il cmdlet **Get-CsServerVersion**, progettato esclusivamente per l'esecuzione nel computer locale senza alcun parametro aggiuntivo, tenta di leggere il valore del Registro di sistema HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Real-Time Communications\\{A593FD00-64F1-4288-A6F4-E699ED9DCA35}\\Type. Sulla base di tale valore del Registro di sistema, il cmdlet restituisce il numero di versione del software e le informazioni sulla licenza di Lync Server. I dati sulla licenza forniscono una delle informazioni seguenti:

È stato installato il codice di licenza di valutazione.

È stato installato il codice per contratti multilicenza.

Non è richiesto un codice di licenza per i componenti installati sul computer locale. La licenza è necessaria solo per i computer che svolgono il ruolo di Front End Server, Server Director o server perimetrale.

Se si verifica un errore, il cmdlet **Get-CsServerVersion** segnalerà che il tipo di licenza e le informazioni sulla versione non possono essere recuperati e consiglierà di reinstallare i componenti di Lync Server.

Si noti che con Get-CsServerVersion viene restituito solo il numero della versione di base. Ad esempio, con Get-CsServerVersion verrà restituito un valore quale 5.0.8308 anche se in seguito a un aggiornamento il numero di versione è cambiato in 5.0.8308.291. Se è necessaria una versione molto specifica, è necessario utilizzare il Pannello di controllo di Windows.

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
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsServerVersion** non supporta l'input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsServerVersion** restituisce un valore stringa.

