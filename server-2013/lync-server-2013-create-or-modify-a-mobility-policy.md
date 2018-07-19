---
title: Creare o modificare criteri dispositivi mobili
TOCTitle: Creare o modificare criteri dispositivi mobili
ms:assetid: fc2dfea0-2215-440d-9f4b-7c985da29211
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721946(v=OCS.15)
ms:contentKeyID: 49887839
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare criteri dispositivi mobili

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile creare o modificare criteri dispositivi mobili per consentire agli utenti di dispositivi mobili di utilizzare i dispositivi mobili supportati per le funzionalità di Lync, quali la messaggistica istantanea, la presenza e i contatti. È possibile creare o modificare i criteri dispositivi mobili dal Pannello di controllo di Lync Server 2013 o da Lync Server 2013 Management Shell

## Per creare un criterio dispositivi mobili dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Criteri dispositivi mobili**.

4.  Nella pagina **Criteri dispositivi mobili** fare clic su **Nuovo** e quindi eseguire una delle operazioni seguenti:
    
    1.  Per creare criteri dispositivi mobili per un sito, fare clic su **Criteri sito**, selezionare un sito, fare clic su **OK**, controllare le impostazioni predefinite e, se necessario, apportare eventuali modifiche.
    
    2.  Per creare criteri dispositivi mobili per un utente, fare clic su **Criteri utente**, digitare un nome, controllare le impostazioni predefinite e, se necessario, apportare eventuali modifiche.

5.  Fare clic su **Commit**.

## Per modificare criteri dispositivi mobili dal Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Criteri dispositivi mobili**.

4.  Nella pagina **Criteri dispositivi mobili** fare clic su uno dei criteri dispositivi mobili esistenti.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  Modificare le impostazioni.

7.  Fare clic su **Commit**.

## Rimozione dei criteri di accesso esterno utilizzando i cmdlet Windows PowerShell

In ambito sito o utente è possibile creare i criteri dispositivi mobili anche utilizzando Windows PowerShell e il cmdlet **New-CsMobilityPolicy**. È inoltre possibile utilizzare il cmdlet **Set-CsMobilityPolicy** per modificare i criteri esistenti, inclusi i criteri globali. È possibile eseguire i cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Creazione di criteri dispositivi mobili in ambito sito

  - Questo comando crea un nuovo criterio dispositivi mobili per il sito Redmond:
    
        New-CsMobilityPolicy -Identity "site:Redmond"
    
    Poiché non sono stati specificati parametri nel comando precedente (oltre al parametro obbligatorio Identity), i criteri utilizzeranno tutti i valori predefiniti per tutte le proprietà.

## Creazione di criteri dispositivi mobili in ambito utente

  - Per creare un criterio dispositivi mobili in ambito utente, specificare un'identità univoca per il criterio:
    
        New-CsMobilityPolicy -Identity "RedmondMobilityPolicy"

## Modifica di un valore di proprietà durante la creazione di criteri dispositivi mobili

  - Per creare criteri che utilizzano valori di proprietà diversi, includere il parametro e il valore del parametro appropriati. Ad esempio, questo comando crea un criterio dispositivi mobili che disabilita la chiamata da ufficio:
    
        New-CsMobilityPolicy -Identity "site:Redmond" -EnableOutsideVoice $False

## Modifica di più valori di proprietà durante la creazione di criteri dispositivi mobili

  - È possibile modificare più valori di proprietà includendo più parametri. Ad esempio, questo comando crea un criterio che disabilita sia la mobilità che la chiamata da ufficio:
    
        New-CsMobilityPolicy "site:Redmond" -EnableMobility $False -EnableOutsideVoice $False

Per informazioni dettagliate, vedere l'argomento della Guida per i cmdlet [New-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsMobilityPolicy) e [Set-CsMobilityPolicy](set-csmobilitypolicy.md).

## Vedere anche

#### Attività

[Configurazione dei criteri per dispositivi mobili in Lync Server 2013](lync-server-2013-configuring-mobility-policy.md)

