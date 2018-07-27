---
title: 'Lync Server 2013: Definire un Survivable Branch Appliance o un Survivable Branch Server'
TOCTitle: Definire un Survivable Branch Appliance o un Survivable Branch Server
ms:assetid: 1f49cfbe-30b3-4600-af15-47cb2f58d18a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398280(v=OCS.15)
ms:contentKeyID: 49299890
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire un Survivable Branch Appliance o un Survivable Branch Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-07_

Eseguire questa procedura presso il sito centrale se la Survivable Branch Appliance o il Survivable Branch Server non è stato definito quando è stato aggiunto alla topologia.

## Per definire Survivable Branch Appliance o Survivable Branch Server

1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server 2013** e quindi fare clic su **Lync ServerGeneratore di topologie**.

2.  Nell'albero della console espandere il sito centrale, espandere **Siti di succursale** e quindi espandere il nome del sito di succursale in cui si prevede di distribuire Survivable Branch Appliance o Survivable Branch Server.

3.  Fare clic con il pulsante destro del mouse su **Survivable Branch Appliance** e quindi scegliere **New Survivable Branch Appliance**.
    
    > [!IMPORTANT]  
    > In <strong>Survivable Branch Appliance</strong> vengono definiti Survivable Branch Server e Survivable Branch Appliance.

4.  Nella finestra di dialogo **Definisci Survivable Branch Appliance** fare clic su **FQDN** , digitare il nome di dominio completo (FQDN) del Survivable Branch Appliance o del Survivable Branch Server che verrà distribuito nel sito di succursale e quindi fare clic su **Avanti** .
    
    > [!IMPORTANT]  
    > Se si definisce un Survivable Branch Appliance, il nome immesso in <strong>FQDN</strong> deve corrispondere all'FQDN di Survivable Branch Appliance assegnato all'attributo <strong>servicePrincipalName</strong> . Per informazioni dettagliate, vedere <a href="lync-server-2013-add-a-survivable-branch-appliance-to-active-directory.md">Aggiungere un Survivable Branch Appliance ad Active Directory in Lync Server 2013</a>.

5.  Fare clic su **Pool Front End** , sul Front End Server (pool di servizi utente) del sito centrale a cui si connetterà questo Survivable Branch Appliance o Survivable Branch Server e quindi fare clic su **Avanti** .

6.  Fare clic su **Server perimetrale** , sul pool di server perimetrali a cui si connetterà questo Survivable Branch Appliance o Survivable Branch Server per fornire la connettività PSTN agli utenti remoti del sito di succursale e quindi su **Avanti** .

7.  Fare clic su **FQDN gateway o indirizzo IP** e quindi digitare l'FQDN o l'indirizzo IP del peer gateway a cui è associato il Survivable Branch Appliance o Survivable Branch Server per il routing di chiamate PSTN in ingresso o in uscita.
    
    > [!IMPORTANT]  
    > Se si sta definendo un Survivable Branch Appliance, questo è il gateway a cui si connetterà il Mediation Server all'interno del Survivable Branch Appliance per la connettività PSTN.

8.  Fare clic su **Porta di attesa per gateway IP/PSTN** e quindi accettare la porta predefinita.

9.  In **Protocollo trasporto SIP** fare clic sul protocollo di trasporto che verrà utilizzato dal Survivable Branch Appliance o Survivable Branch Server e quindi fare clic su **Fine** .
    

    > [!NOTE]
    > Per motivi di sicurezza, è consigliabile utilizzare Transport Layer Security (TLS). Se si definisce un Survivable Branch Appliance, vedere la documentazione del fornitore del proprio Survivable Branch Appliance per verificare che il Survivable Branch Appliance supporti il protocollo TLS.



10. Nell'albero della console fare clic con il pulsante destro del mouse sul nuovo Survivable Branch Appliance o Survivable Branch Server, scegliere **Topologia** e quindi fare clic su **Pubblica** .

**Passaggio successivo**: [Distribuire un Survivable Branch Appliance o un Survivable Branch Server con Lync Server 2013 - Attività presso il sito di succursale](lync-server-2013-deploy-a-survivable-branch-appliance-or-server-branch-site-task.md)

