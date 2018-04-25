---
title: Installazione dei Management Pack di Lync Server 2013
TOCTitle: Installazione dei Management Pack di Lync Server 2013
ms:assetid: b800d4ab-fdc8-4c72-a76a-b78932779fe3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205202(v=OCS.15)
ms:contentKeyID: 49301758
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione dei Management Pack di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-22_

System Center Operations Manager da solo è in grado di effettuare il monitoraggio solo di una piccola parte del sistema operativo Windows. È tuttavia possibile estendere le funzionalità di System Center Operations Manager installando i Management Pack, componenti software che determinano quali elementi possono essere monitorati da System Center Operations Manager, incluse le modalità di monitoraggio di tali elementi e di attivazione e segnalazione degli avvisi. In Microsoft Lync Server 2013 sono inclusi due Management Pack di System Center Operations Manager che offrono le funzionalità seguenti:

  - Il Management Pack per componenti e utenti (Microsoft.LS.2013.Monitoring.ComponentAndUser.mp) tiene traccia dei problemi di Lync Server registrati nei log eventi, registrati dai contatori delle prestazioni oppure registrati nelle registrazioni dettagli chiamata (CDR) o nei database QoE. Per problemi critici, System Center Operations Manager può essere configurato in modo da avvisare immediatamente gli amministratori tramite posta elettronica, messaggi istantanei o messaggi SMS. La tecnologia SMS viene utilizzata per inviare messaggi di testo da un dispositivo mobile a un altro.
    

    > [!NOTE]
    > Per ulteriori informazioni sulla configurazione della notifica di Operations Manager, vedere Configurazione delle notifiche nella Libreria TechNet all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268785%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=268785&amp;clcid=0x410</A>.



  - Il Management Pack per il monitoraggio attivo (Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp) testa attivamente i principali componenti di Lync Server, ad esempio l'accesso al sistema, lo scambio di messaggi istantanei o l'esecuzione di chiamate a un telefono sulla rete PSTN (Public Switched Telephone Network). Questi test vengono eseguiti utilizzando i cmdlet delle transazioni sintetiche di Lync Server. Il cmdlet **Test-CsIM** ad esempio viene utilizzato per simulare una conversazione istantanea tra due utenti di test. Se questa conversazione simulata ha esito negativo, verrà generato un avviso.

I due Management Pack inclusi in Lync Server 2013 presentano numerosi miglioramenti rispetto ai Management Pack utilizzati con Microsoft Lync Server 2010. Ad esempio, il Management Pack per componenti di Lync Server 2013 non si limita a monitorare Lync Server. Oltre a monitorare i log eventi e i contatori delle prestazioni per Lync Server, tale Management Pack può tenere traccia delle prestazioni e generare avvisi per fattori critici come i seguenti:

  - **Internet Information Services (IIS)**   Vengono generati avvisi se Internet Information Services è offline. Questo è importante perché i servizi Web di Lync Server si basano su IIS.

  - **Utilizzo del processore**   Vengono generati avvisi se le risorse di sistema, ad esempio la memoria disponibile, iniziano a essere insufficienti. Tali avvisi verranno generati anche se Lync Server non è responsabile dell'utilizzo eccessivo del sistema.

  - **Eventi problematici del computer**   Vengono generati avvisi in caso di problemi hardware o software che mettono a rischio il funzionamento di un server. Gli amministratori di Lync Server ad esempio riceveranno una notifica se su un server sta per verificarsi un problema del disco rigido.

I nuovi Management Pack inoltre offrono funzionalità di segnalazione avanzate. I nuovi rapporti per Lync Server 2013 sono:

  - **End to End Scenario Availability Report**   In questo rapporto sono riportati i dettagli relativi alla disponibilità e al tempo di attività per i servizi principali di Lync Server, ad esempio registrazione o presenza.

  - **Capacity Report**   Utilizzando le informazioni dei contatori delle prestazioni, questo rapporto illustra le tendenze per i componenti di sistema, ad esempio la disponibilità della memoria e l'utilizzo del processore.

  - **Component Report**   In questo rapporto sono elencati i principali generatori di avvisi, raggruppati in base al componente di Lync Server.

Oltre a questi rapporti predefiniti, i Management Pack per Lync Server 2013 generano automaticamente avvisi per l'affidabilità delle chiamate (metrica misurata dalla registrazione dettagli chiamata) e per gli stati QoE (metrica misurata dalla qualità percepita dagli utenti). Se è stata abilitata la registrazione dettagli chiamata, è possibile visualizzare gli avvisi di affidabilità delle chiamate eseguendo la procedura seguente dalla console di System Center Operations Manager:

  - Espandere **Monitoring**, **Microsoft Lync Server 2013 Health** e **Call Reliability and Media Quality** e quindi fare clic su **Call Reliability**.

Per visualizzare gli avvisi QoE, eseguire questa procedura dalla console di System Center Operations Manager:

  - Espandere **Monitoring**, **Microsoft Lync Server 2013 Health**, **Call Reliability and Media Quality** e quindi **Media Quality**.

I Management Pack per Lync Server 2013 ora utilizzano l'individuazione a livello di computer invece del meccanismo di individuazione centrale utilizzato in Microsoft Lync Server 2010. Questo significa che ogni agente di System Center fondamentalmente individua se stesso e segnala la propria esistenza al server di gestione centrale. L'utilizzo dell'individuazione a livello di computer semplifica l'amministrazione dell'infrastruttura di System Center e consente la coesistenza di diverse versioni di Management Pack di Lync Server, ad esempio Management Pack per Lync Server 2010 e Management Pack per Lync Server 2013.

