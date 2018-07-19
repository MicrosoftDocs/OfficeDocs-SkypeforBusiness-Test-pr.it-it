---
title: "Lync Server 2013: Configurare criteri per controllare l'accesso utente federato"
TOCTitle: Configurare criteri per controllare l'accesso utente federato
ms:assetid: 5485e208-81e4-4e59-9aeb-1232c11dd8a2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398359(v=OCS.15)
ms:contentKeyID: 49300604
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare criteri per controllare l'accesso utente federato in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Quando si configurano criteri per supportare le comunicazioni con partner federati, i criteri si applicano agli utenti dei domini federati. È possibile configurare uno o più criteri di accesso utente esterno per controllare se gli utenti dei domini federati possono o meno collaborare con utenti interni di Lync Server 2013. Per controllare l'accesso utente federato, è possibile configurare criteri a livello globale, di sito e di utente. Le impostazioni criteri di Lync Server applicate a un determinato livello di criteri possono sostituire le impostazioni applicate a un altro livello di criteri. La precedenza dei criteri di Lync Server è la seguente: i criteri utente (maggiore influenza) sostituiscono i criteri sito e i criteri sito sostituiscono i criteri globali (minore influenza). Ciò significa che maggiore è la prossimità dell'impostazione criteri all'oggetto su cui influiscono i criteri, maggiore è l'influenza su tale oggetto.


> [!NOTE]
> È possibile configurare criteri per il controllo dell'accesso degli utenti federati anche se non è stata abilitata la federazione per l'organizzazione. I criteri configurati, tuttavia, verranno applicati solo dopo aver abilitato la federazione per l'organizzazione. Per informazioni dettagliate sull'abilitazione della federazione, vedere <A href="lync-server-2013-enable-or-disable-remote-user-access.md">Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013</A> nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni. Se inoltre si specificano criteri utente per il controllo dell'accesso degli utenti federati, i criteri verranno applicati solo agli utenti abilitati per Lync Server 2013 e configurati per l'utilizzo dei criteri.



## Per configurare criteri per supportare l'accesso da parte di utenti di domini federati

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e quindi su **Criteri di accesso esterno** .

4.  Nella pagina **Criteri di accesso esterno** eseguire una delle operazioni seguenti:
    
      - Per configurare i criteri globali per il supporto dell'accesso degli utenti federati, fare clic sui criteri globali, su **Modifica** e quindi su **Mostra dettagli** .
    
      - Per creare nuovi criteri di sito, fare clic su **Nuovo** e quindi su **Criteri sito** . In **Seleziona un sito** fare clic sul sito appropriato nell'elenco e quindi fare clic su **OK** .
    
      - Per creare nuovi criteri utente, fare clic su **Nuovo** e quindi su **Criteri utente** . In **Nuovi criteri di accesso esterno** creare un nome univoco nel campo **Nome** che indichi lo scopo dei criteri, ad esempio **AbilitaUtentiFederati** per criteri utente che abilitano le comunicazioni per gli utenti di domini federati.
    
      - Per modificare criteri esistenti, fare clic sui criteri appropriati indicati nella tabella, fare clic su **Modifica** e quindi fare clic su **Mostra dettagli** .

5.  (Facoltativo) Se si desidera aggiungere o modificare una descrizione, specificare le informazioni per i criteri in **Descrizione** .

6.  Eseguire una delle operazioni seguenti:
    
      - Per abilitare l'accesso degli utenti federati per i criteri, selezionare la casella di controllo **Abilita comunicazioni con utenti federati** .
    
      - Per disabilitare l'accesso degli utenti federati per i criteri, deselezionare la casella di controllo **Abilita comunicazioni con utenti federati** .

7.  Fare clic su **Commit** .

Per consentire l'accesso degli utenti federati, è inoltre necessario abilitare il supporto per la federazione nell'organizzazione. Per informazioni dettagliate, vedere [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md).

Se si tratta di criteri utente è inoltre necessario applicarli agli utenti ai quali si desidera consentire di collaborare con utenti federati. Per informazioni dettagliate, vedere [Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md).

## Per configurare criteri esistenti mediante Windows PowerShell per supportare l'accesso da parte di utenti di domini federati

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  In Lync Server Management Shell digitare:
    
        Set-CsExternalAccessPolicy -Identity <name of global, site or user policy - policy must exist when using Set-CsExternalAccessPolicy > -Description <descriptive name for policy> -EnableFederationAccess <$true, $false> -EnableXmppAccess <$true, $false> -EnablePublicCloudAcess <$true, $false> -EnablePublicCloudAudioVideoAcess <$true, $false> -EnableOutsideAcess <$true, $false>
    
    Ecco un comando di esempio che abilita i criteri globali per l'accesso utente federato, l'accesso al dominio XMPP, l'accesso utente remoto e l'accesso provider pubblico, e consente l'uso di audio e video ai provider pubblici che li supportano:
    
        Set-CsExternalAccessPolicy -Identity global -EnableFederationAccess $true -EnableXmppAccess $true -EnableOutsideAccess $true -EnablePublicCloudAccess $true -EnablePublicCloudAudioVideoAccess $true
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Per il parametro “EnablePublicCloudAudioVideoAccess” non esiste un'opzione corrispondente nel Pannello di controllo di Lync Server</td>
    </tr>
    </tbody>
    </table>


## Per creare nuovi criteri mediante Windows PowerShell e supportare l'accesso da parte di utenti di domini federati

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  In Lync Server Management Shell digitare:
    
        New-CsExtenalAccessPolicy -Identity <name of site or user policy - you cannot create a new global policy using New-CsExternalAccessPolicy > -Description <descriptive name for policy> -EnableFederationAccess <$true, $false> -EnableXmppAccess <$true, $false> -EnablePublicCloudAccess <$true, $false> -EnablePublicCloudAudioVideoAccess <$true, $false> -EnableOutsideAccess <$true, $false>
    
    Ecco un esempio di creazione di nuovi criteri sito:
    
        New-CsExternalAccessPolicy -Identity site:Redmond -EnableFederationAccess $true -EnableXmppAccess $true -EnableOutsideAccess $true -EnablePublicCloudAccess $true -EnablePublicCloudAudioVideoAccess $true

## Per eliminare o reimpostare criteri mediante Windows PowerShell per supportare l'accesso da parte di utenti di domini federati

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  In Lync Server Management Shell digitare:
    
        Remove-CsExternalAccessPolicy -Identity <name of global, site or user policy> 
    
    Ecco un esempio di reimpostazione dei criteri globali. È possibile rimuovere impostazioni dai criteri globali, ma non è possibile eliminarli:
    
        Remove-CsExternalAccessPolicy -Identity global 
    
    Per rimuovere criteri sito, digitare:
    
        Remove-CsExternalAccessPolicy -Identity site:Redmond 
    
    Elimina i criteri sito Redmond. Per eliminare criteri utenti denominati UserEAPPolicy, digitare:
    
        Remove-CsExternalAccessPolicy -Identity UserEAPPolicy

## Vedere anche

#### Attività

[Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)  
[Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md)  

#### Ulteriori risorse

[Gestire i domini federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)  
[Gestire i provider federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)  
[Set-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsExternalAccessPolicy)  
[New-CsExternalAccessPolicy](new-csexternalaccesspolicy.md)  
[Get-CsExternalAccessPolicy](get-csexternalaccesspolicy.md)  
[Remove-CsExternalAccessPolicy](remove-csexternalaccesspolicy.md)  
[Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)

