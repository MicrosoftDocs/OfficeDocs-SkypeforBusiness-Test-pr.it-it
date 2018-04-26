---
title: "Lync Server 2013: Configurare i criteri di conferenza per l'accesso esterno"
TOCTitle: Configurare i criteri di conferenza per l'accesso esterno
ms:assetid: 9bf926d6-0248-4352-98c3-9c5a333debbc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398810(v=OCS.15)
ms:contentKeyID: 49301471
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i criteri di conferenza per l'accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-03-21_

I criteri di conferenza sono impostazioni dell'account utente che definiscono l'esperienza di utilizzo delle conferenze da parte dei partecipanti. È possibile creare criteri di conferenza con un ambito sito o un ambito utente. Le impostazioni dei criteri di conferenza definiscono molti aspetti della pianificazione e della partecipazione alle conferenze. Diverse impostazioni dei criteri di conferenza supportano le conferenze telefoniche con accesso esterno dei partecipanti. Quando si configurano le conferenze telefoniche con accesso esterno, è consigliabile verificare che questi campi siano impostati in modo appropriato per l'organizzazione ed eventualmente modificarli in base alle proprie esigenze.

Verificare i campi seguenti nei criteri di conferenza:

  - **Consenti ai partecipanti di invitare utenti anonimi**    Questa impostazione consente agli organizzatori delle riunioni di invitare partecipanti anonimi, ovvero non autenticati. Per le conferenze telefoniche con accesso esterno, questa opzione è facoltativa. Nel criterio di conferenza globale predefinito, è selezionata per impostazione predefinita.

  - **Consenti conferenza telefonica con accesso esterno PSTN**    Questa impostazione consente agli utenti di partecipare alla parte audio di una conferenza eseguendo un accesso telefonico dalla rete PSTN. Per le conferenze telefoniche con accesso esterno, questa opzione è obbligatoria. Nel criterio di conferenza globale predefinito, è selezionata per impostazione predefinita.

  - **Consenti chiamate in uscita ai partecipanti anonimi**    Questa impostazione consente agli utenti anonimi (non autenticati) di partecipare alla parte audio di una conferenza utilizzando chiamate in uscita. Per le conferenze telefoniche con accesso esterno, questa opzione è facoltativa. Nel criterio di conferenza globale predefinito, è deselezionata per impostazione predefinita.

  - **Consenti chiamate in uscita ai partecipanti non abilitati per VoIP aziendale**   Questa impostazione consente ai partecipanti e agli organizzatori della riunione non abilitati per VoIP aziendale di chiamare un numero di telefono per partecipare alla parte audio della conferenza. La chiamata in uscita è autorizzata in base ai criteri vocali assegnati dall'organizzatore. Questa impostazione non è selezionata per impostazione predefinita nei criteri di conferenza globali. Per impostazione predefinita, questa opzione è disabilitata.
    

    > [!NOTE]
    > Per abilitare questa funzionalità, l'organizzatore di una riunione non abilitato per VoIP aziendale deve disporre di criteri vocali appropriati per autorizzare eventuali chiamate in uscita della conferenza. È possibile assegnare criteri vocali a un utente non abilitato per VoIP aziendale da Lync Server Management Shell. Se l'utente non dispone di criteri vocali assegnati esplicitamente, verranno usati i criteri vocali del sito per autorizzare la richiesta di chiamata in uscita. In assenza di criteri del sito, verranno utilizzati i criteri vocali globali.



La procedura illustrata in questa sezione spiega come modificare i criteri di conferenza. Per informazioni dettagliate su come configurare tutte le impostazioni che definiscono l'esperienza dei partecipanti nei criteri di conferenza predefiniti, vedere [Creare o modificare una raccolta di impostazioni di configurazione delle riunioni](lync-server-2013-create-or-modify-a-collection-of-meeting-configuration-settings.md). Per informazioni dettagliate su come creare un criterio di conferenza per un utente specifico o un gruppo di utenti, vedere [Creare o modificare criteri conferenza](lync-server-2013-create-or-modify-a-conferencing-policy.md). Per un elenco di tutte le impostazioni dei criteri di conferenza disponibili, vedere [Guida di riferimento alle impostazioni dei criteri di conferenza di Lync Server 2013](lync-server-2013-conferencing-policy-settings-reference.md).

## Per modificare i criteri di conferenza per le conferenze telefoniche con accesso esterno

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins o come membro del ruolo **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** .

4.  Nella scheda **Criteri conferenza** fare doppio clic sul nome di un di conferenza per aprire la finestra di dialogo **Modifica criteri conferenza** .

5.  Verificare che i campi per le conferenze telefoniche con accesso esterno siano appropriati per l'organizzazione e, se necessario, modificare le impostazioni.

6.  Fare clic su **Commit** .

