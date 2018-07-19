---
title: Creazione di una configurazione dell'archiviazione per gestire l'archiviazione per specifici siti o pool
TOCTitle: Creazione di una configurazione dell'archiviazione per gestire l'archiviazione per specifici siti o pool
ms:assetid: c5c864a6-96c7-4bbb-ab7c-61eb1744246c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205251(v=OCS.15)
ms:contentKeyID: 49301898
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione di una configurazione dell'archiviazione per gestire l'archiviazione per specifici siti o pool

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Nel Pannello di controllo di Lync Server 2013 le configurazioni di archiviazione consentono di definire come viene implementata l'archiviazione nella distribuzione. Sono incluse le configurazioni di archiviazione seguenti:

  - Una configurazione globale creata per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Configurazioni facoltative a livello di sito e di pool che possono essere create e utilizzate per specificare come deve essere implementata l'archiviazione per siti o pool specifici.

Le configurazioni di archiviazione vengono definite inizialmente al momento della distribuzione dell'archiviazione, ma è possibile modificarle, aggiungerle ed eliminarle dopo la distribuzione. Per informazioni dettagliate sul modo in cui vengono implementate le configurazioni di archiviazione, incluse le opzioni che è possibile specificare e la gerarchia delle configurazioni di archiviazione, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Per utilizzare l'archiviazione, è necessario configurare criteri di archiviazione per specificare se abilitare l'archiviazione per comunicazioni interne, comunicazioni esterne o per entrambi i tipi di comunicazioni per gli utenti ospitati in Lync Server 2013. Per impostazione predefinita, l'archiviazione non è abilitata per le comunicazioni interne o esterne. Prima di abilitare l'archiviazione nei criteri, è consigliabile specificare le configurazioni di archiviazione appropriate per la distribuzione e facoltativamente per siti e pool specifici, come descritto in questa sezione. Per informazioni dettagliate sull'abilitazione dell'archiviazione, vedere <A href="lync-server-2013-configuring-and-assigning-archiving-policies.md">Configurazione e assegnazione dei criteri di archiviazione</A> nella documentazione relativa alla distribuzione.<BR>Se dopo la distribuzione dell'archiviazione si decide che si desidera utilizzare l'integrazione con Microsoft Exchange per conservare i file e i dati di archiviazione nei server Exchange 2013 e tutti gli utenti sono ospitati in server Exchange 2013, rimuovere la configurazione del database di SQL Server dalla topologia. A tale scopo, è necessario utilizzare Generatore di topologie. Per informazioni dettagliate, vedere <A href="lync-server-2013-changing-archiving-database-options.md">Modifica delle opzioni del database di archiviazione in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Per creare una configurazione di archiviazione per un sito o un pool

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Nella pagina **Configurazione archiviazione** fare clic su **Nuovo** e quindi eseguire una delle operazioni seguenti:
    
      - Per creare una configurazione di archiviazione per un sito, fare clic su **Configurazione sito** e quindi in **Seleziona un sito** selezionare un sito da configurare per l'archiviazione.
    
      - Per creare una configurazione di archiviazione per un pool, fare clic su **Configurazione pool** e quindi in **Seleziona pool** selezionare un pool da configurare per l'archiviazione.

5.  Nell'elenco a discesa **Impostazione di archiviazione** in **Nuova impostazione di archiviazione** eseguire una delle operazioni seguenti:
    
      - Per abilitare l'archiviazione solo per le sessioni di messaggistica istantanea, fare clic su **Archivia sessioni di messaggistica istantanea**.
    
      - Per abilitare l'archiviazione per le sessioni di messaggistica istantanea e le conferenze Web, fare clic su **Archivia sessioni di messaggistica istantanea e Web Conferencing**.
    
      - Per disabilitare l'archiviazione dei criteri, fare clic su **Disabilita archiviazione**.

6.  Sempre in **Nuova impostazione di archiviazione** eseguire le operazioni seguenti:
    
      - Per bloccare l'attività quando l'archiviazione non è disponibile, selezionare la casella di controllo **Blocca sessioni di messaggistica istantanea o Web Conferencing se l'archiviazione non riesce**.
    
      - Per utilizzare Microsoft Exchange Server per memorizzare i dati di archiviazione, selezionare la casella di controllo **Integrazione Microsoft Exchange**.
    
      - Per abilitare l'eliminazione dei dati, selezionare la casella di controllo **Abilita eliminazione dei dati di archiviazione** e quindi eseguire una delle operazioni seguenti:
        
          - Per specificare l'eliminazione dopo un numero specifico di giorni, fare clic su **Elimina dati di archiviazione esportati e archiviati dopo durata massima (giorni)** e quindi specificare il numero di giorni.
        
          - Per limitare l'eliminazione ai dati di archiviazione esportati, fare clic su **Elimina solo i dati di archiviazione esportati**.

7.  Fare clic su **Commit**.

## Creazione delle impostazioni di configurazione di archiviazione mediante i cmdlet di Lync Server

Le impostazioni di configurazione di archiviazione possono essere create anche utilizzando Windows PowerShell e il cmdlet New-CsArchivingConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Creare una nuova raccolta di impostazioni di configurazione di archiviazione per un sito

  - Con il comando seguente viene creata una nuova raccolta di impostazioni di configurazione di archiviazione per il sito Redmond:
    
        New-CsArchivingConfiguration -Identity "site:Redmond"

## Creazione di una nuova raccolta di impostazioni di configurazione di archiviazione che consentono solo l'archiviazione della messaggistica istantanea

  - Poiché nel comando precedente non sono stati specificati parametri, eccetto il parametro obbligatorio Identity, la nuova raccolta di impostazioni di configurazione utilizzerà i valori predefiniti per le relative proprietà. Per creare impostazioni basate su valori di proprietà diversi, è sufficiente includere il parametro appropriato e il valore corrispondente. Per creare ad esempio una raccolta di impostazioni di configurazione di archiviazione che consentano per impostazione predefinita di archiviare le sessioni di messaggistica istantanea, utilizzare un comando simile al seguente:
    
        New-CsArchivingConfiguration -Identity "site:Redmond" -EnableArchiving "ImOnly"

## Specifica di più valori di proprietà durante la creazione di impostazioni di configurazione di archiviazione

  - È possibile modificare più valori di proprietà includendo più parametri. Con il comando seguente ad esempio vengono configurate nuove impostazioni per archiviare le sessioni di messaggistica istantanea e per bloccare la messaggistica istantanea del servizio di archiviazione, se non disponibile:
    
        New-CsArchivingConfiguration -Identity "site:Redmond" -EnableArchiving "ImOnly" -BlockOnArchiveFailure $True

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [New-CsArchivingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsArchivingConfiguration).

## Vedere anche

#### Concetti

[Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md)  

#### Ulteriori risorse

[Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)

