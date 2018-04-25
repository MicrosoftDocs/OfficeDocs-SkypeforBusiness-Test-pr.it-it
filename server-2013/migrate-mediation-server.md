---
title: Eseguire la migrazione di Mediation Server
TOCTitle: Eseguire la migrazione di Mediation Server
ms:assetid: b0b77121-2c8f-413e-b276-dbf1038361d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205173(v=OCS.15)
ms:contentKeyID: 49301687
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione di Mediation Server

 

_**Ultima modifica dell'argomento:** 2012-09-28_

Il Mediation Server viene unito alla topologia pilota di Lync Server 2013 durante l'esecuzione della procedura di unione guidata. È tuttavia possibile configurare il Mediation Server di Lync Server 2013 dopo che è stata eseguita la migrazione di tutti gli utenti, in quanto un pool di Office Communications Server 2007 R2 non può comunicare con un Mediation Server di Lync Server 2013. Durante la migrazione side-by-side, il pool di Lync Server 2013 comunica con il Mediation Server di Office Communications Server 2007 R2.

Quando si configura il Mediation Server di Lync Server 2013, è inoltre necessario aggiornare o sostituire i gateway di Office Communications Server 2007 R2. I gateway di Office Communications Server 2007 R2 non supportano il Mediation Server di Lync Server 2013. È necessario distribuire i gateway certificati per Lync Server 2013 e associarli al Mediation Server di Lync Server 2013. È necessario eseguire questo passaggio prima di poter rimuovere completamente le autorizzazioni per la distribuzione di Office Communications Server 2007 R2.

Negli argomenti di questa sezione vengono descritte le attività di configurazione che è necessario eseguire dopo avere completato la migrazione del Mediation Server di Lync Server 2013. L'esecuzione della transizione dal Mediation Server collocato a un Mediation Server autonomo è un'attività facoltativa.

  - [Configurare il Mediation Server](configure-mediation-server.md)

  - [Modificare le route vocali per l'utilizzo del nuovo Lync Server 2013 Mediation Server](change-voice-routes-to-use-the-new-lync-server-2013-mediation-server.md)

  - [Effettuare la transizione di un server Mediation Server collocato in un server Mediation Server autonomo (facoltativo)](transition-a-collocated-mediation-server-to-a-stand-alone-mediation-server-optional.md)

