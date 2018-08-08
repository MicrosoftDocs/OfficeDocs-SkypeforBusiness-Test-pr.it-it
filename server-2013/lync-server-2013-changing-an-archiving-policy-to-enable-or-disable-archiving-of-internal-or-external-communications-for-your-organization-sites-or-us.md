---
title: "Lync Server 2013: Abil./disabil. archiv. comunic. int./est. di azienda, siti, utenti"
TOCTitle: "Lync Server 2013: Abil./disabil. archiv. comunic. int./est. di azienda, siti, utenti"
ms:assetid: b85dc3fb-8ebd-4e3c-ac90-fc79270ac867
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182576(v=OCS.15)
ms:contentKeyID: 49301769
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifica di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per l'organizzazione, siti o utenti

 

_**Ultima modifica dell'argomento:** 2013-02-23_

In Lync Server 2013 è possibile utilizzare i criteri per abilitare e disabilitare l'archiviazione per le comunicazioni interne ed esterne per gli utenti che si trovano in Lync Server 2013. Sono inclusi i criteri di archiviazione seguenti:

  - Un criterio globale che viene creato per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Criteri a livello di sito e di utente facoltativi che è possibile creare e utilizzare per specificare la modalità di implementazione dell'archiviazione per siti o utenti specifici.

È inizialmente necessario impostare i criteri di archiviazione quando si distribuisce l'archiviazione, ma è possibile modificare, aggiungere ed eliminare criteri dopo la distribuzione. Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare la pagina **Criteri di archiviazione** del gruppo **Archiviazione e monitoraggio** per gestire i criteri a livello globale, di sito e di utente. Se si integra l'archivio di Lync Server con l'archivio di Exchange 2013, i criteri utente di Exchange avranno la precedenza sui criteri di archiviazione di Lync Server 2013.

Per informazioni dettagliate sull'implementazione dei criteri, inclusa la gerarchia dei criteri, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Se è stata abilitata l'integrazione di Microsoft Exchange per la distribuzione in uso, i criteri di Exchange controllano se l'archiviazione è abilitata per gli utenti disponibili in Exchange 2013 le cui cassette postali sono in archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.<BR>Specificare tutte le opzioni appropriate nelle configurazioni di archiviazione prima di abilitare l'archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Per modificare i criteri di archiviazione

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Criteri di archiviazione**.

4.  Nell'elenco dei criteri eseguire una delle operazioni seguenti:
    
      - Per modificare i criteri per l'intera distribuzione, fare clic su **Globale** nell'elenco dei criteri, fare clic su **Modifica** e quindi su **Mostra dettagli**.
    
      - Per modificare i criteri per un singolo sito, fare clic sul nome del sito nell'elenco dei criteri, fare clic su **Modifica** e quindi su **Mostra dettagli**.
    
      - Per modificare i criteri per un singolo utente o gruppo di utenti, fare clic sul nome dell'utente o del gruppo di utenti nell'elenco dei criteri, fare clic su **Modifica** e quindi su **Mostra dettagli**.

5.  Nella pagina **Modifica Criteri di archiviazione** eseguire le operazioni seguenti:
    
      - Per abilitare o disabilitare l'archiviazione interna per i criteri, selezionare o deselezionare la casella di controllo **Archivia comunicazioni interne**.
    
      - Per abilitare o disabilitare l'archiviazione esterna per i criteri, selezionare o deselezionare la casella di controllo **Archivia comunicazioni esterne**.

6.  Fare clic su **Commit**.
    
    > [!IMPORTANT]  
    > Le impostazioni dei criteri utente sono valide solo per gli utenti e i gruppi di utenti specifici a cui vengono applicati i criteri. Per informazioni dettagliate, vedere <a href="lync-server-2013-applying-an-archiving-policy-to-users.md">Applicazione di criteri di archiviazione agli utenti</a>

## Abilitazione e disabilitazione dell'archiviazione mediante i cmdlet di Lync Server PowerShell

L'archiviazione può essere abilitata e disabilitata, per le sessioni di comunicazione interne ed esterne, anche mediante il cmdlet **Set-CsArchivingPolicy**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Abilitazione dell'archiviazione delle sessioni di comunicazione interne

  - Per abilitare l'archiviazione delle sessioni di comunicazione interne, impostare il valore della proprietà **ArchiveInternal** su True ($True). Ad esempio:
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $True

## Abilitazione dell'archiviazione delle sessioni di comunicazione esterne

  - Per abilitare l'archiviazione delle sessioni di comunicazione esterne, impostare il valore della proprietà **ArchiveExternal** su True ($True). Ad esempio:
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveExternal $True

## Abilitazione dell'archiviazione delle sessioni di comunicazione sia interne che esterne

  - Per abilitare l'archiviazione delle sessioni di comunicazione sia interne che esterne, impostare le proprietà **ArchiveInternal** e **ArchiveExternal** su True:
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $True -ArchiveExternal $True

## Disabilitazione dell'archiviazione

  - Per disabilitare completamente l'archiviazione, impostare le proprietà **ArchiveInternal** e **ArchiveExternal** su False ($False). Ad esempio:
    
        Set-CsArchivingPolicy -Identity "global" -ArchiveInternal $False -ArchiveExternal $False

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsArchivingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsArchivingPolicy).

## Vedere anche

#### Ulteriori risorse

[Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

