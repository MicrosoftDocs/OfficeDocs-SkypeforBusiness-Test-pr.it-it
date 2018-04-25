---
title: 'Lync Server 2013: Pubblicare la topologia aggiornata'
TOCTitle: Pubblicare la topologia aggiornata
ms:assetid: 59455dd1-6a9e-433f-a714-d3636c068100
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204910(v=OCS.15)
ms:contentKeyID: 49300665
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pubblicare la topologia aggiornata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

Dopo aver aggiornato la topologia in Generatore di topologie, è necessario pubblicarla nell' archivio di gestione centrale prima di configurare e usare server Chat persistente. In tutti i server della topologia vengono replicate copie di sola lettura dei dati in modo che tutti i server siano sincronizzati con la topologia e altre modifiche della configurazione.

## Per pubblicare una topologia aggiornata

Prima di pubblicare la topologia, installare i database per server Chat persistente. Usare il Generatore di topologie per installare i database selezionando **Azione** e **Installa database** .

1.  In un computer che esegue Lync Server 2013 o in cui sono installati gli strumenti di amministrazione di Lync Server, eseguire l'accesso con un account membro sia del gruppo **Domain Admins** che del gruppo **RTCUniversalServerAdmins** e con autorizzazioni di controllo completo (ovvero, lettura, scrittura e modifica) per l'archivio file da usare per server Chat persistente, in modo che il Generatore di topologie possa configurare i DACL (Discretionary Access Control List) richiesti o un account con diritti utente equivalenti.

2.  Avviare il Generatore di topologie. Selezionare **Scarica topologia dalla distribuzione esistente** o **Apri topologia da un file locale** , se la topologia è stata salvata in locale.

3.  Nell'albero della console fare clic con il pulsante destro del mouse su **Lync Server 2013** e quindi scegliere **Pubblica topologia** .

4.  Nella pagina **Pubblicare la topologia** fare clic su **Avanti** .

5.  Nella pagina **Pubblicazione guidata completata** verificare che la topologia sia stata pubblicata correttamente e quindi fare clic su **Fine** .
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Dopo aver pubblicato la topologia, prima che sia possibile archiviare contenuto di qualsiasi tipo è necessario configurare il supporto per server Chat persistente.</td>
    </tr>
    </tbody>
    </table>

