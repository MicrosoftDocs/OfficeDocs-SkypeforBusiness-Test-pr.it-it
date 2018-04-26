---
title: 'Lync Server 2013: Distribuzione di Lync Server 2013 Standard Edition in un server Lync Server 2013 Enterprise esistente'
TOCTitle: Distribuzione di Lync Server 2013 Standard Edition in un server Lync Server 2013 Enterprise esistente
ms:assetid: 05ea128d-6c94-49b3-b28b-477367196425
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398112(v=OCS.15)
ms:contentKeyID: 49299557
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di Lync Server 2013 Standard Edition in un server Lync Server 2013 Enterprise esistente

 

_**Ultima modifica dell'argomento:** 2012-10-01_

La distribuzione di un server Standard Edition in una distribuzione Enterprise Edition esistente è analoga alla distribuzione di ulteriori ruoli del server. Un server Standard Edition può essere distribuito in un altro sito, consentendo agli utenti di quel sito di essere situati nel server Standard Edition anziché nel pool Front End su una rete WAN (Wide Area Network). Le procedure per installare il nuovo sito e i nuovi server in tale sito sono già state descritte in altre sezioni della documentazione relativa alla [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md).

**Per definire un nuovo sito**

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console fare clic con il pulsante destro del mouse su **Lync Server 2013** e quindi scegliere **Nuovo sito centrale** .

3.  Nella pagina **Identificare il sito** assegnare un nome al sito e facoltativamente immettere una descrizione.

4.  Eseguire le procedure per definire il resto della topologia del sito. Per informazioni dettagliate, vedere [Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md).

5.  Pubblicare la topologia aggiornata. Per informazioni dettagliate, vedere [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md).

6.  Impostare e installare un server Standard Edition.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ205186.Caution(OCS.15).gif" title="Caution" alt="Caution" />Attenzione:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se è stato distribuito un ambiente solo con un server Standard Edition, è possibile avviare il processo di configurazione dalla Distribuzione guidata di Lync Server utilizzando il collegamento <strong>Prepara primo Server Standard</strong> per installare i file di database iniziali nel nuovo server Standard Edition. <strong>Non</strong> seguire tale processo per installare un server Standard Edition in una distribuzione di Lync Server 2013 già esistente.</td>
    </tr>
    </tbody>
    </table>

