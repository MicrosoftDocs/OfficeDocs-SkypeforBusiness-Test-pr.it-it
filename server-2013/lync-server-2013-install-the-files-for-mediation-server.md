---
title: 'Lync Server 2013: Installare i file per Mediation Server'
TOCTitle: Installare i file per Mediation Server
ms:assetid: f0f7dd15-58e1-40fd-aa7e-6db50ceafacd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412998(v=OCS.15)
ms:contentKeyID: 49302416
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installare i file per Mediation Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-06_

Per eseguire questa procedura, è necessario accedere al server almeno come amministratore locale e come utente di dominio appartenente almeno al gruppo RTCUniversalReadOnlyAdmin.

In questo argomento vengono descritti i passaggi della Distribuzione guidata di Lync Server 2013 da eseguire per installare i file del Mediation Server in un computer aggiunto al pool di Mediation Server utilizzando Generatore di topologie per definire e pubblicare il pool. Durante l'installazione dei file per il Mediation Server, viene anche installato e assegnato il certificato richiesto da ogni computer di un pool di Mediation Server.

Se nel sito sono già stati installati Mediation Server collocati nei pool Front End o nei server Standard Edition, è possibile saltare questo argomento e passare a [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md).


> [!NOTE]
> In questo argomento si presuppone che sia già stato definito e pubblicato un pool di Mediation Server come descritto in <A href="lync-server-2013-define-a-mediation-server-in-topology-builder.md">Definire un Mediation Server in Generatore di topologie in Lync Server 2013</A> e in <A href="lync-server-2013-publish-the-topology.md">Pubblicare la topologia in Lync Server 2013</A> nella documentazione relativa alla distribuzione e che sia stato verificato che i computer del pool di Mediation Server soddisfino i prerequisiti descritti in <A href="lync-server-2013-software-prerequisites-for-enterprise-voice.md">Prerequisiti software per VoIP aziendale in Lync Server 2013</A> e in <A href="lync-server-2013-security-and-configuration-prerequisites-for-enterprise-voice.md">Prerequisiti di configurazione e sicurezza per VoIP aziendale in Lync Server 2013</A>.



## Per installare i file per un pool Mediation Server autonomo

1.  Dal supporto di installazione fare clic con il pulsante destro del mouse su *\<supporto installazione\>* **\\Setup\\amd64\\Setup.exe** e quindi scegliere **Esegui come amministratore** .

2.  Nella pagina **Percorso di installazione**, fare clic su **OK**.

3.  Nella pagina **Contratto di licenza con l'utente finale** fare clic su **Accetto** e quindi su **OK** . Questa operazione è obbligatoria per proseguire.

4.  Nella pagina **Distribuzione guidata di Lync Server 2010** fare clic su **Installa o aggiorna il sistema Lync Server** .

5.  Accanto a **Passaggio 1: Installazione dell'archivio di configurazione locale** fare clic su **Esegui** e quindi seguire le istruzioni visualizzate sullo schermo.

6.  Nella pagina **Configura la replica locale dell'archivio di gestione centrale** accettare l'impostazione predefinita **Recupera direttamente dall'archivio di gestione centrale** e quindi fare clic su **Avanti** .

7.  Nella pagina **Esecuzione comandi in corso** , quando lo stato dell'attività risulta completato, fare clic su **Fine** .

8.  Accanto a **Passaggio 2: Installazione o rimozione componenti di Lync Server** fare clic su **Esegui** e quindi su **Avanti** .

9.  Nella pagina **Esecuzione comandi in corso** , quando lo stato dell'attività risulta completato, fare clic su **Fine** .

10. Accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** fare clic su **Esegui** . Seguire le istruzioni visualizzate sullo schermo, accettando le impostazioni predefinite. Il Mediation Server richiede un certificato, quindi il **Passaggio 3** verrà eseguito due volte, una per emettere il certificato necessario e l'altra per assegnarlo.

11. Dopo che il certificato è stato emesso e assegnato correttamente, accanto **Passaggio 4: Avvia servizi** fare clic su **Esegui** e quindi seguire le istruzioni visualizzate sullo schermo.

12. Al termine del **Passaggio 4** , riavviare il server e accedere come membro del gruppo DomainAdmins.

13. Nel computer che esegue Pannello di controllo di Lync Server verificare nella pagina **Topologia** di Pannello di controllo di Lync Server che lo stato del Mediation Server sia indicato con un segno di spunta verde. Se invece appare una X rossa, selezionare il Mediation Server. Scegliere **Avvia tutti i servizi** dal menu **Azione** .

Se sono stati aggiunti più computer al pool Mediation Server, eseguire i passaggi di questa procedura in tutti gli altri computer del pool di Mediation Server. Se non è necessario installare file per Mediation Server per altri computer, eseguire le procedure descritte in [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md) per configurare le impostazioni per la connessione di trunk tra questo pool di Mediation Server (o tutti i Mediation Server di un sito) e il relativo peer.

## Vedere anche

#### Concetti

[Requisiti dei certificati per i server interni in Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md)

