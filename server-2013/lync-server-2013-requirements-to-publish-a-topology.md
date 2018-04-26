---
title: 'Lync Server 2013: Requisiti per la pubblicazione di una topologia'
TOCTitle: Requisiti per la pubblicazione di una topologia
ms:assetid: 841cdf5d-d884-414d-ab50-3bb681b622ed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg195733(v=OCS.15)
ms:contentKeyID: 49301184
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti per la pubblicazione di una topologia Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In questo argomento vengono descritti i requisiti relativi a software e infrastruttura specifici per la pubblicazione di una topologia, sia che si utilizzi Generatore di topologie o l'interfaccia della riga di comando di Lync Server 2013 Management Shell. Questi requisiti sono in aggiunta ai requisiti generali relativi a sistema operativo, software e autorizzazioni applicabili a tutti gli strumenti di amministrazione di Lync Server 2013. Prima di pubblicare una topologia, verificare che siano soddisfatti tutti i requisiti relativi agli strumenti di amministrazione.

  - È necessario eseguire Generatore di topologie in un computer che fa parte dello stesso dominio o foresta della distribuzione di Lync Server 2013 che si sta creando affinché i passaggi di preparazione di Servizi di dominio Active Directory siano già completati e sia possibile utilizzare gli strumenti di amministrazione nel computer per pubblicare correttamente la topologia.

  - I computer definiti nella topologia devono appartenere al dominio, ad eccezione dei server perimetrali, nonché essere in Servizi di dominio Active Directory. Non è tuttavia necessario che i computer siano online quando si pubblica la topologia.

  - La condivisione file per il pool deve essere creata ed essere disponibile per gli utenti remoti.

  - Per pubblicare un pool Front End Enterprise Edition, il server back-end basato su SQL Server deve appartenere al dominio in cui si distribuiscono i server, deve essere online e deve essere configurato con le regole del firewall appropriate per renderlo disponibile per gli utenti remoti. Per informazioni dettagliate sull'impostazione delle eccezioni del firewall, vedere [Informazioni sui requisiti del firewall per SQL Server con Lync Server 2013](lync-server-2013-understanding-firewall-requirements-for-sql-server.md). Per ulteriori dettagli sulla configurazione di SQL Server, vedere [Configurare SQL Server per Lync Server 2013](lync-server-2013-configure-sql-server-for-lync-server.md).
    

    > [!NOTE]
    > Il server Standard Edition dispone di un database collocato che accetta la configurazione pubblicata. È prima necessario eseguire l'attività di configurazione <STRONG>Prepara primo Server Standard</STRONG> nella Distribuzione guidata di Lync Server.



## Vedere anche

#### Attività

[Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md)  
[Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md)  

#### Concetti

[Requisiti software degli strumenti di amministrazione in Lync Server 2013](lync-server-2013-administrative-tools-software-requirements.md)  
[Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md)  

#### Ulteriori risorse

[Autorizzazioni e diritti di amministratore necessari per l'installazione e l'amministrazione di Lync Server 2013](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)

