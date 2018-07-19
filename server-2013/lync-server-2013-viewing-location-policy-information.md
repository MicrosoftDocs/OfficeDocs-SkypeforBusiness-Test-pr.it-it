---
title: Visualizzazione delle informazioni sui criteri percorso
TOCTitle: Visualizzazione delle informazioni sui criteri percorso
ms:assetid: 14e41bcb-ea0a-49c2-99b3-1f61fc34416d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520954(v=OCS.15)
ms:contentKeyID: 49299773
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sui criteri percorso

 

_**Ultima modifica dell'argomento:** 2012-11-01_

In Lync Server 2013 i criteri percorso consentono di applicare impostazioni relative alla funzionalità Enhanced 9-1-1 (E9-1-1) e impostazioni relative alla posizione per utenti o contatti. Tali criteri consentono di determinare se un utente è abilitato per E9-1-1 e, in caso affermativo, il comportamento specifico di una chiamata di emergenza. È ad esempio possibile utilizzare i criteri percorso per definire i numeri che rappresentano una chiamata di emergenza (911 negli Stati Uniti), per specificare se inviare o meno una notifica all'ufficio di sicurezza aziendale e per impostare la modalità di instradamento della chiamata.

È possibile configurare i criteri percorso dal gruppo **Configurazione di rete** del Pannello di controllo di Lync Server 2013. Dal Pannello di controllo di Lync Server è possibile visualizzare, creare o eliminare i criteri percorso. Utilizzare la seguente procedura per visualizzare informazioni sui criteri percorso. Per informazioni dettagliate sulla creazione o la modifica di criteri percorso, vedere [Creazione o modifica di criteri percorso](lync-server-2013-creating-or-modifying-a-location-policy.md).

## Per visualizzare informazioni sui criteri percorso

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri percorso**.

4.  Nella pagina **Criteri percorso** selezionare il criterio percorso che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.
    

    > [!NOTE]
    > È possibile visualizzare le informazioni su un solo criterio percorso alla volta.



Per impostazione predefinita, esiste un solo criterio, denominato Globale, e non può essere eliminato o rinominato. È tuttavia possibile modificarlo. Tale criterio verrà applicato a tutti gli utenti e i contatti, a meno che non vengano creati criteri sito o criteri utente. I criteri utente devono essere applicati a utenti specifici.

## Vedere anche

#### Attività

[Creazione o modifica di criteri percorso](lync-server-2013-creating-or-modifying-a-location-policy.md)  
[Creare criteri percorso in Lync Server 2013](lync-server-2013-create-location-policies.md)  
[Creare o modificare un sito di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-site.md)  

#### Ulteriori risorse

[New-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsLocationPolicy)  
[Set-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsLocationPolicy)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)

