---
title: 'Lync Server 2013: Opzioni di distribuzione SIP diretta'
TOCTitle: Opzioni di distribuzione SIP diretta
ms:assetid: 84691944-03f2-4a89-9f2b-1ab3d7f388cc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398672(v=OCS.15)
ms:contentKeyID: 49301191
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Opzioni di distribuzione SIP diretta in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento vengono illustrate topologie di esempio per la distribuzione di connessioni SIP dirette.

## Lync Server autonomo

Se nell'organizzazione viene utilizzata una delle distribuzioni descritte in questa sezione, è possibile utilizzare il Lync Server 2013 come soluzione di telefonia unica per l'intera organizzazione o parte di essa. In questa sezione vengono descritte in modo dettagliato le distribuzioni seguenti:

  - **Distribuzione incrementale:** questa opzione presuppone la presenza di un'infrastruttura PBX già esistente e l'introduzione incrementale di VoIP aziendale per piccoli gruppi o team all'interno dell'organizzazione.

  - **Distribuzione di Lync Server solo VoIP:** questa opzione presuppone la distribuzione di VoIP aziendale in un sito senza un'infrastruttura di telefonia tradizionale.

## Distribuzione incrementale

Nella distribuzione incrementale Lync Server 2013 è l'unica soluzione di telefonia per singoli team o reparti, mentre gli altri utenti di un'organizzazione continuano a utilizzare un sistema PBX. Questa strategia di distribuzione incrementale consente di introdurre la telefonia IP nell'organizzazione tramite programmi pilota controllati. I gruppi di lavoro le cui esigenze di comunicazione vengono soddisfatte meglio da una soluzione Microsoft Unified Communications vengono spostati a VoIP aziendale, mentre gli altri utenti rimangano nel sistema PBX esistente. È possibile eseguire la migrazione di altri gruppi di lavoro a VoIP aziendale, se necessario.

L'opzione incrementale è consigliata se sono stati chiaramente definiti gruppi di utenti con requisiti di comunicazione in comune e che si prestano a una gestione centralizzata. Questa opzione è anche efficace se sono presenti team o reparti dislocati in aree geografiche estese, per i quali il risparmio sulle spese per le chiamate interurbane può essere significativo. Questa opzione è di fatto utile per la creazione di team virtuali, i cui membri possono essere dislocati in tutto il mondo. È possibile creare, modificare o eliminare tali team per rispondere rapidamente ai cambiamenti dei requisiti aziendali.

Nella figura seguente viene illustrata la topologia generica per la distribuzione di VoIP aziendale controllato da un sistema PBX. SI tratta della topologia consigliata per la distribuzione incrementale.

**Opzione di distribuzione incrementale**

