---
title: 'Lync Server 2013: Pubblicare la topologia'
TOCTitle: Pubblicare la topologia
ms:assetid: bfed3829-7a54-4b5c-a7cb-28871acd35e7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412935(v=OCS.15)
ms:contentKeyID: 49301843
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pubblicare la topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Ogni volta che si utilizza Generatore di topologie per generare la topologia, è necessario pubblicare la topologia in un database nell' archivio di gestione centrale in modo che i dati possano essere utilizzati per la distribuzione di Lync Server 2013. Eseguire la procedura seguente per pubblicare la topologia.

## Per pubblicare la topologia

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console di Generatore di topologie fare clic con il pulsante destro del mouse su **Lync 2013** e quindi scegliere **Pubblica topologia** .

3.  Nella pagina iniziale della procedura guidata fare clic su **Avanti** .

4.  Nella pagina **Archivio di gestione centrale rilevato da Generatore di topologie** fare clic su **Avanti** .

5.  Nella pagina **Crea database** fare clic su **Avanti** .

6.  Quando lo stato indica che la creazione del database è stata completata, eseguire le operazioni seguenti:
    
      - Per visualizzare il log, fare clic su **Visualizza log** .
    
      - Per chiudere la procedura guidata, fare clic su **Fine** .
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Se si tratta di una nuova installazione di un server perimetrale o di un pool di server perimetrali, sarà necessario esportare la configurazione del server perimetrale da un Front End Server, un pool Front End o un server Standard Edition esistente. Per esportare la configurazione, vedere <a href="lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md">Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale</a>. Il file di configurazione verrà importato dalla condivisione di rete o dal supporto esterno durante la fase di installazione e distribuzione dei server perimetrali mediante la Distribuzione guidata di Lync Server.<br />
        Dopo che i server perimetrali sono operativi e che il database dell'archivio di gestione della configurazione locale viene replicato con la distribuzione interna, i successivi aggiornamenti apportati alla configurazione di Lync Server 2013 verranno pubblicati e replicati nei server perimetrali.</td>
        </tr>
        </tbody>
        </table>

