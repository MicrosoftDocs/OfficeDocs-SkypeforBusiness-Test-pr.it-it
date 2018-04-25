---
title: 'Lync Server 2013: Assegnare i criteri di conferenza per supportare gli utenti anonimi'
TOCTitle: Assegnare i criteri di conferenza per supportare gli utenti anonimi
ms:assetid: 662de022-1111-40f7-bad4-f2b686f30973
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521007(v=OCS.15)
ms:contentKeyID: 49300806
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare i criteri di conferenza per supportare gli utenti anonimi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Per impostazione predefinita, a tutti gli utenti è proibito invitare utenti anonimi a partecipare a una riunione. È possibile decidere chi può invitare utenti anonimi configurando un criterio di conferenza che li supporti e applicando tale criterio a utenti specifici. Per informazioni dettagliate su come configurare criteri di conferenza per supportare utenti anonimi, vedere [Creare o modificare criteri conferenza](lync-server-2013-create-or-modify-a-conferencing-policy.md) e [Gestione della federazione e dell'accesso esterno a Lync Server 2013](lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md).

Utilizzare la procedura in questa sezione per applicare criteri di conferenza già creati a uno o più utenti o gruppi di utenti.


> [!NOTE]
> Oltre alla configurazione e all'applicazione di criteri per consentire agli utenti di invitare utenti anonimi, è inoltre necessario abilitare il supporto degli utenti anonimi per l'organizzazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-configure-policies-to-control-public-user-access.md">Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013</A>.



## Per configurare i criteri utente per la partecipazione anonima alle riunioni

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi eseguire una delle operazioni seguenti:
    
    1.  Per creare nuovi criteri utente, fare clic su **Nuovo** e quindi su **Criteri utente** . Creare un nome univoco nel campo **Nome** che indichi lo scopo dei criteri, ad esempio **AbilitaAnonimi** per criteri utente per l'abilitazione delle comunicazioni per gli utenti anonimi.
    
    2.  Per configurare criteri utente esistenti, fare clic sui criteri appropriati indicati nella tabella, fare clic su **Modifica** e quindi fare clic su **Mostra dettagli** .

4.  Nella finestra di dialogo **Criteri conferenza** selezionare la casella di controllo **Consenti ai partecipanti di invitare utenti anonimi** .

5.  Fare clic su **Commit** .

6.  Sulla barra di spostamento sinistra fare clic su **Utenti** e quindi cercare l'account utente che si desidera configurare.

7.  Nella tabella in cui sono elencati i risultati della ricerca fare clic sull'account utente, su **Modifica** e quindi su **Mostra dettagli** .

8.  In **Modifica utente di Lync Server** in **Criteri conferenza** selezionare i criteri utente con la configurazione per l'accesso degli utenti anonimi che si desidera applicare all'utente.
    

    > [!NOTE]
    > Le impostazioni <STRONG>&lt;Automatico&gt;</STRONG> si applicano alle impostazioni di installazione predefinite del server e vengono applicate automaticamente dal server.



Per consentire agli utenti di invitare utenti anonimi alle conferenze, è necessario abilitare anche il supporto per gli utenti anonimi nell'organizzazione. Per informazioni dettagliate, vedere [Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013](lync-server-2013-configure-policies-to-control-public-user-access.md) nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.

