---
title: 'Lync Server 2013: Supporto per la messaggistica unificata di Exchange'
TOCTitle: Supporto per la messaggistica unificata di Exchange
ms:assetid: 0da62b8d-7416-4fb8-a405-381ca805c53a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398179(v=OCS.15)
ms:contentKeyID: 49299671
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per la messaggistica unificata di Exchange in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Lync Server 2013 supporta l'integrazione con la Messaggistica unificata di Exchange per combinare i messaggi vocali e i messaggi di posta elettronica in un'unica infrastruttura di messaggistica. In Exchange 2013 la Messaggistica unificata di Exchange è costituita dal servizio Messaggistica unificata di Exchange, che viene installato ed eseguito sul server Cassette postali, e dal router di chiamate di messaggistica unificata, che viene installato ed eseguito sul server Accesso client. Per le distribuzioni di VoIP aziendale di Lync Server 2013, la Messaggistica unificata di Exchange combina i messaggi vocali e i messaggi di posta elettronica in un unico archivio accessibile tramite telefono (ovvero Outlook Voice Access) o tramite computer. La Messaggistica unificata di Exchange e Lync Server 2013 interagiscono per garantire il risponditore automatico, Outlook Voice Access e i servizi con operatore automatico agli utenti di VoIP aziendale.

Oltre al supporto dell'integrazione con distribuzioni locali della Messaggistica unificata di Exchange, Lync Server 2013 offre il supporto per l'integrazione con la Messaggistica unificata di Exchange ospitata. Questo consente di fornire la funzionalità di messaggistica vocale agli utenti di cui viene eseguita la migrazione in parte o completamente in un provider di servizi di Exchange ospitato, ad esempio Microsoft Exchange Online.

Lync Server 2013 supporta le versioni seguenti:

  - Microsoft Exchange 2013

  - Microsoft Exchange Server 2010 (necessario) o con il Service Pack più recente (consigliato)

  - Microsoft Exchange Server 2007 con Service Pack 1 (SP1) (necessario) o con il Service Pack più recente (consigliato)

Non è possibile collocare la Messaggistica unificata di Exchange con Lync Server 2013 o un database di Lync Server 2013. È possibile installare la Messaggistica unificata di Exchange e Lync Server 2013 in foreste separate.


> [!NOTE]
> La Messaggistica unificata di Exchange potrebbe non essere necessaria per le distribuzioni di VoIP aziendale con un sistema PBX distribuito, in quanto tale sistema può continuare a fornire a tutti gli utenti il servizio di segreteria telefonica e gli altri servizi correlati. Se successivamente si disattiva il sistema PBX, ad esempio se si distribuisce il trunking SIP per la connettività PSTN (Public Switched Telephone Network), sarà necessario riconfigurare la Messaggistica unificata di Exchange per fornire il servizio di segreteria telefonica agli utenti che in precedenza avevano utilizzato il sistema di segreteria telefonica PBX.



## Argomenti della sezione

  - [Componenti e topologie per la messaggistica unificata locale in Lync Server 2013](lync-server-2013-components-and-topologies-for-on-premises-unified-messaging.md)

  - [Supporto per l'integrazione di messaggistica unificata di Exchange ospitata in Lync Server 2013](lync-server-2013-support-for-hosted-exchange-um-integration.md)

