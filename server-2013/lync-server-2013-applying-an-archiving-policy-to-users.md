---
title: Applicazione di criteri di archiviazione agli utenti
TOCTitle: Applicazione di criteri di archiviazione agli utenti
ms:assetid: 624a7d3e-389d-403a-97e5-f7bb17023ef3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521004(v=OCS.15)
ms:contentKeyID: 49300764
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applicazione di criteri di archiviazione agli utenti

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Se un utente è stato abilitato per Lync Server 2013 e sono stati creati uno o più criteri utente per l'archiviazione per gli utenti ospitati in Lync Server 2013, è possibile implementare il supporto dell'archiviazione per utenti specifici applicando i criteri appropriati a tali utenti o gruppi di utenti. Se ad esempio si crea un criterio per supportare l'archiviazione delle comunicazioni interne, sarà possibile applicarlo ad almeno un utente o un gruppo di utenti per supportare l'archiviazione delle comunicazioni dell'utente relative a Lync Server 2013.


> [!NOTE]
> Se per la distribuzione viene abilitata l'integrazione di Microsoft Exchange, i criteri di archiviazione sul posto di Exchange determinano se l'archiviazione è abilitata per gli utenti ospitati in Exchange 2013 con cassette postali impostate per l'archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.<BR>Prima di abilitare l'archiviazione, è necessario specificare tutte le opzioni appropriate nelle configurazioni di archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013</A> nella documentazione relativa alle operazioni.



Utilizzare la procedura in questo argomento per applicare criteri di archiviazione a livello utente creati in precedenza a uno o più account utente o gruppo di utenti.

## Per applicare criteri di archiviazione a livello di utente a un account utente

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti** e quindi cercare l'account utente che si desidera configurare.

4.  Nella tabella dei risultati di ricerca fare clic sull'account utente, fare clic su **Modifica** e quindi fare clic su **Mostra dettagli**.

5.  In **Modifica utente di Lync Server**, in **Criteri di archiviazione**, selezionare i criteri di archiviazione che si desidera applicare.
    

    > [!NOTE]
    > Le impostazioni <STRONG>&lt;Automatico&gt;</STRONG> si applicano alle impostazioni di installazione predefinite del server e vengono applicate automaticamente dal server.



6.  Fare clic su **Commit**.

## Assegnazione di criteri di archiviazione per utente tramite i cmdlet di Lync Server Management Shell

I criteri di archiviazione per utente possono inoltre essere assegnati utilizzando Lync ServerWindows PowerShell e il cmdlet **Grant-CsArchivingPolicy**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Assegnazione di criteri di archiviazione per utente a un singolo utente

  - Il comando seguente consente di assegnare i criteri di archiviazione per utente denominati RedmondArchivingPolicy all'utente Ken Myer.
    
        Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName "RedmondArchivingPolicy"

## Assegnazione di criteri di archiviazione per utente a più utenti

  - Questo comando consente di assegnare i criteri di archiviazione per utente denominati RedmondArchivingPolicy a tutti gli utenti con account ospitati nel pool di registrazione atl-cs-001.litwareinc.com. Per informazioni dettagliate sul parametro Filter utilizzato in questo comando, vedere la documentazione relativa al cmdlet [Get-CsUser](get-csuser.md).
    
        Get-CsUser -Filter {RegistrarPool -eq "atl-cs-001.litwareinc.com"} | Grant-CsArchivingPolicy -PolicyName "RedmondArchivingPolicy"

## Annullamento dell'assegnazione di criteri di archiviazione per utente

  - Il comando seguente consente di annullare l'assegnazione dei criteri di archiviazione per utente precedentemente assegnati all'utente Ken Myer. Dopo l'annullamento dell'assegnazione dei criteri per utente, Ken Myer verrà gestito automaticamente tramite i criteri globali oppure i criteri di sito locale, se esistenti. I criteri di sito sono prioritari rispetto ai criteri globali.
    
        Grant-CsArchivingPolicy -Identity "Ken Myer" -PolicyName $Null

Per informazioni dettagliate, vedere la documentazione relativa al cmdlet [Grant-CsArchivingPolicy](grant-csarchivingpolicy.md).

## Vedere anche

#### Ulteriori risorse

[Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md)  
[Assegnazione di criteri per utente in Lync Server 2013](lync-server-2013-assigning-per-user-policies.md)

