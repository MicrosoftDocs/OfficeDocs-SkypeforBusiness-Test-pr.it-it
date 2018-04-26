---
title: Abilitare il controllo delle chiamate remote
TOCTitle: Abilitare il controllo delle chiamate remote
ms:assetid: 0b91d418-e6ed-4556-97af-e8523e01f249
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204664(v=OCS.15)
ms:contentKeyID: 49299642
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare il controllo delle chiamate remote

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Il controllo delle chiamate remote consente agli utenti di controllare i telefoni PBX da tavolo utilizzando Lync Server 2013. Se nell'ambiente legacy è stato distribuito il controllo delle chiamate remote e si desidera effettuarne la migrazione in Lync Server 2013, è necessario eseguire le attività seguenti:

1.  Installare un gateway SIP/CSTA e configurarlo per la comunicazione con il PBX. È necessario completare questo passaggio durante la distribuzione del pool pilota di Lync Server 2013.

2.  Dopo aver unito la topologia e aver eseguito la migrazione di criteri e impostazioni, configurare Lync Server 2013 per instradare le richieste CSTA al gateway SIP/CSTA. Questo passaggio deve essere eseguito manualmente dopo la migrazione automatizzata. Per configurare il routing per le richieste CSTA, eseguire le operazioni seguenti:
    
      - Rimuovere le voci host autorizzate legacy, denominate *voci del server trusted* in Lync Server 2013. Se si esegue la migrazione degli utenti dalla distribuzione legacy, assicurarsi di rimuovere tutte le voci host autorizzate esistenti create per il gateway SIP/CSTA prima di configurare nuove voci di applicazioni attendibili nel pool pilota di Lync Server 2013. Per informazioni dettagliate su come rimuovere le voci host autorizzate legacy, vedere [Rimuovere una voce host autorizzata](remove-an-authorized-host-entry.md).
    
      - Configurare una route statica per il controllo delle chiamate remote. È possibile configurare una route statica per i singoli pool che si desidera supportino il controllo delle chiamate remote oppure una route statica globale in modo che ogni pool non configurato con una route statica a livello di pool utilizzi la route statica globale. Per informazioni dettagliate su come configurare la route statica, vedere [Configurare una route statica per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-static-route-for-remote-call-control.md) nella documentazione relativa alla distribuzione.
    
      - Configurare una voce applicazione attendibile per il controllo delle chiamate remote in ogni pool per il quale si desidera il supporto per il controllo delle chiamate remote. Per informazioni dettagliate su come configurare una voce applicazione attendibile, vedere [Configurare una voce applicazione attendibile per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md) nella documentazione relativa alla distribuzione.

3.  Se è stato distribuito un gateway SIP/CSTA che utilizza TCP (Transmission Control Protocol) per la connessione a Lync Server 2013, definire l'indirizzo IP del gateway nel Generatore di topologie. Per informazioni dettagliate su come definire l'indirizzo IP, vedere [Definire l'indirizzo IP di un gateway SIP/CSTA in Lync Server 2013](lync-server-2013-define-a-sip-csta-gateway-ip-address.md) nella documentazione relativa alla distribuzione.

4.  Configurare gli utenti di Lync 2013 per il controllo delle chiamate remoto abilitando questa funzionalità e assegnando un URI (Uniform Resource Identifier) di server di linea e un URI di linea. Quando si esegue la migrazione degli utenti dalla distribuzione legacy a Lync Server 2013, vengono trasferite anche le impostazioni del controllo delle chiamate remote insieme alle altre impostazioni utente.

5.  Se nella distribuzione legacy sono state personalizzate le regole di normalizzazione dei numeri di telefono della Rubrica, è necessario eseguire alcune attività manuali al termine della migrazione automatizzata di criteri e impostazioni per eseguire la migrazione delle regole di normalizzazione personalizzate. Se tali regole non sono state personalizzate, la migrazione della Rubrica viene eseguita insieme al resto della topologia. Per informazioni dettagliate sulla migrazione manuale delle regole di normalizzazione personalizzate, vedere [Eseguire la migrazione della rubrica](migrate-address-book_1.md).

