---
title: Configurazione dei criteri globali per l'archiviazione
TOCTitle: Configurazione dei criteri globali per l'archiviazione
ms:assetid: 58341d6b-c3ff-4dd9-b1c7-0048f33861ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204906(v=OCS.15)
ms:contentKeyID: 49300608
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei criteri globali per l'archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-09_

Quando si distribuiscono i Front End Server, Lync Server crea criteri globali per l'archiviazione. Per impostazione predefinita, nei criteri globali l'archiviazione è disabilitata. I criteri globali controllano se l'archiviazione è abilitata per le comunicazioni interne ed esterne nell'intera distribuzione, a meno che non si impostino criteri a livello di sito o di utente, che forzano i criteri globali, o a meno che non si usi l'integrazione di Microsoft Exchange per alcuni utenti o per tutti. Se si usa l'integrazione di Microsoft Exchange, i criteri globali non si applicano agli utenti disponibili in Exchange 2013 e con cassette postali impostate per l'archiviazione sul posto.

Per informazioni dettagliate sul funzionamento dei criteri di archiviazione, compresa la gerarchia dei criteri globali, a livello di sito e a livello di utente, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Se si abilita l'integrazione di Microsoft Exchange per la distribuzione, i criteri di archiviazione sul posto di Exchange controllano se l'archiviazione deve essere abilitata per gli utenti disponibili in Exchange 2013 e con cassette postali impostate per l'archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.<BR>Prima di abilitare l'archiviazione, è necessario specificare tutte le opzioni appropriate nelle configurazioni di archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-configuring-archiving-options.md">Configurazione delle opzioni di archiviazione</A> nella documentazione relativa alla distribuzione.



## Per configurare i criteri globali per l'archiviazione usando database di archiviazione di Lync Server

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server 2013. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server 2013, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Criteri di archiviazione**.

4.  Nella pagina **Criteri di archiviazione**fare clic su **Globale**, **Modifica** e quindi su **Mostra dettagli**.

5.  In **Modifica Criteri di archiviazione - Globale** eseguire le operazioni seguenti:
    
      - In **Nome**, se non si vuole usare il nome predefinito Globale, specificare un nuovo nome per i criteri globali.
    
      - In **Descrizione** immettere le informazioni sui criteri, ad esempio "Criteri globali per *nomeDivisione*".
    
      - Per controllare l'archiviazione delle comunicazioni interne per tutti i siti e gli utenti non controllati in modo specifico tramite criteri utente o sito, selezionare o deselezionare la casella di controllo **Archivia comunicazioni interne**.
    
      - Per controllare l'archiviazione delle comunicazioni esterne per tutti i siti e gli utenti non controllati in modo specifico tramite criteri utente o di sito, selezionare o deselezionare la casella di controllo **Archivia comunicazioni esterne**.

6.  Fare clic su **Commit**.

