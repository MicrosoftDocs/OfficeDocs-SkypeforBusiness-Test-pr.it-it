---
title: Autorizzare la connessione al server perimetrale di Office Communications Server 2007 R2
TOCTitle: Autorizzare la connessione al server perimetrale di Office Communications Server 2007 R2
ms:assetid: 14f6798a-28d6-4b3d-8734-942192e1bbf5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204702(v=OCS.15)
ms:contentKeyID: 49299775
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Autorizzare la connessione al server perimetrale di Office Communications Server 2007 R2

 

_**Ultima modifica dell'argomento:** 2012-09-28_

Per ogni Front End Server o server Standard Edition di Lync Server 2013 presente nel pool pilota, è necessario aggiornare l'elenco dei server interni autorizzati per la connessione al server Office Communications Server 2007 R2 Edge. In caso contrario, la conferenza audio/visiva (A/V) con accesso esterno per utenti che partecipano utilizzando il server perimetrale legacy non funzionerà.

## Per autorizzare la connessione al server Office Communications Server 2007 R2 Edge

1.  Nel gruppo **Strumenti di amministrazione** del server Office Communications Server 2007 R2 Edge aprire lo snap-in **Gestione computer** .

2.  Nell'albero della console espandere **Servizi e applicazioni** .

3.  Fare clic con il pulsante destro del mouse su **Office Communications Server 2007 R2**, quindi fare clic su **Proprietà** .

4.  Fare clic sulla scheda **Interno** .

5.  In **Aggiungi server** fare clic su **Aggiungi** .

6.  Nella finestra di dialogo **Aggiungi Office Communications Server** inserire le informazioni pertinenti:
    
      - Specificare il nome di dominio completo (FQDN) di ogni Front End Server o server Standard Edition di Lync Server 2013 e del pool di Lync Server 2013.
    
      - Specificare l'FQDN del Director di Lync Server 2013 se si è configurata una route statica nel pool che specifica il computer dell'hop successivo in base all'FQDN.

7.  Dopo aver aggiunto una voce per ogni Front End Server, server Standard Edition, pool e Director di Lync Server 2013, fare clic su **Applica**, quindi scegliere **OK** per chiudere la pagina delle proprietà.

