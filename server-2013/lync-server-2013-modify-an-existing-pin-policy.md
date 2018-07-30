---
title: Modificare criteri per il PIN esistenti
TOCTitle: Modificare criteri per il PIN esistenti
ms:assetid: 517caaee-3349-4fa6-8d86-e4da3258a445
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520993(v=OCS.15)
ms:contentKeyID: 49300569
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare criteri per il PIN esistenti

 

_**Ultima modifica dell'argomento:** 2012-06-19_

È possibile utilizzare la scheda **Criterio PIN** per fornire l'autenticazione tramite PIN (Personal Identification Number) agli utenti che si connettono a Lync 2013 con telefoni IP. Per poter utilizzare l'autenticazione tramite PIN, verificare che l'opzione **Abilita autenticazione tramite PIN** sia selezionata nelle impostazioni del servizio Web. Per informazioni dettagliate, vedere [Modificare le impostazioni di configurazione del servizio Web esistente](lync-server-2013-modify-existing-web-service-configuration-settings.md).

Eseguire questa procedura per modificare un criterio PIN a livello di utente o di sito.

## Per modificare un criterio PIN esistente

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Sicurezza** e quindi su **Criteri PIN**.

4.  Nella pagina **Criteri PIN** fare clic su criterio, fare clic su **Modifica** e quindi su **Mostra dettagli**.

5.  In **Modifica criterio PIN**, in **Lunghezza minima PIN**, digitare o selezionare la lunghezza minima che si desidera consentire per il PIN. La lunghezza minima predefinita è di cinque cifre.

6.  Per poter specificare il numero massimo di tentativi di accesso prima che un utente venga bloccato, selezionare la casella di controllo **Specifica numero massimo di tentativi di accesso**. Se non si seleziona questa opzione, il numero massimo di tentativi consentiti viene determinato automaticamente in base alla lunghezza del PIN. Per impostazione predefinita, il numero massimo di tentativi viene determinato automaticamente.

7.  Se si seleziona la casella di controllo **Specifica numero massimo di tentativi di accesso**, in **Numero massimo di tentativi di accesso** digitare o selezionare il numero massimo di tentativi di accesso che si desidera consentire.

8.  Per impostare una scadenza per i PIN, selezionare la casella di controllo **Abilita scadenza PIN**. Se non si seleziona questa opzione, i PIN non scadranno mai, come da impostazione predefinita.

9.  Se si seleziona la casella di controllo **Abilita scadenza PIN**, in **Scadenza PIN dopo (giorni)** digitare o selezionare il numero di giorni trascorsi i quali scadranno i PIN.

10. In **Conteggio cronologia PIN** digitare il numero di PIN che deve creare un utente prima che possa riutilizzare un PIN. Per impostazione predefinita, gli utenti possono riutilizzare i loro PIN.

11. Per consentire schemi comuni di cifre nei PIN, ad esempio numeri progressivi o gruppi ripetuti di numeri, selezionare la casella di controllo **Consenti formati comuni**. Se non si seleziona questa opzione, saranno consentiti solo schemi complessi di cifre, come da impostazione predefinita.
    
    > [!IMPORTANT]  
    > È consigliabile evitare di consentire i formati comuni.

12. Fare clic su **Commit**.

