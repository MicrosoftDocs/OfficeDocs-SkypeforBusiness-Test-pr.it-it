---
title: 'Lync Server 2013: Modifica delle impostazioni predefinite dei PIN per le conferenze telefoniche con accesso esterno'
TOCTitle: Modifica delle impostazioni predefinite dei PIN per le conferenze telefoniche con accesso esterno
ms:assetid: 2d110e94-ad29-4755-b17f-d8c2da9b78a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425780(v=OCS.15)
ms:contentKeyID: 49300037
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifica delle impostazioni predefinite dei PIN per le conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-18_

Il criterio PIN globale definisce le regole per i PIN delle conferenze telefoniche con accesso esterno a livello della foresta. Eseguire questa procedura per modificare tale criterio. Per informazioni dettagliate sulla creazione o la modifica di un criterio PIN per conferenze telefoniche con accesso esterno a livello di sito o utente, vedere [Creare o modificare le impostazioni del PIN di conferenza telefonica con accesso esterno in Lync Server 2013 per un sito o un gruppo di utenti](lync-server-2013-create-or-modify-dial-in-conferencing-pin-settings-for-a-site-or-group-of-users.md).

## Per modificare il criterio PIN globale

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Criteri PIN** .

4.  Nella pagina **Criteri PIN** fare clic sul criterio **Globale** , su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Modifica criterio PIN** , in **Lunghezza minima PIN** , digitare o selezionare la lunghezza minima che si desidera consentire per il PIN. La lunghezza minima predefinita è di cinque cifre.

6.  Per poter specificare il numero massimo di tentativi di accesso prima che un utente venga bloccato, selezionare la casella di controllo **Specifica numero massimo di tentativi di accesso** . Se non si seleziona questa opzione, il numero massimo di tentativi consentiti viene determinato automaticamente in base alla lunghezza del PIN. Per impostazione predefinita, il numero massimo di tentativi viene determinato automaticamente.

7.  Se si seleziona la casella di controllo **Specifica numero massimo di tentativi di accesso** , in **Numero massimo di tentativi di accesso** digitare o selezionare il numero massimo di tentativi di accesso che si desidera consentire.

8.  Per impostare una scadenza per i PIN, selezionare la casella di controllo **Abilita scadenza PIN** . Se non si seleziona questa opzione, i PIN non scadranno mai, come da impostazione predefinita.

9.  Se si seleziona la casella di controllo **Abilita scadenza PIN** , in **Scadenza PIN dopo (giorni)** digitare o selezionare il numero di giorni trascorsi i quali scadranno i PIN.

10. In **Conteggio cronologia PIN** digitare il numero di PIN che deve creare un utente prima che possa riutilizzare un PIN. Per impostazione predefinita, gli utenti possono riutilizzare i loro PIN.

11. Per consentire schemi comuni di cifre nei PIN, ad esempio numeri progressivi o gruppi ripetuti di numeri, selezionare la casella di controllo **Consenti formati comuni** . Se non si seleziona questa opzione, saranno consentiti solo schemi complessi di cifre, come da impostazione predefinita.
    
    > [!important]  
    > È consigliabile evitare di consentire i formati comuni.

12. Fare clic su **Commit** .

