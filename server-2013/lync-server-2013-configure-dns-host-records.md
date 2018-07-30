---
title: 'Lync Server 2013: Configurare i record host DNS'
TOCTitle: Configurare i record host DNS
ms:assetid: 78a1afcf-41c8-4da5-8740-c6570c19078c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398593(v=OCS.15)
ms:contentKeyID: 49301046
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i record host DNS per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Per eseguire correttamente questa procedura, è necessario connettersi al server o al dominio almeno come membro del gruppo Domain Admins o DnsAdmins.

## Per configurare i record A dell'host DNS

1.  Nel server DNS (Domain Name System) fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **DNS** .

2.  Nell'albero della console per il dominio espandere **Zone di ricerca diretta** e quindi fare clic con il pulsante destro del mouse sul dominio in cui verrà installato Lync Server 2013.

3.  Scegliere **Nuovo host (A o AAAA)** .

4.  Fare clic su **Nome** e digitare il nome host per il pool. Il nome di dominio viene presupposto dalla zona in cui è definito il record e non deve essere immesso come parte del record A.

5.  Fare clic su **Indirizzo IP** e digitare l'IP virtuale (VIP) del servizio di bilanciamento del carico per il pool Front End.
    
    > [!IMPORTANT]  
    > Nelle distribuzioni in cui viene utilizzato un pool di server Director, i record host (A) per gli URL semplici devono puntare al VIP del servizio di bilanciamento del carico dei server Director.    

    > [!NOTE]
    > Se si distribuisce solo un Server Enterprise o un server Director connesso alla topologia senza un servizio di bilanciamento del carico o si distribuisce un server Standard Edition, digitare l'indirizzo IP del Server Enterprise, del server Standard Edition o del server Director. Un servizio di bilanciamento del carico è necessario se si distribuiscono più Server Enterprise o server Director in un pool. I servizi di bilanciamento del carico non vengono utilizzati con server Standard Edition.



6.  Fare clic su **Aggiungi host** e quindi su **OK** .

7.  Per creare un record A aggiuntivo, ripetere i passaggi 4 e 5.

8.  Al termine della creazione di tutti i record A necessari, fare clic su **Fine** .

