---
title: 'Lync Server 2013: Componenti utilizzati da Response Group'
TOCTitle: Componenti utilizzati da Response Group
ms:assetid: 2b058785-47ca-43b7-b3de-6928a60dc685
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425768(v=OCS.15)
ms:contentKeyID: 49300018
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti utilizzati da Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-11_

L' applicazione Response Group viene abilitata automaticamente quando si distribuisce VoIP aziendale. In questa sezione vengono descritti i componenti che supportano l' applicazione Response Group.

## Componenti di Response Group

I componenti di Microsoft Lync Server 2013 seguenti supportano l' applicazione Response Group:

  - **Servizio applicazione**   Il Servizio applicazione offre una piattaforma per la distribuzione, l'hosting e la gestione delle applicazioni di comunicazione unificate, come Response Group. Il Servizio applicazione viene installato automaticamente in ogni Front End Server di un pool Front End e in ogni server Standard Edition.

  - **applicazione Response Group**   L' applicazione Response Group è una delle applicazioni per comunicazioni unificate ospitate dal Servizio applicazione. Viene inclusa automaticamente quando si distribuisce Response Group. L' applicazione Response Group instrada e accoda le chiamate in arrivo per i gruppi di agenti.

  - **Language Pack**   È necessario un Language Pack per il supporto delle funzionalità di sintesi vocale e riconoscimento vocale. Queste tecnologie vocali vengono usate quando si configurano messaggi, ad esempio messaggi di benvenuto o di altro tipo, nonché domande e risposte IVR (Interactive Voice Response). Per impostazione predefinita, quando si distribuisce Lync Server 2013 vengono installati i 26 Language Pack predefiniti.

  - **File audio**   I file audio vengono utilizzati per i messaggi e la musica di attesa.

  - **Archivio file**   In Response Group viene utilizzato l'archivio file per archiviare i file audio. Più pool di Response Group possono utilizzare la stessa istanza di archivio file.

  - **Strumento di configurazione di Response Group**   Lo Strumento di configurazione di Response Group è uno strumento basato sul Web utilizzato per creare e configurare Response Group. Lo Strumento di configurazione di Response Group viene incluso quando si installano i servizi Web.

  - **Pannello di controllo di Microsoft Lync Server 2013**   È possibile usare Pannello di controllo di Lync Server per installare e configurare gruppi di agenti e code per i Response Group.

  - **Lync Server Management Shell**   Tutte le impostazioni di Response Group possono essere configurate utilizzando i cmdlet di Lync Server Management Shell.

  - **Microsoft Lync 2013**   Gli agenti formali, ovvero agenti che devono eseguire l'accesso al gruppo per poter accettare le chiamate per il gruppo, usano Lync 2013 per l'accesso e la disconnessione dal gruppo. Se un gruppo di agenti è configurato per gli agenti formali, gli agenti scelgono una voce di menu in Lync 2013 per aprire Internet Explorer e visualizzare una console su pagina Web per l'accesso e la disconnessione del gruppo.

  - **Servizi Web**   I servizi Web sono necessari per lo Strumento di configurazione di Response Group, la console di accesso e di disconnessione degli agenti, il Pannello di controllo di Lync Server e il servizio Web client Response Group.

  - **Servizio Web client Response Group**   L' applicazione Response Group offre un servizio Web client che può essere usato da applicazioni di terze parti per recuperare informazioni sugli agenti, sull'appartenenza a gruppi di agenti, sullo stato dell'accesso degli agenti, sullo stato delle chiamate per i gruppi e sui gruppi che supportano le chiamate anonime. In Lync 2013 e Lync 2010 Attendant viene usato il servizio Web client Response Group per recuperare l'elenco dei Response Group che possono essere usati dagli agenti per eseguire chiamate anonime. Il servizio Web client viene incluso quando si installano i servizi Web.

