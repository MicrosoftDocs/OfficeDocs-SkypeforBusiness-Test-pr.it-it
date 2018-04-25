---
title: 'Lync Server 2013: Installare il database del server Standard Edition'
TOCTitle: Installare il database del server Standard Edition
ms:assetid: 0bd3a804-aad6-48cb-981b-54725af032db
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398167(v=OCS.15)
ms:contentKeyID: 49299663
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installare il database del server Standard Edition per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

L'impostazione di un server Standard Edition come l'unico server dell'infrastruttura che ospiti gli utenti si differenzia dalle altre installazioni di server perché nella **Distribuzione guidata** è presente un'opzione specifica per installare il server iniziale.

## Per installare un server Standard Edition

1.  Eseguire l'accesso al server in cui si intende installare il server Standard Edition come amministratori locali o con un ruolo equivalente a livello di dominio.

2.  Se non si è provveduto a preparare Servizi di dominio Active Directory, eseguire prima tali procedure. Per informazioni dettagliate, vedere [Preparazione di Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-preparing-active-directory-domain-services.md).

3.  Nella Distribuzione guidata di Lync Server fare clic su **Prepara primo server Standard Edition** .

4.  Nella pagina **Prepara singolo Server Standard** fare clic su **Avanti** .

5.  Nella pagina **Esecuzione comandi in corso** SQL Server 2012 Express viene installato come archivio di gestione centrale. Vengono create le regole firewall necessarie. Al termine dell'installazione del database e dei prerequisiti software, fare clic su **Fine** .
    

    > [!NOTE]
    > L'installazione iniziale può richiedere tempo senza che vengano visualizzati aggiornamenti visibili nella schermata riepilogativa di output dei comandi. Questo è dovuto all'installazione di SQL Server Express. Se si desidera monitorare l'installazione del database, usare Gestione attività.



6.  Nella pagina Distribuzione guidata di Lync Server fare clic su **Installa Generatore di topologie** se gli strumenti di amministrazione non sono stati installati in precedenza. Per informazioni dettagliate, vedere [Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md).

7.  Verificare che accanto a "Prepara Active Directory", "Prepara primo Server Standard" e "Installa Generatore di topologie" siano visualizzati segni di spunta di colore verde.

