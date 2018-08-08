---
title: "Lync Server 2013: Gestisce opz. di config. dell'archiviaz. per az., siti e pool"
TOCTitle: "Lync Server 2013: Gestisce opz. di config. dell'archiviaz. per az., siti e pool"
ms:assetid: 377a6f80-5f2b-4bc1-b507-e930a461fb1d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204802(v=OCS.15)
ms:contentKeyID: 49300209
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Nel Pannello di controllo di Lync Server 2013 è possibile usare le configurazioni di Archiviazione per specificare il modo in cui l'archiviazione deve essere implementata. Sono incluse le configurazioni seguenti:

  - Una configurazione globale creata per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Configurazioni facoltative a livello di sito e a livello di pool che è possibile creare e usare per specificare il modo in cui l'archiviazione deve essere implementata per siti o pool specifici.

Le configurazioni di Archiviazione vengono specificate inizialmente in fase di distribuzione, tuttavia è possibile modificare, aggiungere ed eliminare le configurazioni dopo la distribuzione. Nel Pannello di controllo di Lync Server 2013 è possibile usare la pagina **Configurazione archiviazione** del gruppo **Monitoraggio e archiviazione** per gestire le configurazioni a livello globale, a livello di sito e a livello di pool. Per informazioni dettagliate sull'implementazione delle configurazioni di Archiviazione, incluse la gerarchia delle configurazioni di Archiviazione e le opzioni che è possibile specificare, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Per usare l'archiviazione, è necessario configurare i criteri di Archiviazione in modo da specificare se abilitare l'archiviazione per le comunicazioni interne, per le comunicazioni esterne o per entrambe per tutti gli utenti disponibili in Lync Server 2013. Per impostazione predefinita, l'archiviazione non è abilitata per le comunicazioni interne o esterne. Se si usa l'integrazione di Microsoft Exchange, è necessario abilitare e configurare Exchange 2013 per il supporto dell'archiviazione per tutti gli utenti disponibili in Exchange 2013 le cui caselle di posta siano state impostate sullo stato Archiviazione sul posto.<BR>Prima di abilitare Archiviazione, è necessario specificare le configurazioni di Archiviazione appropriate per la distribuzione e, facoltativamente, per siti e pool specifici, come descritto in questa sezione. Per informazioni dettagliate sull'abilitazione di Archiviazione, vedere <A href="lync-server-2013-configuring-and-assigning-archiving-policies.md">Configurazione e assegnazione dei criteri di archiviazione</A> nella documentazione relativa alla distribuzione.



**Per visualizzare informazioni sulla configurazione di Archiviazione tramite i cmdlet di Lync Server Management Shell**

  - È inoltre possibile visualizzare informazioni sulla configurazione di Archiviazione utilizzando Lync ServerWindows PowerShell e il cmdlet **Get-CsArchivingConfiguration**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).
    
    In Lync Server Management Shell usare il comando seguente per visualizzare informazioni su tutte le impostazioni di configurazione dell'archiviazione:
    
        Get-CsArchivingConfiguration

## Argomenti della sezione

  - [Creazione di una configurazione dell'archiviazione per gestire l'archiviazione per specifici siti o pool](lync-server-2013-creating-an-archiving-configuration-to-manage-archiving-for-specific-sites-or-pools.md)

  - [Abilitazione o disabilitazione dell'archiviazione delle sessioni di messaggistica istantanea e di conferenza](lync-server-2013-enabling-or-disabling-archiving-of-im-or-conferencing-sessions.md)

  - [Abilitazione o disabilitazione dell'eliminazione dei dati archiviati](lync-server-2013-enabling-or-disabling-the-purging-of-archived-data.md)

  - [Abilitare o disabilitare la modalità critica per bloccare o consentire sessioni di messaggistica istantanea e Web Conferencing se l'archiviazione non riesce](lync-server-2013-enabling-or-disabling-critical-mode-to-block-or-allow-im-and-web-conferencing-sessions-if-archiving-fails.md)

  - [Abilitare o disabilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione ai partner federati in Lync Server 2013](lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md)

  - [Abilitazione o disabilitazione dell'integrazione con l'archiviazione di Exchange](lync-server-2013-enabling-or-disabling-integration-with-exchange-storage.md)

  - [Eliminazione della configurazione di archiviazione](lync-server-2013-deleting-an-archiving-configuration.md)

## Vedere anche

#### Ulteriori risorse

[Gestione dell'archiviazione in Lync Server 2013](lync-server-2013-managing-archiving.md)