![Diagramma dell'opzione di migrazione dipartimentale (di reparto)](images/Gg398672.e951ecf4-7cd2-425a-9106-76977492d682(OCS.15).jpg "Diagramma dell'opzione di migrazione dipartimentale (di reparto)")


> [!NOTE]
> Se si connette la distribuzione di Lync Server a un partner SIP diretto certificato, non è necessario un gateway PSTN tra Mediation Server e il sistema PBX. Per un elenco di partner SIP diretti certificati, vedere il sito Web relativo al programma Microsoft Unified Communications Open Interoperability Program all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=203309">http://go.microsoft.com/fwlink/p/?linkId=203309</A>.




> [!NOTE]
> Per il percorso multimediale illustrato in questa figura è abilitata la possibilità di ignorare Mediation Server (Media Bypass) (configurazione consigliata). Se si sceglie di disabilitare Media Bypass, il percorso multimediale viene instradato tramite Mediation Server.



In questa topologia i reparti o i gruppi di lavoro selezionati sono abilitati per VoIP aziendale. Un gateway PSTN provvede a collegare al PBX il gruppo di lavoro abilitato per VoIP. Gli utenti abilitati per VoIP aziendale, inclusi i lavoratori remoti, comunicano attraverso la rete IP. Le chiamate da parte degli utenti di VoIP aziendale alla rete PSTN e ai collaboratori non abilitati per VoIP aziendale vengono instradate al gateway PSTN appropriato. Le chiamate dai colleghi ancora nel sistema PBX o da chiamanti nella rete PSTN vengono instradate al gateway PSTN, che le inoltra a Lync Server per il routing.

Vi sono due configurazioni consigliate per la connessione di VoIP aziendale a un'infrastruttura PBX esistente per garantire l'interoperabilità: VoIP aziendale controllato dal sistema PBX e il sistema PBX controllato da VoIP aziendale.

## VoIP aziendale controllato dal sistema PBX

Quando VoIP aziendale viene distribuito in modo da essere controllato dal sistema PBX, tutte le chiamate dalla rete PSTN arrivano al sistema PBX, da cui le chiamate per gli utenti di VoIP aziendale vengono instradate a un gateway PSTN, mentre quelle per gli utenti del sistema PBX vengono instradate al sistema PBX.

## Sistema PBX controllato da VoIP aziendale

Quando VoIP aziendale viene distribuito in modo da controllare il sistema PBX, tutte le chiamate arrivano al gateway PSTN, da cui le chiamate per gli utenti di VoIP aziendale vengono instradate a Lync Server, mentre quelle per gli utenti del sistema PBX vengono instradate al sistema PBX. Le chiamate alla rete PSTN, sia dagli utenti di VoIP aziendale che dagli utenti del sistema PBX vengono instradate tramite la rete IP al gateway più conveniente. Nella tabella seguente sono illustrati i vantaggi e gli svantaggi di questa configurazione.

### Vantaggi e svantaggi della distribuzione di un sistema PBX controllato da VoIP aziendale

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Vantaggi</th>
<th>Svantaggi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Il sistema PBX continua a essere utilizzato da tutti gli utenti non abilitati per VoIP aziendale.</p></td>
<td><p>I gateway esistenti potrebbero non supportare le funzionalità o le caratteristiche desiderate.</p></td>
</tr>
<tr class="even">
<td><p>Il sistema PBX gestisce tutti i dispositivi di versioni precedenti.</p></td>
<td><p>È necessario un trunk dal gateway al sistema PBX e dal gateway a Mediation Server. Potrebbero essere necessari più trunk dal provider di servizi.</p></td>
</tr>
<tr class="odd">
<td><p>Gli utenti di VoIP aziendale mantengono gli stessi numeri di telefono.</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## Distribuzione di Lync Server solo VoIP

VoIP aziendale offre alle nuove aziende o anche ai nuovi uffici di aziende esistenti la possibilità di implementare una soluzione VoIP completa senza doversi preoccupare dell'integrazione del sistema PBX o dover sostenere costi sostanziali per la distribuzione e la manutenzione di un'infrastruttura IP-PBX. Questa soluzione supporta sia i lavoratori sul posto che quelli remoti.

In questa distribuzione tutte le chiamate vengono instradate attraverso la rete IP. Le chiamate alla rete PSTN vengono instradate al gateway PSTN appropriato. Lync 2013 o Lync Phone Edition funge da softphone. Il controllo delle chiamate remote non è disponibile e non è necessario in quanto non vi sono telefoni PBX da controllare. I servizi di segreteria telefonica e operatore automatico sono disponibili tramite la distribuzione facoltativa della Messaggistica unificata di Exchange.


> [!NOTE]
> Oltre all'infrastruttura di rete necessaria per supportare Lync Server 2013, una distribuzione solo VoIP può utilizzare un gateway qualificato di piccole dimensioni per il supporto di fax e dispositivi analogici.



Nella figura seguente viene illustrata una topologia tipica per una distribuzione solo VoIP.

**Opzione di distribuzione solo VoIP**

![Opzione di distribuzione vergine](images/Gg398672.820dc5fe-0e20-431b-ae4e-fefdf2221d3b(OCS.15).jpg "Opzione di distribuzione vergine")


> [!NOTE]
> Per il percorso multimediale illustrato in questa figura è abilitata la possibilità di ignorare Mediation Server (Media Bypass) (configurazione consigliata). Se si sceglie di disabilitare Media Bypass, il percorso multimediale viene instradato tramite Mediation Server.


