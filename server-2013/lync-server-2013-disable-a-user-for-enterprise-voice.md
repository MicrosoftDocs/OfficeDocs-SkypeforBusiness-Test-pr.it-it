---
title: Disabilitare un utente per VoIP aziendale
TOCTitle: Disabilitare un utente per VoIP aziendale
ms:assetid: 462002d8-21df-4d77-bf7f-4d059d6a4bb2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688043(v=OCS.15)
ms:contentKeyID: 49887541
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disabilitare un utente per VoIP aziendale

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Attenersi alla procedura seguente per disabilitare VoIP aziendale per un account utente abilitato per Lync Server 2013.

## Per disabilitare un account utente per VoIP aziendale

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti**.

4.  Nella casella **Cerca utenti** digitare anche solo la prima parte del nome visualizzato, del nome, del cognome, del nome dell'account di Gestione account di protezione, dell'indirizzo SIP o dell'URI (Uniform Resource Identifier) di linea dell'account utente da abilitare e quindi fare clic su **Trova**.

5.  Nella tabella fare clic sull'account utente da abilitare per VoIP aziendale.

6.  Scegliere **Mostra dettagli** dal menu **Modifica**.

7.  Nella pagina **Modifica utente Lync Server**, in **Telefonia** fare clic su qualsiasi opzione, ad eccezione di **VoIP aziendale**.
    

    > [!NOTE]
    > Per impedire a un utente di effettuare chiamate audio o video utilizzando Lync, in <STRONG>Telefonia</STRONG> fare clic su <STRONG>Audio/video disabilitati</STRONG>.



8.  Fare clic su **Commit**.

L'utente ora non può utilizzare la funzionalità VoIP aziendale.

## Vedere anche

#### Attività

[Abilitare gli utenti per VoIP aziendale in Lync Server 2013](lync-server-2013-enable-users-for-enterprise-voice.md)  

#### Ulteriori risorse

[Gestione di VoIP aziendale per gli utenti](lync-server-2013-managing-enterprise-voice-for-users.md)  
[Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md)

