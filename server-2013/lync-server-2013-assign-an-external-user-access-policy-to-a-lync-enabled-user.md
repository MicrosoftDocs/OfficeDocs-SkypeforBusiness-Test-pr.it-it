---
title: 'Lync Server 2013: Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync'
TOCTitle: Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync
ms:assetid: 736fcaad-9f95-4896-b767-e199d86a00a4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398551(v=OCS.15)
ms:contentKeyID: 49300973
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

Se un utente è stato abilitato per Lync Server, è possibile configurare la federazione SIP, la federazione XMPP, l'accesso utente remoto e la connettività di messaggistica istantanea pubblica nel Pannello di controllo di Lync Server applicando i criteri appropriati a utenti specifici. Se, ad esempio, sono stati creati criteri per supportare l'accesso utente remoto, è necessario applicarli all'utente prima che possa connettersi a Lync Server da una postazione remota e collaborare con utenti interni dalla postazione remota.


> [!NOTE]
> Per supportare l'accesso utente esterno, è necessario abilitare il supporto per ogni tipo di accesso utente esterno desiderato e configurare i criteri appropriati e altre opzioni per il controllo. Per informazioni dettagliate, vedere <A href="lync-server-2013-configuring-support-for-external-user-access.md">Configurazione del supporto per l'accesso degli utenti esterni in Lync Server 2013</A> nella documentazione relativa alla distribuzione o <A href="lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md">Gestione della federazione e dell'accesso esterno a Lync Server 2013</A> nella documentazione relativa alle operazioni.



Utilizzare la procedura contenuta in questo argomento per applicare criteri di accesso utente esterno creati in precedenza a uno o più account utente.

## Per applicare criteri di accesso utente esterno a un account utente

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti** e quindi cercare l'account utente da configurare.

4.  Nella tabella in cui sono elencati i risultati della ricerca fare clic sull'account utente, su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Criteri di accesso esterno** in **Modifica utente di Lync Server** selezionare i criteri utente che si desidera applicare.
    

    > [!NOTE]
    > Le impostazioni <STRONG>&lt;automatiche&gt;</STRONG> applicano le impostazioni predefinite del server o dei criteri globali.



## Assegnazione dei criteri di accesso esterno per utente tramite i cmdlet di Windows PowerShell

I criteri di accesso esterno per utente possono essere assegnati tramite Windows PowerShell e il cmdlet Grant-CsExternalAccessPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per assegnare criteri di accesso esterno per utente a un singolo utente

  - Questo comando assegna il criterio di accesso esterno per utente RedmondExternalAccessPolicy all'utente Ken Myer.
    
        Grant-CsExternalAccessPolicy -Identity "Ken Myer" -PolicyName "RedmondExternalAccessPolicy"

## Per assegnare criteri di accesso esterno per utente a più utenti

  - Questo comando assegna il criterio di accesso esterno per utente USAExternalAccessPolicy a tutti gli utenti che dispongono di account nell'unità organizzativa UnitedStates in Active Directory. Per maggiori informazioni sul parametro OU (unità organizzativa) utilizzato in questo comando, vedere la documentazione relativa al cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser).
    
        Get-CsUser -OU "ou=UnitedStates,dc=litwareinc,dc=com" | Grant-CsExternalAccessPolicy -PolicyName "USAExternalAccessPolicy"

## Per annullare l'assegnazione di criteri di accesso esterno per utente

  - Questo comando annulla l'assegnazione di tutti i criteri di accesso esterno per utente precedentemente assegnati a Ken Myer. Dopo l'annullamento del criterio per utente, Ken Myer sarà gestito automaticamente dal criterio globale oppure dall'eventuale criterio del sito locale, che ha la precedenza sul criterio globale.
    
        Grant-CsExternalAccessPolicy -Identity "Ken Myer" -PolicyName $Null

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md).

