---
title: Test della scalabilità
TOCTitle: Test della scalabilità
ms:assetid: bf41bac6-d4ec-4de6-9a44-a82d01a87279
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205226(v=OCS.15)
ms:contentKeyID: 49301832
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test della scalabilità

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Lync Server 2013 offre l'infrastruttura server per tutte le comunicazioni in tempo reale di Lync Server, tra cui la messaggistica istantanea e la presenza, le conferenze e VoIP aziendale. Sono incluse le eventuali funzionalità che utilizzano le risorse hardware di un pool di Lync Server 2013 e che pertanto incidono sulle prestazioni e sul dimensionamento. Non tutte le organizzazioni si avvalgono di tutte le funzionalità nello stesso modo.

Alcune organizzazioni ad esempio possono utilizzare molto frequentemente i video nelle conferenze, mentre altre possono utilizzarli raramente o addirittura non utilizzarli affatto. Alcune organizzazioni preferiscono la condivisione delle diapositive di PowerPoint alla condivisione delle applicazioni, mentre altre preferiscono il contrario. Le organizzazioni che distribuiscono VoIP aziendale possono fare un uso più o meno intenso dell'applicazione Response Group. La maggior parte delle organizzazioni distribuisce Monitoring Server, ma non molte di esse distribuiscono server di archiviazione. Le organizzazioni inoltre non dispongono tutte delle stesse infrastrutture, anche in termini di capacità hardware, capacità di rete e numero e dimensione dei pool distribuiti. La diversità di funzionalità e infrastrutture pone una sfida ai fini del testing della scalabilità, in quanto non si riescono a simulare tutte le combinazioni di funzionalità e infrastrutture possibili.

Per determinare il supporto della scalabilità per Lync Server, il testing viene eseguito utilizzando tutte le funzionalità di Lync Server contemporaneamente sulla base di un modello di utilizzo (modello utente) medio. Per definire un modello utente appropriato per i carichi di lavoro di Lync Server, vengono analizzati numerosi punti dati, tra cui i sondaggi svolti presso i clienti, i commenti e suggerimenti provenienti dal programma Analisi utilizzo software Microsoft, i dati relativi all'utilizzo di Lync Server forniti dal reparto IT Microsoft e i dati ottenuti tramite data mining dal servizio Live Meeting. In molti casi il modello utente tende a preferire i carichi più pesanti in modo da lasciare un margine adeguato per l'utilizzo all'interno di un'organizzazione.

Nei test di scalabilità eseguiti i pool di Lync Server 2013 vengono impostati secondo le specifiche hardware e software consigliate, inclusi i componenti di infrastruttura come Servizi di dominio Active Directory, i dispositivi di bilanciamento del carico hardware e i firewall. Gli ambienti Lync Server inoltre vengono impostati in modo da somigliare il più possibile agli ambienti reali tipici. Viene quindi utilizzato lo strumento Lync Server 2013 Stress and Performance Tool per simulare i carichi di Lync Server 2013 in base al modello utente.

Vengono eseguite più iterazioni dei test di scalabilità, incluse più esecuzioni di prova della durata di tre settimane. I risultati di tutti i test vengono utilizzati per l'ottimizzazione delle prestazioni e la verifica del supporto per i numeri di scalabilità previsti nel modello utente.

