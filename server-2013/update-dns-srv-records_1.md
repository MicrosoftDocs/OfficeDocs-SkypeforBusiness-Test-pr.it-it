---
title: Aggiornare i record SRV DNS
TOCTitle: Aggiornare i record SRV DNS
ms:assetid: a29149aa-30cc-4a59-af98-fb95c2385cce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688161(v=OCS.15)
ms:contentKeyID: 49887687
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiornare i record SRV DNS

 

_**Ultima modifica dell'argomento:** 2012-09-29_

Per eseguire correttamente questa procedura, è necessario connettersi al server o al dominio come membro del gruppo Domain Admins o DnsAdmins.

In questo argomento viene illustrato come aggiornare i record DNS (Domain Name System) dopo la migrazione in Lync Server 2013. Dopo che tutti gli utenti sono stati spostati in Lync Server 2013, ma prima che vengano rimosse le autorizzazioni per il Director o il pool di Office Communications Server 2007 R2 legacy, è necessario aggiornare i record SRV DNS nel sistema DNS interno per ogni dominio SIP. Per questa procedura si presuppone che nel sistema DNS interno siano disponibili zone per i domini utente SIP.

**Per configurare un record DNS SRV**

1.  Nel server DNS fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **DNS** .

2.  Nell'albero della console per il dominio SIP espandere **Zone di ricerca diretta** , espandere il dominio SIP in cui è installato Lync Server 2013 e passare all'impostazione **\_tcp**.

3.  Nel riquadro destro fare clic con il pulsante destro del mouse su **\_sipinternaltls** e scegliere **Proprietà**.

4.  In **Host che offre questo servizio** aggiornare il nome di dominio completo (FQDN) dell'host in modo che punti al pool di Lync Server 2013.

5.  Fare clic su **OK** .

**Per verificare che il nome di domino completo del pool Front End o del server Standard Edition possa essere risolto**

1.  Eseguire l'accesso a un computer client nel dominio.

2.  Fare clic sul pulsante **Start** e quindi scegliere **Esegui** .

3.  Nella casella **Apri** digitare **cmd** e quindi fare clic su **OK** .

4.  Al prompt dei comandi digitare **nslookup** *\<FQDN del pool Front End\>* o *\<FQDN del server Standard Edition\>* e quindi premere INVIO.

5.  Verificare di ricevere una risposta che si risolve nell'indirizzo IP appropriato per l'FQDN.

