---
title: Scenari di esempio sulla configurazione del video
TOCTitle: Scenari di esempio sulla configurazione del video
ms:assetid: da0d61a2-7ac4-4562-bf6a-18473a29acb2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205297(v=OCS.15)
ms:contentKeyID: 49302149
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Scenari di esempio sulla configurazione del video

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In Lync 2013 sono state aggiunte nuove funzionalità video per supportare video ad alta definizione (full HD) da 1920 x 1080 e la visualizzazione Raccolta. Dalle misurazioni basate sui dati dei clienti risulta che in generale la larghezza di banda video non è aumentata in modo significativo rispetto a Lync 2010, mentre è aumentata la larghezza di banda massima del flusso video a causa del supporto full HD. Per informazioni dettagliate, vedere la sezione "Utilizzo della rete per il traffico multimediale" in [Requisiti di larghezza di banda di rete per il traffico multimediale in Lync Server 2013](lync-server-2013-network-bandwidth-requirements-for-media-traffic.md). Gli amministratori possono pertanto limitare la larghezza di banda video per alcuni utenti, ad esempio gli utenti di una succursale con una capacità di rete inferiore, e garantire la migliore qualità video possibile per altri utenti, ad esempio i dirigenti.

Nella tabella seguente viene fornito un elenco di impostazioni consigliate per la configurazione della funzionalità video secondo diverse capacità di rete. In base a queste impostazioni, verranno applicate limitazioni ad alcuni scenari di utenti, per cui non sarà possibile inviare e ricevere video con risoluzione superiore (colonna di estrema destra). Con l'impostazione video minima, la visualizzazione Raccolta non sarà disponibile a causa del valore ridotto per la larghezza di banda massima della rete di ricezione.

### Impostazioni video consigliate

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>-</th>
<th>AllowMultiView</th>
<th>EnableMultiViewJoin</th>
<th>VideoBitRateKB</th>
<th>TotalReceiveVideoBitRateKB</th>
<th>Risoluzione video prevista per una buona qualità video</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ottima</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
<td><p>8000</p></td>
<td><p>8000</p></td>
<td><p>Peer-to-peer: risoluzione video massima da 1920 x 1080</p>
<p>Visualizzazione Raccolta: fino a due video con risoluzione da 1920 x 1080 o più video con risoluzione inferiore</p></td>
</tr>
<tr class="even">
<td><p>Buona</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
<td><p>2500</p></td>
<td><p>2500</p></td>
<td><p>Peer-to-peer: risoluzione video massima da 1280 x 720</p>
<p>Visualizzazione Raccolta: fino a cinque video con risoluzione da 640 x 360</p></td>
</tr>
<tr class="odd">
<td><p>Media</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
<td><p>1000</p></td>
<td><p>1000</p></td>
<td><p>Peer-to-peer: risoluzione video massima da 960 x 540</p>
<p>Visualizzazione Raccolta: fino a cinque video con risoluzione da 424 x 240</p></td>
</tr>
<tr class="even">
<td><p>Minima</p></td>
<td><p>True</p></td>
<td><p>False</p></td>
<td><p>350</p></td>
<td><p>350</p></td>
<td><p>Peer-to-peer: risoluzione video massima da 424 x 240</p>
<p>Visualizzazione Raccolta: non disponibile</p></td>
</tr>
</tbody>
</table>


È possibile utilizzare le informazioni contenute nella tabella precedente per distribuire le nuove funzionalità di videoconferenze in HD e visualizzazione Raccolta per alcuni utenti dell'organizzazione, definendo risoluzioni video diverse per altri utenti.

Nell'esempio seguente l'amministratore distribuisce le nuove funzionalità video con la massima qualità video disponibile solo ai dirigenti. Per i dipendenti di una succursale con capacità di rete ridotta vengono distribuite solo le impostazioni minime descritte nella tabella precedente. Per tutti gli altri dipendenti vengono distribuite le impostazioni di qualità video "Buona" definite nella tabella precedente.

Per la distribuzione delle nuove funzionalità ai dirigenti, l'amministratore crea un criterio di conferenza denominato ExecutiveVideo con le impostazioni seguenti:

  - VideoBitRateKB impostato su 8000 Kbps

  - TotalReceiveVideoBitRateKB impostato su 8000 Kbps

  - AllowMultiview impostato su True

  - EnableMultiviewJoin impostato su True

Per i dipendenti della succursale, l'amministratore crea un criterio di conferenza denominato BranchOfficeVideo con le impostazioni seguenti:

  - VideoBitRateKB impostato su 350 Kbps

  - TotalReceiveVideoBitRateKB impostato su 350 Kbps

  - AllowMultiview impostato su True

  - EnableMultiviewJoin impostato su False

Per tutti gli altri dipendenti, l'amministratore crea un criterio di conferenza denominato StandardVideo con le impostazioni seguenti:

  - VideoBitRateKB impostato su 2500 Kbps

  - TotalReceiveVideoBitRateKB impostato su 2500 Kbps

  - AllowMultiview impostato su True

  - EnableMultiviewJoin impostato su True

L'amministratore assegna i criteri di conferenza agli utenti come indicato di seguito:

  - Il criterio di conferenza ExecutiveVideo viene assegnato ai dirigenti.

  - Il criterio di conferenza BranchOfficeVideo viene assegnato a tutti i dipendenti della succursale.

  - Il criterio di conferenza StandardVideo viene assegnato a tutti gli altri dipendenti.

Queste assegnazioni di criteri di conferenza determinano l'esperienza utente seguente:

  - Tutte le conferenze organizzate da un utente supportano la visualizzazione Raccolta, ma i dipendenti della succursale non possono utilizzare questa funzionalità.

  - Per le conferenze a due o più parti, i dirigenti possono inviare video full HD con risoluzione da 1920 x 1080, se supportata dall'hardware e dal collegamento di rete di cui dispongono, e possono ricevere video full HD con risoluzione 1920 x 1080, se supportata dai client degli altri partecipanti.

  - I dipendenti diversi dai dirigenti usufruiscono di risoluzioni inferiori rispetto ai dirigenti per le conferenze a due o più parti, da dispongono comunque di una buona risoluzione.

  - I dipendenti della succursale usufruiranno di una buona qualità video nelle chiamate a due parti quando in Lync viene visualizzata la finestra video predefinita. Se però si ingrandisce la finestra di Lync a schermo intero, la risoluzione video resterà invariata. Per le conferenze con più utenti, i dipendenti della succursale visualizzeranno solo un video attivo.

