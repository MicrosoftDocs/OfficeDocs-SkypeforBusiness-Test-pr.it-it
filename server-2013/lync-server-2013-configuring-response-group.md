---
title: 'Lync Server 2013: Configurazione di Response Group'
TOCTitle: Configurazione di Response Group
ms:assetid: c56db929-cb21-4af0-be3f-c8f807b78a5a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205249(v=OCS.15)
ms:contentKeyID: 49301897
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-30_

Response Group è una funzionalità di VoIP aziendale che consente di instradare e accodare le chiamate in arrivo per gruppi di utenti, denominati *agenti* , ad esempio un helpdesk o un servizio clienti.

I componenti richiesti da Response Group vengono installati e abilitati automaticamente nel Front End Server o nel server Standard Edition quando si distribuisce VoIP aziendale. Affinché gli utenti possano usufruire di Response Group, è necessario configurare gruppi di agenti, quindi code e infine flussi di lavoro. Un amministratore di Response Group inoltre può delegare la configurazione di un flusso di lavoro esistente a un responsabile di Response Group, che può quindi modificare e riconfigurare il flusso di lavoro con i gruppi di agenti e le code associati.

In questa sezione viene illustrata la configurazione di Lync Server 2013Response Group. Si presuppone che siano state già lette le sezioni sulla pianificazione relative a Response Group e che sia stato distribuito un server Enterprise Edition o un server Standard Edition con VoIP aziendale.

> [!tip]  
> Per informazioni dettagliate sulla creazione di un Response Group tramite Lync Server Management Shell, incluso uno script di esempio, vedere &quot;Creazione del primo Response Group tramite Lync Server Management Shell&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=204108">http://go.microsoft.com/fwlink/p/?linkId=204108</a>.

## Argomenti della sezione

  - [Autorizzazioni e prerequisiti per la configurazione di Response Group in Lync Server 2013](lync-server-2013-response-group-configuration-permissions-and-prerequisites.md)

  - [Processo di distribuzione per Response Group in Lync Server 2013](lync-server-2013-deployment-process-for-response-group.md)

  - [Panoramica degli scenari di creazione del flusso di lavoro in Lync Server 2013](lync-server-2013-overview-of-workflow-creation-scenarios.md)

  - [Creare gruppi di agenti per Response Group in Lync Server 2013](lync-server-2013-create-response-group-agent-groups.md)

  - [Creare code di Response Group in Lync Server 2013](lync-server-2013-create-response-group-queues.md)

  - [Definire l'orario di ufficio dei Response Group (facoltativo) in Lync Server 2013](lync-server-2013-optional-define-response-group-business-hours.md)

  - [Definire gli insiemi di festività dei Response Group (facoltativo)](lync-server-2013-optional-define-response-group-holiday-sets.md)

  - [Creare flussi di lavoro per Response Group in Lync Server 2013](lync-server-2013-create-response-group-workflows.md)

  - [Verificare la distribuzione dei Response Group (facoltativo)](lync-server-2013-optional-verify-response-group-deployment.md)

## Vedere anche

#### Ulteriori risorse

[Pianificazione delle funzionalità di gestione delle chiamate in Lync Server 2013](lync-server-2013-planning-for-call-management-features.md)

