---
title: "Lync Server 2013: Processo di distribuzione per l'applicazione Annuncio"
TOCTitle: Processo di distribuzione per l'applicazione Annuncio
ms:assetid: 72c66249-c4ce-48ce-b1b9-90ebf77d7805
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398545(v=OCS.15)
ms:contentKeyID: 49300958
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per l'applicazione Annuncio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Questa sezione contiene una panoramica dei passaggi necessari per la distribuzione del applicazione Annuncio. È necessario distribuire componenti VoIP aziendale prima di configurare gli annunci. I componenti necessari per il applicazione Annuncio vengono installati e abilitati durante la distribuzione di VoIP aziendale.

### Processo di distribuzione degli annunci

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Ruoli</th>
<th>Documentazione relativa alla distribuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configurazione delle impostazioni degli annunci</p></td>
<td><ul>
<li><p>Creare l'annuncio registrando e caricando file audio o tramite sintesi vocale.</p></li>
<li><p>Configurare gli intervalli di numeri non assegnati nella tabella dei numeri non assegnati e associarli all'annuncio appropriato.</p></li>
</ul></td>
<td><p>RTCUniversalServerAdmins</p>
<p>CsVoiceAdministrator</p>
<p>CsServerAdministrator</p>
<p>CsAdministrator</p>
<p>CsViewOnlyAdministrator</p></td>
<td><p><a href="lync-server-2013-create-an-announcement.md">Creare un annuncio in Lync Server 2013</a></p>
<p><a href="lync-server-2013-configure-the-unassigned-number-table.md">Configurare la tabella dei numeri non assegnati in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Verifica della distribuzione degli annunci</p></td>
<td><p>Testare ascoltando annunci per verificare che la configurazione funzioni nel modo previsto.</p></td>
<td><p>-</p></td>
<td><p><a href="lync-server-2013-optional-verify-announcement-deployment.md">(Facoltativo) Verificare la distribuzione degli annunci in Lync Server 2013</a></p></td>
</tr>
</tbody>
</table>

