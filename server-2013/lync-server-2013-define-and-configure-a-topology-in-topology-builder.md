---
title: 'Lync Server 2013: Definire e configurare una topologia in Generatore di topologie'
TOCTitle: Definire e configurare una topologia in Generatore di topologie
ms:assetid: 99231ff5-1c21-432b-ad65-8675fcd484f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398788(v=OCS.15)
ms:contentKeyID: 49301414
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire e configurare una topologia in Generatore di topologie per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

L'esecuzione di Generatore di topologie per definire una nuova topologia o per modificarne una esistente non richiede l'appartenenza a un gruppo di amministratori locali o di domini con privilegi. Generatore di topologie consente di eseguire le operazioni necessarie per definire la topologia per un pool Front End Enterprise Edition o un Standard Edition, a seconda dei requisiti della configurazione.

È necessario utilizzare Generatore di topologie per completare e pubblicare la topologia prima che sia possibile installare Lync Server 2013 nei server. La procedura seguente include i passaggi per definizione di una nuova topologia.

## Per definire una topologia

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  In Generatore di topologie selezionare **Nuova topologia** . Verrà richiesto di inserire un percorso e un nome file per il salvataggio della topologia. Assegnare alla topologia un nome significativo e accettare l'estensione predefinita tbxml. Fare clic su **OK** .

3.  Passare al percorso in cui si desidera salvare il file XML della nuova topologia, immettere un nome per il file e quindi fare clic su **Salva** .

4.  Nella pagina **Definire il dominio primario** immettere il nome del dominio SIP primario per l'organizzazione e quindi fare clic su **Avanti** .

5.  Nella pagina **Specificare i domini aggiuntivi supportati** immettere i nomi degli eventuali domini aggiuntivi e quindi fare clic su **Avanti** .

6.  Nella pagina **Definire il primo sito** immettere il nome e la descrizione del primo sito e quindi fare clic su **Avanti** .

7.  Nella pagina **Specificare i dettagli del sito** immettere le informazioni relative alla posizione del sito e quindi fare clic su **Avanti** .

8.  Nella pagina **Definizione della nuova topologia completata** assicurarsi che la casella di controllo **Al termine della procedura guidata, aprire la procedura guidata del nuovo Front End** sia selezionata e quindi fare clic su **Fine**.

Dopo aver definito e salvato la topologia, utilizzare la procedura guidata del nuovo Front End per definire un pool Front End o un server Standard Edition per il sito. Per informazioni dettagliate, vedere [Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md).

