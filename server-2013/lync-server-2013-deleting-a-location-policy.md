---
title: Eliminazione di criteri percorso
TOCTitle: Eliminazione di criteri percorso
ms:assetid: 8ca9ba10-f45f-435a-b39c-519d251e9085
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688125(v=OCS.15)
ms:contentKeyID: 49887645
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione di criteri percorso

 

_**Ultima modifica dell'argomento:** 2012-10-10_

In Lync Server 2013, è possibile usare i criteri di posizione per applicare impostazioni correlate alla funzionalità Enhanced 9-1-1 (E9-1-1) e alle impostazioni di posizione per utenti o contatti. I criteri di posizione determinano se un utente è abilitato per E9-1-1 e in questo caso il funzionamento di una chiamata di emergenza. Ad esempio, è possibile usare i criteri di posizione per definire il numero di emergenza (ad esempio il 113 in Italia), se la sicurezza aziendale deve essere automaticamente notificata e come instradare la chiamata.

È possibile configurare i criteri di posizione dal gruppo **Configurazione di rete** in Pannello di controllo di Lync Server 2013. Da Pannello di controllo di Lync Server è possibile visualizzare, creare, modificare ed eliminare i criteri di posizione. Usare le procedure seguenti per eliminare un criteri di posizione. Per dettagli sulla creazione o la modifica di criteri di posizione, vedere [Creazione o modifica di criteri percorso](lync-server-2013-creating-or-modifying-a-location-policy.md).

## Per eliminare un criterio di posizione

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri percorso** .

4.  Nella pagina **Criteri percorso** selezionare il criterio percorso che si desidera eliminare.
    

    > [!NOTE]
    > È possibile eliminare più criteri percorso contemporaneamente. A tale scopo, tenere premuto CTRL e selezionare i diversi criteri. In alternativa, per selezionare tutti i criteri, scegliere <STRONG>Seleziona tutto</STRONG> dal menu <STRONG>Modifica</STRONG> .



5.  Scegliere **Elimina** dal menu **Modifica** .

6.  Fare clic su **OK**.
    
    > [!important]  
    > Non è possibile eliminare il criterio percorso Globale. Se si tenta di eliminare tale criterio, verrà visualizzato un messaggio di avviso e il criterio verrà reimpostato sui relativi valori predefiniti.

## Vedere anche

#### Attività

[Creazione o modifica di criteri percorso](lync-server-2013-creating-or-modifying-a-location-policy.md)  
[Visualizzazione delle informazioni sui criteri percorso](lync-server-2013-viewing-location-policy-information.md)

