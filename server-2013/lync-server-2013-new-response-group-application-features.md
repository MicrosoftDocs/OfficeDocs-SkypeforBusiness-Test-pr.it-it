---
title: "Lync Server 2013: Nuove funzionalità dell'applicazione Response Group"
TOCTitle: Nuove funzionalità dell'applicazione Response Group
ms:assetid: 569544b4-fa97-429b-97e6-568afab6c19b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398373(v=OCS.15)
ms:contentKeyID: 49300620
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Nuove funzionalità dell'applicazione Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

Con l'applicazione Response Group, è possibile instradare e accodare le chiamate in arrivo per persone designate a svolgere compiti particolari come il servizio clienti, l'helpdesk interno o il supporto telefonico generico per un reparto.

Le funzionalità seguenti dell'applicazione Response Group sono una novità di Lync Server 2013:

  - **Ruolo Responsabile**
    
    Lync Server 2013 introduce il nuovo ruolo Responsabile Response Group. Ora per i Response Group esistono due ruoli di gestione: Responsabile Response Group e Amministratore Response Group. Mentre un Amministratore Response Group può ancora configurare qualsiasi elemento di qualsiasi Response Group, un Responsabile può configurare solo elementi specifici e solo per i Response Group di cui è proprietario.
    
    Questo miglioramento del modello di amministrazione va a vantaggio della scalabilità dei Response Group, soprattutto negli scenari di distribuzioni di grandi dimensioni.

  - **Disponibilità elevata**
    
    Il supporto della disponibilità elevata per l' applicazione Response Group, sotto forma di mirroring SQL Server, è abilitato all'interno della configurazione generale e della distribuzione della disponibilità elevata per Lync Server 2013. Se la configurazione prevede la disponibilità elevata e si perde la connettività al server back-end primario, il funzionamento di Response Group non ne risente, grazie all'intervento del server back-end mirror.
    
    Non è possibile abilitare o configurare singolarmente il supporto del mirroring SQL Server per l' applicazione Response Group al di fuori della configurazione generale della disponibilità elevata di Lync Server 2013.

  - **Ripristino di emergenza**
    
    Il supporto del ripristino di emergenza per l' applicazione Response Group viene abilitato all'interno della configurazione e della distribuzione dei pool Front End abbinati, che fanno parte della configurazione del ripristino di emergenza Lync Server 2013 complessivo. Inoltre, i cmdlet di importazione ed esportazione di Response Group supportano il processo di failover al pool di backup e il processo di failback al pool primario o a un nuovo pool. Se si verifica un'interruzione del pool primario, per i Response Group è possibile eseguire il failover al pool di backup e quindi, al termine dell'interruzione, il failback al pool primario o a un nuovo pool.

## Vedere anche

#### Ulteriori risorse

[Pianificazione dei Response Group in Lync Server 2013](lync-server-2013-planning-for-response-groups.md)

