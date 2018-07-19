---
title: Creazione di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per specifici siti o utenti
TOCTitle: Creazione di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per specifici siti o utenti
ms:assetid: 5864793a-ba72-470c-bb5b-9fb41e968896
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398385(v=OCS.15)
ms:contentKeyID: 49300610
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per specifici siti o utenti

 

_**Ultima modifica dell'argomento:** 2013-02-23_

In Lync Server 2013 si usano criteri per abilitare e disabilitare l'archiviazione delle comunicazioni interne ed esterne per gli utenti ospitati in Lync Server 2013. I criteri di archiviazione sono:

  - Criteri globali, creati per impostazione predefinita al momento della distribuzione di Lync Server 2013.

  - Criteri facoltativi a livello di sito e di utente, che è possibile creare e usare per specificare la modalità di implementazione dell'archiviazione per siti o utenti specifici.

Inizialmente i criteri di archiviazione vengono configurati al momento della distribuzione della funzionalità di archiviazione, ma dopo la distribuzione è possibile modificare, aggiungere ed eliminare criteri. In Pannello di controllo di Lync Server 2013 è possibile gestire i criteri a livello globale, di sito e di utente mediante la pagina **Criteri di archiviazione** del gruppo **Archiviazione e monitoraggio**. Se si integra l'archiviazione Lync Server con l'archiviazione Exchange 2013, i criteri utente di Exchange hanno la priorità sui criteri di archiviazione di Lync Server 2013.

Per informazioni dettagliate sull'implementazione dei criteri, inclusa la gerarchia dei criteri, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Per controllare l'implementazione dell'archiviazione, è necessario specificare le opzioni desiderate nelle configurazioni di archiviazione, ad esempio l'archiviazione o meno dei messaggi istantanei o delle conferenze, l'uso della modalità critica e le opzioni di eliminazione. Per impostazione predefinita, nella configurazione di archiviazione globale e nelle configurazioni di archiviazione a livello di sito o di pool non sono abilitate opzioni. Prima di abilitare l'archiviazione per le comunicazioni interne o esterne nei criteri di archiviazione è necessario specificare tutte le opzioni appropriate nelle configurazioni di archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013</A> nella documentazione relativa alle operazioni.<BR>Se per la distribuzione viene abilitata l'integrazione di Microsoft Exchange, i criteri di archiviazione di Exchange determinano se l'archiviazione è abilitata per gli utenti ospitati in Exchange 2013 con cassette postali impostate per l'archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.



## Per creare criteri di archiviazione per un sito o per utenti

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Criteri di archiviazione**.

4.  Fare clic su **Nuovo** e quindi eseguire una delle operazioni seguenti:
    
      - Per creare criteri di archiviazione a livello di sito, fare clic su **Criteri sito** e quindi in **Seleziona un sito** fare clic sul sito a cui applicare i criteri.
    
      - Per creare criteri di archiviazione a livello di utente, fare clic su **Criteri utente**.

5.  In **Nuovi criteri di archiviazione** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nome per i nuovi criteri, ad esempio ContosoEsterni.
    
      - In **Descrizione** immettere informazioni dettagliate sugli scopi dei criteri, ad esempio "Criteri di archiviazione degli utenti esterni per Contoso".
    
      - Per controllare l'archiviazione delle comunicazioni con gli utenti interni, selezionare o deselezionare la casella di controllo **Archivia comunicazioni interne**.
    
      - Per controllare l'archiviazione delle comunicazioni con gli utenti esterni, selezionare o deselezionare la casella di controllo **Archivia comunicazioni esterne**.

6.  Fare clic su **Commit**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Le impostazioni dei criteri utente si applicano solo agli utenti e ai gruppi di utenti a cui si applicano i criteri. Per informazioni dettagliate, vedere <a href="lync-server-2013-applying-an-archiving-policy-to-users.md">Applicazione di criteri di archiviazione agli utenti</a></td>
    </tr>
    </tbody>
    </table>


## Creazione di criteri di archiviazione tramite i cmdlet di Lync Server Management Shell

I criteri di archiviazione possono inoltre essere creati tramite il cmdlet **Remove-CsArchivingPolicy** di Windows PowerShell. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Creazione di nuovi criteri di archiviazione a livello di ambito sito

  - Questo comando crea nuovi criteri di archiviazione per il sito Redmond:
    
        New-CsArchivingPolicy -Identity "site:Redmond"

## Creazione di nuovi criteri di archiviazione a livello di ambito per utente

  - Per creare nuovi criteri di archiviazione a livello di ambito per utente, è sufficiente specificare un parametro Identity univoco quando si creano i criteri:
    
        New-CsArchivingPolicy -Identity "RedmondArchivingPolicy"

## Creazione di nuovi criteri di archiviazione per l'archiviazione delle sessioni di comunicazione interne

  - Dal momento che nei comandi precedenti non sono stati specificati parametri, oltre al parametro Identity obbligatorio, i nuovi criteri useranno i valori predefiniti per ogni proprietà. Per creare criteri che usano valori di proprietà diversi, includere semplicemente il parametro e il valore di parametro appropriato. Ad esempio, per creare criteri di archiviazione che permettono l'archiviazione di sessioni di messaggistica istantanea interne, usare un comando come questo:
    
        New-CsArchivingPolicy -Identity "site:Redmond" -ArchiveInternal $True

## Creazione di nuovi criteri di archiviazione per l'archiviazione delle sessioni di comunicazione sia interne che esterne

  - Per modificare più valori di proprietà, è possibile includere più parametri nel comando. Ad esempio, questo comando configura i nuovi criteri per consentire l'archiviazione delle sessioni di messaggistica istantanea sia interne che esterne:
    
        New-CsArchivingPolicy -Identity "site:Redmond" -ArchiveInternal $True -ArchiveExternal $True

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [New-CsArchivingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsArchivingPolicy).

## Vedere anche

#### Ulteriori risorse

[Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)

