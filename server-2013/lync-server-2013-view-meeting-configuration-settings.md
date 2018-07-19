---
title: Visualizzare le impostazioni di configurazione delle riunioni
TOCTitle: Visualizzare le impostazioni di configurazione delle riunioni
ms:assetid: d03a4684-9d8b-4728-917d-5b5c91511e2c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721894(v=OCS.15)
ms:contentKeyID: 49887769
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le impostazioni di configurazione delle riunioni

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Nel Pannello di controllo di Lync Server 2013 utilizzare l'impostazione di configurazione di riunione per definire la modalità di implementazione delle riunioni nella distribuzione. Sono incluse le configurazioni di riunione seguenti:

  - Una configurazione globale creata per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Configurazioni facoltative a livello di sito e di utente che possono essere create e utilizzate per specificare come devono essere implementate le riunioni per siti o utenti specifici.

## Per visualizzare le impostazioni di configurazione di riunione

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Configurazione riunione**.

4.  Nella pagina **Configurazione riunione** fare clic sulla configurazione di riunione che si desidera visualizzare.

5.  In **Modifica filtro file** selezionare la casella di controllo **Mostra dettagli…**
    
    Verrà visualizzato **Modifica configurazione riunione - \<criteri\>** con le impostazioni dei criteri selezionati. Per informazioni dettagliate sulla configurazione delle impostazioni, vedere [Creare o modificare una raccolta di impostazioni di configurazione delle riunioni](lync-server-2013-create-or-modify-a-collection-of-meeting-configuration-settings.md).

## Visualizzazione delle informazioni sulla configurazione di riunione mediante i cmdlet di Lync Server PowerShell

Le impostazioni di configurazione di riunione possono essere visualizzate anche utilizzando Lync Server PowerShell e il cmdlet Get-CsMeetingConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione delle informazioni sulla configurazione di riunione

  - Per visualizzare informazioni su tutte le impostazioni di configurazione di riunione, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsMeetingConfiguration
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity                        : Global
        PstnCallersBypassLobby          : True
        EnableAssignedConferenceType    : True
        DesignateAsPresenter            : Company
        AssignedConferenceTypeByDefault : True
        AdmitAnonymousUsersByDefault    : True
        RequireRoomSystemsAuthorization : False
        LogoURL                         :
        LegalURL                        :
        HelpURL                         :
        CustomFooterText                :
        AllowConferenceRecording        : True

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsMeetingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingConfiguration).

