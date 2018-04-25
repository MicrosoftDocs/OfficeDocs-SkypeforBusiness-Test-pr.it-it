---
title: Configurare le estensioni del numeri di telefono per il parcheggio chiamata
TOCTitle: Configurare le estensioni del numeri di telefono per il parcheggio chiamata
ms:assetid: fbf97624-9587-42a6-b276-1b69c574a74d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182611(v=OCS.15)
ms:contentKeyID: 49302562
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le estensioni del numeri di telefono per il parcheggio chiamata

 

_**Ultima modifica dell'argomento:** 2012-09-10_

L'applicazione Parcheggio di chiamata utilizza i numeri di interno nella tabella dei codici orbit di Parcheggio di chiamata per parcheggiare le chiamate. È necessario configurare la tabella dei codici orbit di Parcheggio di chiamata con gli intervalli di numeri di interno riservati dall'organizzazione alla chiamate parcheggiate. Questi interni devono essere virtuali (ovvero interni a cui non è assegnato alcun utente o telefono). Ogni pool Lync Server in cui viene distribuita e configurata un'applicazione Parcheggio di chiamata può avere uno o più intervalli di codici orbit. Gli intervalli di codici orbit devono essere univoci nell'intera distribuzione Lync Server.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per utilizzare il Parcheggio di chiamata, è necessario selezionare la casella di controllo <strong>Abilita parcheggio di chiamata</strong> nel criterio vocale. Per impostazione predefinita, questa opzione non è selezionata.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Creare o modificare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)

  - [Eliminare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013](lync-server-2013-delete-a-call-park-orbit-range.md)

