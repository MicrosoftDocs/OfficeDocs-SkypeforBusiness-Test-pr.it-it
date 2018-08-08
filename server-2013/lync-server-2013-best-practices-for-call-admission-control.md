---
title: "Lync Server 2013: Procedure consigliate per controllo ammissione di chiamata"
TOCTitle: Procedure consigliate per il controllo di ammissione di chiamata
ms:assetid: 97173cca-8175-4ae2-a247-eb7ef809da93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398770(v=OCS.15)
ms:contentKeyID: 49301387
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Procedure consigliate per il controllo di ammissione di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-22_

Per migliorare le prestazioni e facilitare la distribuzione, applicare le procedure consigliate seguenti quando si distribuisce il servizio Controllo di ammissione di chiamata:

  - Verificare che il provisioning delle WAN sia adeguato al traffico multimediale corrente e previsto.
    

    > [!NOTE]
    > È consigliabile considerare un buffer rispetto ai limiti di larghezza di banda. Esistono scenari, ad esempio le race condition, che incidono sulla larghezza di banda totale utilizzata e possono produrre situazioni in cui i limiti di larghezza di banda vengono superati. Se ad esempio si tenta di avviare due chiamate mentre il traffico multimediale si avvicina al limite di larghezza di banda, è possibile che una delle due venga rifiutata perché l'altra è configurata per partire per prima.



  - Monitorare l'utilizzo della rete e i record dettagli chiamata, in modo da poter scegliere impostazioni ottimali per il servizio Controllo di ammissione di chiamata e aggiornarle al variare dell'utilizzo della rete.

  - Utilizzare i criteri larghezza di banda relativi al servizio Controllo di ammissione di chiamata a complemento delle impostazioni QoS.

  - Se si desidera reindirizzare le chiamate bloccate al PSTN, verificare le funzionalità e le capacità PSTN. Per ulteriori informazioni, vedere [Pianificazione del routing vocale in uscita in Lync Server 2013](lync-server-2013-planning-outbound-voice-routing.md).
    

    > [!NOTE]
    > La capacità fa riferimento al numero di porte che è necessario aprire per supportare il potenziale reindirizzamento PSTN.


