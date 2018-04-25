---
title: "Lync Server 2013: Presentazione dell'ID chiamante"
TOCTitle: Presentazione dell'ID chiamante
ms:assetid: 6a643961-a0a1-41d1-96ba-6c428a89d82e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204980(v=OCS.15)
ms:contentKeyID: 49300871
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Presentazione dell'ID chiamante in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Con Lync Server 2010, il numero di telefono dell'utente chiamato, ovvero il numero di telefono chiamato, può essere convertito dal formato E.164 nel formato di composizione locale richiesto dal *peer trunk* , ovvero il gateway, il centralino (PBX) o il trunk SIP associato. A tale scopo, è necessario definire una o più regole per la conversione dell'URI di richiesta prima del routing al peer trunk.

In Lync Server 2013 viene introdotta inoltre l'opzione per convertire il numero di telefono della parte chiamante (ovvero il numero di telefono da cui chiama il chiamante) dal formato E.164 al formato locale richiesto dal trunk peer. È ad esempio possibile scrivere una regola di conversione per rimuovere +44 da una stringa di composizione e sostituirlo con 0144.

**Per configurare l'ID chiamante tramite Pannello di controllo di Lync Server**

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Configurazione trunk** .

4.  Nella pagina **Configurazione trunk** fare doppio clic su un trunk esistente, ad esempio il trunk **Globale** per visualizzare la finestra di dialogo **Modifica configurazione trunk** .

5.  Per configurare la presentazione dell'ID chiamante:
    
      - Per selezionare una o più regole in un elenco di tutte le regole di conversione disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . In **Regola di conversione per il numero del chiamante** fare clic sulle regole da associare al trunk e quindi fare clic su **OK** .
    
      - Per definire una nuova regola di conversione e associarla al trunk, fare clic su **Nuovo** . Per informazioni dettagliate sulla definizione di una nuova regola, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per modificare una regola di conversione già associata al trunk, fare clic sul nome della regola e quindi fare clic su **Mostra dettagli** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per copiare una regola di conversione esistente in modo da utilizzarla come punto di partenza per definire una nuova regola, fare clic sul nome della regola, fare clic su **Copia** e quindi su **Incolla** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md).
    
      - Per rimuovere una regola di conversione dal trunk, evidenziare il nome della regola e fare clic su **Rimuovi** .
    

    > [!WARNING]
    > Non associare regole di conversione a un trunk se sono state configurate regole di conversione nel trunk peer associato, perché le due regole potrebbero essere in conflitto.


