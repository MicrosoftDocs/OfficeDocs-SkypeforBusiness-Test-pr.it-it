---
title: 'Lync Server 2013: Componenti e topologie per la messaggistica unificata locale'
TOCTitle: Componenti e topologie per la messaggistica unificata locale
ms:assetid: 22fc87cf-a7e5-4c8c-bb9b-101e5380cdcf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425711(v=OCS.15)
ms:contentKeyID: 49299931
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per la messaggistica unificata locale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-25_

In questo argomento vengono descritti i componenti di Microsoft Exchange Server 2013 necessari per garantire le funzionalità di Messaggistica unificata di Exchange alla distribuzione di Lync Server 2013 locale. Vengono inoltre illustrate le topologie supportate per l'integrazione della Messaggistica unificata di Exchange locale.

## Componenti di Exchange Server

Per fornire le funzionalità e i servizi di Messaggistica unificata di Exchange descritti in [Funzionalità della messaggistica unificata integrata e Lync Server 2013](lync-server-2013-features-of-integrated-unified-messaging.md) per gli utenti di VoIP aziendale nell'organizzazione, è necessario distribuire un server delle cassette postali di Microsoft Exchange e server Accesso client, che ospita le cassette postali degli utenti e offre una posizione di archiviazione singola per la posta elettronica e la segreteria telefonica. Messaggistica unificata di Exchange viene eseguito come servizio nei server delle cassette postali di Exchange e Accesso client.

Per informazioni sui componenti di messaggistica unificata di Exchange in Microsoft Exchange Server 2007 e Microsoft Exchange Server 2010, vedere [Distribuzione della messaggistica unificata di Exchange in locale per fornire la funzionalità di segreteria telefonica di Lync Server 2013](lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md) nella documentazione relativa alla distribuzione.

## Topologie supportate

È possibile distribuire Lync Server 2013 e Messaggistica unificata di Exchange nella stessa foresta o in più foreste. Se la distribuzione si estende su più foreste, è necessario eseguire i passaggi di integrazione di Exchange per ogni foresta di Messaggistica unificata di Exchange. È inoltre necessario configurare ogni foresta di Microsoft Exchange in modo che consideri attendibile la foresta di Lync Server 2013 e la foresta di Lync Server 2013 in modo che consideri attendibile ogni foresta di Messaggistica unificata di Exchange. Oltre a questa relazione di trust tra le foreste, le impostazioni di Messaggistica unificata di Exchange di tutti gli utenti devono essere configurate negli oggetti utente della foresta di Lync Server 2013.

Lync Server 2013 supporta le topologie seguenti per l'integrazione di Messaggistica unificata di Exchange:

  - Foresta singola

  - Singolo dominio, ovvero foresta singola con un solo dominio. Lync Server 2013, Microsoft Exchange e gli utenti si trovano tutti nello stesso dominio.

  - Dominio multiplo, ovvero un dominio radice con uno o più domini figlio. Lync Server 2013 e i server Microsoft Exchange sono distribuiti in domini diversi dal dominio in cui si creano gli utenti. I server di Messaggistica unificata di Exchange possono essere distribuiti in domini diversi dal pool di Lync Server 2013 supportato.

  - Foresta multipla, ovvero foresta di risorse. Lync Server 2013 viene distribuito in una singola foresta e quindi gli utenti vengono distribuiti in più foreste. Gli attributi di Messaggistica unificata di Exchange degli utenti devono essere replicati nella foresta di Lync Server 2013.
    

    > [!NOTE]
    > Exchange può essere distribuito in più foreste. Ogni organizzazione di Exchange può offrire la Messaggistica unificata di Exchange agli utenti oppure la Messaggistica unificata di Exchange può essere distribuito nella stessa foresta di Lync Server 2013.


