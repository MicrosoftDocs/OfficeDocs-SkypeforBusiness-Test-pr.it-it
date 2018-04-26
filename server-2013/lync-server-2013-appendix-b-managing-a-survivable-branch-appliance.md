---
title: 'Lync Server 2013: Appendice B: gestione di un Survivable Branch Appliance'
TOCTitle: 'Appendice B: gestione di un Survivable Branch Appliance'
ms:assetid: 2ec9d505-6d39-491c-9524-8cf36866b855
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425797(v=OCS.15)
ms:contentKeyID: 49300065
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Appendice B: gestione di un Survivable Branch Appliance in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-18_

In questo argomento sono descritte le procedure per la gestione di un Survivable Branch Appliance. In particolare viene descritto come sostituire e rinominare un Survivable Branch Appliance e come modificare il pool Front End di Lync Server 2013 al quale è associato il Survivable Branch Appliance.

## Per sostituire un Survivable Branch Appliance

1.  Arrestare tutti i servizi di Lync Server 2013 nel Survivable Branch Appliance. A tale scopo, vedere la documentazione del fornitore del Survivable Branch Appliance.

2.  (Consigliato) Rimuovere il Survivable Branch Appliance dal dominio.

3.  Eliminare l'oggetto computer Survivable Branch Appliance in Servizi di dominio Active Directory eseguendo la procedura seguente:
    
      - Eseguire l'accesso a un server membro come membro del gruppo Enterprise Admins.
    
      - Fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **Utenti e computer di Active Directory** .
    
      - Fare clic con il pulsante destro del mouse sull'oggetto Survivable Branch Appliance e scegliere **Elimina** .

4.  Aggiungere di nuovo l'oggetto computer Survivable Branch Appliance. A tale scopo, vedere [Aggiungere un Survivable Branch Appliance ad Active Directory in Lync Server 2013](lync-server-2013-add-a-survivable-branch-appliance-to-active-directory.md).

5.  Attendere che venga eseguita la replica di Active Directory.

6.  Aprire Lync Server Management Shell e digitare **Enable-CSTopology** .

7.  Connettere il nuovo Survivable Branch Appliance alla rete ed eseguire le operazioni descritte in [Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013 - Attività presso il sito centrale](lync-server-2013-deploying-a-survivable-branch-appliance-or-server-central-site-tasks.md) e [Distribuire un Survivable Branch Appliance o un Survivable Branch Server con Lync Server 2013 - Attività presso il sito di succursale](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md).

## Per rinominare un Survivable Branch Appliance

1.  Spostare gli utenti nel sito centrale. Per informazioni dettagliate, vedere [Spostare gli utenti in un altro pool in Lync Server 2013](lync-server-2013-move-users-to-another-pool.md).

2.  Arrestare tutti i servizi di Lync Server 2013 nel Survivable Branch Appliance. A tale scopo, vedere la documentazione del fornitore del Survivable Branch Appliance.

3.  Rimuovere il Survivable Branch Appliance dalla topologia eseguendo la procedura seguente:
    
      - Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server** e quindi **Generatore di topologie di Lync Server** .
    
      - Nell'albero della console espandere **Siti di succursale** , fare clic sul Survivable Branch Appliance e quindi nel riquadro Azioni fare clic su **Elimina** .

4.  Rimuovere il Survivable Branch Appliance dal dominio.

5.  Eliminare l'oggetto computer Survivable Branch Appliance in Active Directory eseguendo la procedura seguente:
    
      - Accedere a un controller di dominio come membro del gruppo Enterprise Admins.
    
      - Fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **Utenti e computer di Active Directory** .
    
      - Fare clic con il pulsante destro del mouse sull'oggetto Survivable Branch Appliance e scegliere **Elimina** .

6.  Ripristinare le impostazioni predefinite del Survivable Branch Appliance. A tale scopo, vedere la documentazione del fornitore del Survivable Branch Appliance.

7.  Seguire le operazioni descritte in [Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013 - Attività presso il sito centrale](lync-server-2013-deploying-a-survivable-branch-appliance-or-server-central-site-tasks.md) e [Distribuire un Survivable Branch Appliance o un Survivable Branch Server con Lync Server 2013 - Attività presso il sito di succursale](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md).

8.  Spostare gli utenti nel Survivable Branch Appliance ridenominato. Per informazioni dettagliate, vedere [Spostare gli utenti in un altro pool in Lync Server 2013](lync-server-2013-move-users-to-another-pool.md).

## Per cambiare il pool Front End di Lync Server a cui è associato il Survivable Branch Appliance

1.  Spostare gli utenti dal Survivable Branch Appliance al pool Front End di Lync Server nel sito centrale. Per informazioni dettagliate, vedere [Spostare gli utenti in un altro pool in Lync Server 2013](lync-server-2013-move-users-to-another-pool.md).

2.  Arrestare tutti i servizi di Lync Server nel Survivable Branch Appliance. A tale scopo, vedere la documentazione del fornitore del Survivable Branch Appliance.

3.  Aggiornare il pool Front End di Lync Server al quale è associato il Survivable Branch Appliance eseguendo la procedura seguente:
    
      - Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server** e quindi **Generatore di topologie di Lync Server** .
    
      - Espandere **Siti di succursale** .
    
      - Fare clic con il pulsante destro del mouse sull'oggetto Survivable Branch Appliance da modificare e scegliere **Modifica proprietà** .
    
      - In Resilienza selezionare il nuovo pool Front End al quale deve essere associato il Survivable Branch Appliance e fare clic su **Avanti** .
    
      - Nell'albero della console fare clic con il pulsante destro del mouse sul nuovo Survivable Branch Appliance, scegliere **Topologia** e quindi fare clic su **Pubblica** .

4.  Riavviare tutti i servizi di Lync Server nel Survivable Branch Appliance.

5.  Testare il Survivable Branch Appliance. Per informazioni dettagliate, vedere [Ospitare utenti in Survivable Branch Appliance o Survivable Branch Server in Lync Server 2013](lync-server-2013-home-users-on-a-survivable-branch-appliance-or-server.md).

6.  Spostare gli utenti dal pool Front End di Lync Server nel sito centrale al Survivable Branch Appliance.

