---
title: Gestione delle impostazioni di configurazione del servizio di registrazione centralizzato tramite PowerShell
TOCTitle: Gestione delle impostazioni di configurazione del servizio di registrazione centralizzato tramite PowerShell
ms:assetid: f455c3aa-0061-413d-bdfb-a3e78f82723d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721938(v=OCS.15)
ms:contentKeyID: 49887826
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione delle impostazioni di configurazione del servizio di registrazione centralizzato tramite PowerShell

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Il servizio di registrazione centralizzato è controllato e configurato da impostazioni e parametri creati e utilizzati dal controller servizio di registrazione centralizzato (CLSController) per inviare comandi all'agente servizio di registrazione centralizzato (CLSAgent) del singolo computer. L'agente elabora i comandi che riceve e, in caso di un comando Start, utilizza la configurazione di scenari, provider, dimensione del log, durata della traccia e flag per iniziare a raccogliere i log di traccia in base alle informazioni di configurazione fornite.

> [!IMPORATNT]
> <td>Non tutti i cmdlet di Windows PowerShell elencati per il servizio di registrazione centralizzato sono concepiti per essere utilizzati con le distribuzioni locali di Lync Server 2013. Sebbene possa sembrare che funzionino, i cmdlet seguenti non sono progettati per funzionare con le distribuzioni locali di Lync Server 2013:
> <ul>
> <li><p><strong>Cmdlet CsClsRegion:</strong> <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsRegion">Get-CsClsRegion</a>, <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsRegion">Set-CsClsRegion</a>, <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsRegion">New-CsClsRegion</a> e <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsClsRegion">Remove-CsClsRegion</a>.</p></li>
> <li><p><strong>Cmdlet CsClsSearchTerm:</strong> <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsSearchTerm">Get-CsClsSearchTerm</a> e <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsSearchTerm">Set-CsClsSearchTerm</a>.</p></li>
> <li><p><strong>Cmdlet CsClsSecurityGroup:</strong> <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsSecurityGroup">Get-CsClsSecurityGroup</a>, <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsSecurityGroup">Set-CsClsSecurityGroup</a>, <a href="https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsSecurityGroup">New-CsClsSecurityGroup</a> e <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsClsSecurityGroup">Remove-CsClsSecurityGroup</a>.</p></li></ul>
> Le impostazioni definite nei cmdlet non avranno effetti negativi e non causeranno problemi, ma i cmdlet sono progettati per l'utilizzo con Microsoft Office 365 e non genereranno i risultati previsti nelle distribuzioni locali. Questo non significa che non si possono utilizzare nelle distribuzioni locali, ma il loro utilizzo è descritto in un argomento più avanzato che non è incluso in questa documentazione.


## Argomenti della sezione

Negli argomenti di questa sezione sono definiti le opzioni di configurazione, i parametri e le impostazioni per il servizio di registrazione centralizzato. Negli argomenti seguenti è possibile trovare informazioni su come configurare il servizio di registrazione centralizzato, come recuperare le impostazioni di configurazione, la creazione degli scenari e la gestione dei gruppi di sicurezza per servizio di registrazione centralizzato, su come eseguire ricerca e altro ancora.

  - [Gestione della configurazione di computer, siti e servizio di registrazione centralizzato globale](lync-server-2013-managing-computer-site-and-global-centralized-logging-service-configuration.md)

  - [Configurazione dei provider per il servizio di registrazione centralizzato](lync-server-2013-configuring-providers-for-centralized-logging-service.md)

  - [Configurazione degli scenari per il servizio di registrazione centralizzato](lync-server-2013-configuring-scenarios-for-the-centralized-logging-service.md)

## Vedere anche

#### Concetti

[Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md)  
[Cmdlet di registrazione centralizzata](https://docs.microsoft.com/en-us/powershell/module/skype/)

