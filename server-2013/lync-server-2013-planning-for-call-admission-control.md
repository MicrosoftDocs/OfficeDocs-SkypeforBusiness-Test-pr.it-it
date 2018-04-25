---
title: 'Lync Server 2013: Pianificazione del servizio Controllo di ammissione di chiamata'
TOCTitle: Pianificazione del servizio Controllo di ammissione di chiamata
ms:assetid: ca367138-adf5-4119-bc40-5ddf335ed22f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398842(v=OCS.15)
ms:contentKeyID: 49301983
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione del servizio Controllo di ammissione di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Per le applicazioni per comunicazioni unificate basate sul protocollo IP, ad esempio la telefonia, le comunicazioni video e la condivisione di applicazioni, la larghezza di banda disponibile delle reti aziendali non è considerata generalmente un fattore di limitazione negli ambienti LAN. Nei collegamenti WAN tra i siti tuttavia la larghezza di banda della rete può essere limitata. Quando si verifica un eccesso di sottoscrizione di un collegamento WAN da parte del traffico di rete, per risolvere il problema di congestione vengono utilizzati i meccanismi correnti, ad esempio l'accodamento, il buffering e l'eliminazione dei pacchetti. Il traffico in eccesso in genere viene ritardato finché non si risolve la congestione di rete o, se necessario, finché non viene eliminato il traffico. Per il traffico di dati convenzionali, in questi casi è possibile ripristinare il client di ricezione. Per il traffico in tempo reale, ad esempio le comunicazioni unificate, non è possibile risolvere la congestione in questo modo, poiché questo tipo di traffico è sensibile sia alla latenza che alla perdita di pacchetti. La congestione nella WAN può determinare una qualità percepita dagli utenti (QoE) scadente. Per il traffico in tempo reale in condizioni di congestione, è meglio rifiutare le chiamate anziché consentire connessioni di qualità scadente.

Il Servizio Controllo di ammissione di chiamata determina se è disponibile una larghezza di banda di rete sufficiente per stabilire una sessione in tempo reale di qualità accettabile. In Lync Server 2013 questo servizio verifica il traffico in tempo reale solo per le comunicazioni audio e video, ma non influisce sul traffico dei dati. Se il percorso WAN predefinito non dispone della larghezza di banda necessaria, il servizio Controllo di ammissione di chiamata può tentare di instradare la chiamata tramite un percorso Internet o la rete PSTN (Public Switched Telephone Network). Questo servizio è disponibile solo in Lync Server.

In questa sezione viene descritta la funzionalità di Controllo di ammissione di chiamata e viene illustrata la relativa pianificazione.


> [!NOTE]
> Lync Server include tre funzionalità VoIP aziendale avanzate: Controllo di ammissione di chiamata, servizi di emergenza (E9-1-1) e bypass multimediale. Per una panoramica delle informazioni sulla pianificazione comuni a tutte e tre le funzionalità, vedere <A href="lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md">Impostazioni di rete per le funzionalità di VoIP aziendale avanzate in Lync Server 2013</A>.



## Argomenti della sezione

  - [Panoramica del controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-overview-of-call-admission-control.md)

  - [Definizione dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-defining-your-requirements-for-call-admission-control.md)

  - [Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md)

  - [Componenti e topologie per il servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-components-and-topologies-for-cac.md)

  - [Procedure consigliate per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-best-practices-for-call-admission-control.md)

  - [Elenco di controllo di distribuzione per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-deployment-checklist-for-call-admission-control.md)

