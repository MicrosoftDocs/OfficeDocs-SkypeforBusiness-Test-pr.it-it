---
title: Cercare utenti di Lync Server
TOCTitle: Cercare utenti di Lync Server
ms:assetid: 3b9f6f55-d7a9-46ae-8e10-f221ba0d3bb5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429701(v=OCS.15)
ms:contentKeyID: 49300256
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cercare utenti di Lync Server

 

_**Ultima modifica dell'argomento:** 2014-05-14_

È possibile utilizzare i risultati di una query di ricerca per configurare gli utenti per Lync Server 2013. È possibile ricercare utenti in base al nome visualizzato, al nome, al cognome, al nome dell'account SAM (Security Accounts Manager), all'indirizzo SIP o all'URI (Uniform Resource Identifier) della linea.

È possibile ricercare utenti utilizzando il Pannello di controllo di Lync Server oppure lo snap-in Utenti e computer di Active Directory. Nella procedura seguente viene descritto come usare il Pannello di controllo di Lync Server per cercare gli utenti.


> [!NOTE]
> In un ambiente con una topologia a foresta centralizzata i risultati della ricerca potrebbero non essere accurati se si esegue la ricerca di un utente in base all'indirizzo di posta elettronica. È possibile invece ricercare utenti specificando un prefisso di indirizzo SIP, ad esempio sip:nome. È possibile aggiungere un filtro di ricerca e selezionare un indirizzo SIP contenente un indirizzo di posta elettronica parziale oppure utilizzare il cmdlet <STRONG>Get-CSUser</STRONG>.



## Per ricercare uno o più utenti

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti**.

4.  Nella casella **Ricerca utenti** digitare interamente o parzialmente il nome visualizzato, il nome, il cognome, il nome account SAM, l'indirizzo SIP o l'URI linea dell'account utente da ricercare e quindi fare clic su **Trova**.

5.  (Facoltativo) Specificare criteri di ricerca aggiuntivi per ridurre i risultati:
    
    1.  Fare clic sul pulsante freccia di espansione nell'angolo in alto a destra della schermata al di sopra di **Risultati della ricerca** e quindi fare clic su **Aggiungi filtro**.
    
    2.  Digitare la proprietà utente oppure selezionarla facendo clic sulla freccia nell'elenco a discesa.
    
    3.  Nell'elenco **Uguale a** selezionare **Uguale a** o **Diverso da**.
    
    4.  Nella casella di testo digitare i criteri di ricerca che si desidera utilizzare per filtrare i risultati della ricerca e quindi fare clic su **Trova**.

6.  I risultati della ricerca verranno visualizzati al di sotto di **Risultati della ricerca**. È possibile selezionare uno o tutti gli utenti dell'elenco ed eseguire attività di configurazione sugli utenti selezionati.

## Vedere anche

#### Ulteriori risorse

[Visualizzazione delle informazioni sugli account utente abilitati per Lync Server 2013](lync-server-2013-viewing-information-about-user-accounts-enabled-for-lync-server.md)  
[Abilitazione e disabilitazione degli utenti per Lync Server 2013](lync-server-2013-enabling-and-disabling-users-for-lync-server.md)

