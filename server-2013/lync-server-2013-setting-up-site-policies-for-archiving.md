---
title: Configurazione dei criteri sito per l'archiviazione
TOCTitle: Configurazione dei criteri sito per l'archiviazione
ms:assetid: dc2ea206-8b9c-44dd-a479-efb217593c89
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205325(v=OCS.15)
ms:contentKeyID: 49302184
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei criteri sito per l'archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-09_

È possibile abilitare o disabilitare l'archiviazione per siti specifici creando e configurando criteri di archiviazione per ognuno di questi siti. I criteri sito sostituiscono i criteri globali, mentre i criteri utente sostituiscono i criteri sito. I criteri di archiviazione si applicano solo se non si utilizza l'integrazione con Microsoft Exchange oppure se, pur utilizzando l'integrazione con Microsoft Exchange, alcuni utenti non sono ospitati in Exchange 2013 e dispongono di cassette postali con archiviazione sul posto.

Per informazioni dettagliate sul funzionamento dei criteri di archiviazione, inclusa la gerarchia per i criteri globali, sito e utente, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Se si abilita l'integrazione con Microsoft Exchange per la distribuzione, i criteri di archiviazione sul posto di Exchange definiscono se l'archiviazione è abilitata per gli utenti ospitati in Exchange 2013 e con le cassette postali con archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.<BR>È consigliabile specificare tutte le opzioni appropriate nella configurazioni di archiviazione prima di abilitare l'archiviazione di comunicazioni interne o esterne nei criteri di archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-configuring-archiving-options.md">Configurazione delle opzioni di archiviazione</A> nella documentazione relativa alla distribuzione.



## Per creare criteri di archiviazione per un sito

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server 2013.

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Criteri di archiviazione**.
    
    Per informazioni dettagliate sul funzionamento dei criteri di archiviazione, inclusa la gerarchia per i criteri globali, sito e utente, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.

4.  Fare clic su **Nuovo** e quindi su **Criteri sito**.

5.  In **Seleziona un sito** fare clic sul sito a cui devono essere applicati i criteri.

6.  In **Crea nuovi criteri di archiviazione** eseguire le operazioni seguenti:
    
      - In **Nome** specificare il nomi per il criterio sito.
    
      - In **Descrizione** immettere informazioni sullo scopo del criterio sito, ad esempio "Criterio sito per Redmond".
    
      - Per definire l'archiviazione delle comunicazioni interne per il sito specificato, selezionare o deselezionare la casella di controllo **Archivia comunicazioni interne**.
    
      - Per definire l'archiviazione delle comunicazioni esterne per il sito specificato, selezionare o deselezionare la casella di controllo **Archivia comunicazioni esterne**.

7.  Fare clic su **Commit**.

