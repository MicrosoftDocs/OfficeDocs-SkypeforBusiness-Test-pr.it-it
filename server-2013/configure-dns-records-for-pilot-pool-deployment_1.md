---
title: Configurare i record DNS per la distribuzione del pool pilota
TOCTitle: Configurare i record DNS per la distribuzione del pool pilota
ms:assetid: 5c7a6e10-e1e9-4479-9bf9-d4a3e2e09ff0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688072(v=OCS.15)
ms:contentKeyID: 49887580
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i record DNS per la distribuzione del pool pilota

 

_**Ultima modifica dell'argomento:** 2012-09-24_

Prima di distribuire il pool pilota di Lync Server 2013 è necessario aggiornare le voci A host DNS per il pool pilota. Per eseguire correttamente questa procedura, è necessario connettersi al server o al dominio almeno come membro del gruppo Domain Admins o DnsAdmins.

**Per configurare i record A dell'host DNS**

1.  Nel server DNS (Domain Name System) fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **DNS** .

2.  Nell'albero della console per il dominio espandere **Zone di ricerca diretta** e quindi fare clic con il pulsante destro del mouse sul dominio in cui verrà installato Lync Server 2013.

3.  Scegliere **Nuovo host (A o AAAA)** .

4.  Fare clic su **Nome** e digitare il nome host per il pool. Il nome di dominio viene presupposto dalla zona in cui è definito il record e non deve essere immesso come parte del record A.

5.  Fare clic su **Indirizzo IP** e digitare l'indirizzo IP del pool Front End.

6.  Fare clic su **Aggiungi host** e quindi su **OK** .

7.  Al termine, scegliere **Fine** .

