---
title: "Lync Server 2013: Crea topologia di server perimetrali e server Director"
TOCTitle: Creazione di una topologia di server perimetrali e server Director
ms:assetid: 11e5759e-d69f-4c39-8994-f467c279c558
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398202(v=OCS.15)
ms:contentKeyID: 49299727
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione di una topologia di server perimetrali e server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

La creazione della topologia prevede l'esecuzione delle attività di pianificazione e distribuzione seguenti:

  - **Pianificazione**   Definire una topologia appropriata per l'organizzazione e identificare i componenti necessari per distribuirla. Questi sono passaggi standard del processo di pianificazione. Microsoft Lync Server 2013, Strumento di pianificazione fornito con Lync Server 2013 semplifica l'avvio di tale processo, consentendo inoltre di apportare facilmente modifiche man mano che i requisiti e i piani vengono finalizzati.

  - **Distribuzione**   La topologia definita utilizzando Generatore di topologie è fondamentale per la distribuzione di qualsiasi server Lync Server 2013. Se non si completa la definizione e la pubblicazione della topologia tramite il Generatore di topologie durante le attività di pianificazione, sarà necessario completarla e pubblicare la topologia prima di distribuire i server perimetrali.

Non è possibile distribuire componenti di server perimetrali finché non è stato distribuito almeno un pool interno ed è necessario installare Generatore di topologie per distribuire tale pool. In questa sezione non viene illustrata l'installazione di Generatore di topologie perché fa parte del processo di installazione del pool interno.

Per informazioni dettagliate su questi strumenti, vedere [Elenco di controllo di distribuzione per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deployment-checklist-for-external-user-access.md).


> [!NOTE]
> Se in precedenza è stato utilizzato il Generatore di topologie per definire una topologia completa, inclusa la topologia perimetrale, è possibile ignorare le attività <A href="lync-server-2013-define-your-edge-topology.md">Definire la topologia perimetrale in Lync Server 2013</A> e <A href="lync-server-2013-publish-your-topology.md">Pubblicare la topologia in Lync Server 2013</A> di questa sezione, ma è necessario eseguire l'attività <A href="lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md">Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale</A>.



## Argomenti della sezione

  - [Definire la topologia perimetrale in Lync Server 2013](lync-server-2013-define-your-edge-topology.md)

  - [Definire topologie con server Director facoltativi nella topologia per Lync Server 2013](lync-server-2013-define-optional-director-topologies-in-your-topology.md)

  - [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-your-topology.md)

  - [Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md)

