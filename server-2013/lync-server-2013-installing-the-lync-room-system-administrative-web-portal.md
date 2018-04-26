---
title: Installazione del portale Web amministrativo di Lync Room System
TOCTitle: Installazione del portale Web amministrativo di Lync Room System
ms:assetid: dd19e368-c338-4e21-a40d-6439d46a9748
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn436326(v=OCS.15)
ms:contentKeyID: 59602738
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione del portale Web amministrativo di Lync Room System

 

_**Ultima modifica dell'argomento:** 2015-04-09_

È possibile scaricare il portale Web amministrativo di Microsoft Lync Room System dall'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=324044](http://go.microsoft.com/fwlink/p/?linkid=324044).

Per installare il portale Web amministrativo di Lync Room System, eseguire i passaggi seguenti.

1.  Configurare la porta dell'applicazione attendibile eseguendo il cmdlet seguente in Lync Server Management Shell:
    
        Set-CsWebServer -Identity POOLFQDN -MeetingRoomAdminPortalInternalListeningPort 4456 -MeetingRoomAdminPortalExternalListeningPort 4457

2.  Per installare il portale della sala riunioni, scaricare **LyncRoomAdminPortal.exe** e quindi eseguirlo come amministratore.

3.  Aprire il file Web.config dal percorso seguente:
    
    %Program Files%\\Microsoft Lync Server 2013\\Web Components\\Meeting Room Portal\\Int\\Handler\\

4.  Nel file Web.Config sostituire PortalUserName con il nome utente creato nel passaggio 2 della sezione relativa alla configurazione dei prerequisiti per il portale di amministrazione di Lync Room System. Il nome consigliato nel passaggio è LRSApp:
    
        <add key="PortalUserName" value="sip:LRSApp@domain.com" />

5.  Poiché il portale di amministrazione di LRS è un'applicazione attendibile, non è necessario specificare la password durante la configurazione del portale. Se l'utente usa un servizio Registrazione avanzata diverso da quello locale, è necessario specificare tale servizio aggiungendo la riga seguente nel file Web.Config:
    
        <add key="PortalUserRegistrarFQDN" value="pool-xxxx.domain.com" />

6.  Se la porta usata è diversa dalla porta 5061, aggiungere la riga seguente nel file Web.Config:
    
        <add key="PortalUserRegistrarPort" value="5061" />

## Verifica dell'installazione del portale Web amministrativo di Lync Room System

Per verificare l'installazione del portale Web amministrativo di Lync Room System, eseguire le operazioni seguenti:


1.  In un server front-end passare all'URL seguente:
    
    https://\<server-front-end\>/lrs
    
    Non dovrebbe essere segnalato alcun errore, come illustrato nell'immagine seguente:
    
    ![Schermata di accesso al portale di amministrazione di Lync Room System](images/Dn436326.050bcf70-2f3b-46b2-9b96-ebd12679b713(OCS.15).png "Schermata di accesso al portale di amministrazione di Lync Room System")

2.  Se non viene segnalato alcun errore, provare ad accedere all'URL seguente da un altro computer qualsiasi della topologia:
    
    https://\<server-front-end\>/lrs
    
    Per accedere alla pagina, sarà necessario aggiungere i record DNS come descritto nella pagina relativa ai record DNS necessari per l'accesso client automatico all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=318056](http://go.microsoft.com/fwlink/p/?linkid=318056).

