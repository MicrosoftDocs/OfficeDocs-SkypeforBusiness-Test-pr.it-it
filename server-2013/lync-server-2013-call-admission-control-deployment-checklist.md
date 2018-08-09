---
title: "Lync Server 2013: Verifica distribuz. servizio Controllo ammissione chiamata"
TOCTitle: "Lync Server 2013: Verifica distribuz. servizio Controllo ammissione chiamata"
ms:assetid: d56a525f-3da5-4ac0-a311-0c5efd98c9df
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398928(v=OCS.15)
ms:contentKeyID: 49302089
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo per la distribuzione del servizio Controllo di ammissione di chiamata

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Utilizzare l'elenco di controllo seguente per verificare di aver completato tutta le attività di configurazione necessarie per la distribuzione del servizio Controllo di ammissione di chiamata.

  - Se vengono distribuiti uno o più server perimetrali, è necessario aggiungere l'indirizzo IP di ogni interfaccia esterna all'elenco di subnet nelle impostazioni di configurazione di rete, con una maschera di 32 bit. È inoltre necessario associare questa subnet (indirizzo IP) all'ID sito di rete relativo alla località geografica in cui è distribuito il servizio A/V Edge.
    

    > [!NOTE]
    > Per implementare la funzionalità Controllo di ammissione di chiamata, non sono necessari server perimetrali.



  - Verificare che il servizio Controllo di ammissione di chiamata sia abilitato tramite il Pannello di controllo di Lync Server oppure eseguendo il cmdlet specificato in [Abilitare il servizio Controllo di ammissione di chiamata](lync-server-2013-enable-call-admission-control.md).

  - Verificare che il servizio Controllo di ammissione di chiamata sia abilitato in tutti i siti centrali. A tale scopo, è possibile utilizzare Generatore di topologie. Se viene generato un avviso quando si esegue la pubblicazione, *non* ignorarlo.

  - Verificare che tutte le subnet gestite nella rete aziendale siano configurate nelle impostazioni di configurazione di rete. È inoltre essenziale che ogni subnet sia associata a un sito di rete, come descritto in [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md).

  - Verificare che la subnet o gli indirizzi IP di tutti i Front End Server, Survivable Branch Appliance (SBA), Audio/Video Conferencing Server (se in un pool separato) e Mediation Server siano configurati nelle impostazioni di configurazione di rete.

