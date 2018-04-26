---
title: Abilitare o disabilitare la modalità critica per bloccare o consentire sessioni di messaggistica istantanea e Web Conferencing se l'archiviazione non riesce
TOCTitle: Abilitare o disabilitare la modalità critica per bloccare o consentire sessioni di messaggistica istantanea e Web Conferencing se l'archiviazione non riesce
ms:assetid: fafdcd2e-b778-4ed5-a25f-09208aa3b699
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182609(v=OCS.15)
ms:contentKeyID: 49302552
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare la modalità critica per bloccare o consentire sessioni di messaggistica istantanea e Web Conferencing se l'archiviazione non riesce

 

_**Ultima modifica dell'argomento:** 2013-02-23_

In Pannello di controllo di Lync Server 2013 utilizzare le configurazioni per l'archiviazione per abilitare e disabilitare la modalità critica. Sono incluse le seguenti configurazioni per l'archiviazione:

  - Una configurazione globale creata per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Configurazioni facoltative a livello di sito e di pool che è possibile creare e utilizzare per specificare come viene implementata l'archiviazione per siti o protocolli specifici.

Le configurazioni per l'archiviazione vengono inizialmente impostate quando si distribuisce l'archiviazione, ma è possibile modificare, aggiungere ed eliminare le configurazioni dopo la distribuzione. Per informazioni dettagliate su come vengono implementate le configurazioni per l'archiviazione, incluse le opzioni che è possibile specificare e la gerarchia delle configurazioni per l'archiviazione, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione e alle operazioni.


> [!NOTE]
> Per utilizzare l'archiviazione, è necessario configurare i criteri di archiviazione per specificare se abilitare l'archiviazione per le comunicazioni interne, esterne o entrambe per gli utenti ospitati in Lync Server 2013. Per impostazione predefinita, l'archiviazione non è abilitata per le comunicazioni interne o esterne. Prima di abilitare l'archiviazione nei criteri, specificare le configurazioni appropriate per l'archiviazione per la distribuzione e, facoltativamente, per siti e pool specifici, come descritto in questa sezione. Per informazioni dettagliate sull'abilitazione dell'archiviazione, vedere <A href="lync-server-2013-configuring-and-assigning-archiving-policies.md">Configurazione e assegnazione dei criteri di archiviazione</A> nella documentazione relativa alla distribuzione.<BR>Dopo la distribuzione dell'archiviazione, se si decide di utilizzare l'integrazione con Exchange Server per archiviare i dati e i file di archiviazione nei server Exchange 2013 e tutti gli utenti sono ospitati nei server Exchange 2013, rimuovere la configurazione del database SQL Server dalla topologia. Per eseguire tale operazione, è necessario utilizzare il Generatore di topologie. Per informazioni dettagliate, vedere <A href="lync-server-2013-changing-archiving-database-options.md">Modifica delle opzioni del database di archiviazione in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Per abilitare o disabilitare il blocco della messaggistica istantanea e delle sessioni di conferenza Web, in caso di errore dell'archiviazione

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Fare clic sul nome della configurazione globale, di sito o pool appropriata nell'elenco delle configurazioni per l'archiviazione, su **Modifica**, su **Mostra dettagli** e quindi eseguire le operazioni seguenti:

5.  Per impostare il comportamento dell'archiviazione in caso di errore, selezionare o deselezionare la casella di controllo **Blocca sessioni di messaggistica istantanea o Web Conferencing se l'archiviazione non riesce**.

6.  Fare clic su **Commit**.

## Abilitazione e disabilitazione della modalità critica utilizzando i cmdlet Lync ServerWindows PowerShell

È possibile abilitare o disabilitare le modalità critica utilizzando il cmdlet **Set-CsArchivingConfiguration**. È possibile eseguire il cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Abilitazione della modalità critica

  - Per abilitare la modalità critica, impostare il valore della proprietà BlockOnArchiveFailure su True ($True). Ad esempio:
    
        Set-CsArchivingConfiguration -Identity "site:Redmond" -BlockOnArchiveFailure $True

## Disabilitazione della modalità critica

  - Per disabilitare la modalità critica, impostare il valore della proprietà BlockOnArchiveFailure su False ($False). Ad esempio:
    
        Set-CsArchivingConfiguration -Identity "site:Redmond" -BlockOnArchiveFailure $False

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Set-CsArchivingConfiguration](set-csarchivingconfiguration.md).

## Vedere anche

#### Attività

[Modifica delle opzioni del database di archiviazione in Lync Server 2013](lync-server-2013-changing-archiving-database-options.md)  

#### Concetti

[Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md)  

#### Ulteriori risorse

[Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)

