---
title: Visualizzare le informazioni sui criteri conferenza
TOCTitle: Visualizzare le informazioni sui criteri conferenza
ms:assetid: e99fdc4d-926a-4e36-ac99-ab5035568847
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721918(v=OCS.15)
ms:contentKeyID: 49887802
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzare le informazioni sui criteri conferenza

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Nel Pannello di controllo di Lync Server 2013 si utilizzano i criteri conferenza per stabilire le modalità di implementazione delle funzionalità di conferenza nella distribuzione. Sono inclusi i criteri conferenza seguenti:

  - Criteri globali creati per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Criteri facoltativi a livello di sito e di utente, che è possibile creare e utilizzare per specificare come implementare le funzionalità di conferenza per siti o utenti specifici.

## Per visualizzare le impostazioni dei criteri conferenza

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Criteri conferenza**.

4.  Nella pagina **Criteri conferenza** fare doppio clic sui criteri conferenza che si desidera visualizzare.

5.  In **Modifica filtro file** selezionare la casella di controllo **Mostra dettagli**.
    
    Viene visualizzata la scheda **Modifica criteri conferenza- \<criteri\>** in cui sono visualizzate le impostazioni per i criteri selezionati. Per informazioni dettagliate sulla configurazione delle impostazioni, vedere [Creare o modificare criteri conferenza](lync-server-2013-create-or-modify-a-conferencing-policy.md).

## Visualizzazione dei criteri conferenza tramite i cmdlet PowerShell per Lync Server

Per visualizzare i criteri conferenza, è inoltre possibile utilizzare PowerShell per Lync Server e il cmdlet Get-CsConferencingPolicy. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione dei criteri conferenza

  - Per visualizzare informazioni su tutti i criteri conferenza, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsConferencingPolicy
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity                                  : Global
        AllowIPAudio                              : True
        AllowIPVideo                              : True
        AllowMultiView                            : True
        Description                               :
        AllowParticipantControl                   : True
        AllowAnnotations                          : True
        DisablePowerPointAnnotations              : False
        AllowUserToScheduleMeetingsWithAppSharing : True
        AllowNonEnterpriseVoiceUsersToDialOut     : False
        AllowAnonymousUsersToDialOut              : False
        AllowAnonymousParticipantsInMeetings      : True
        AllowExternalUsersToSaveContent           : True
        AllowExternalUserControl                  : False
        AllowExternalUsersToRecordMeeting         : False
        AllowPolls                                : True
        AllowSharedNotes                          : True
        EnableDialInConferencing                  : True
        EnableAppDesktopSharing                   : Desktop
        AllowConferenceRecording                  : False
        EnableP2PRecording                        : False
        EnableFileTransfer                        : True
        EnableP2PFileTransfer                     : True
        EnableP2PVideo                            : True
        AllowLargeMeetings                        : False
        EnableDataCollaboration                   : True
        MaxVideoConferenceResolution              : VGA
        MaxMeetingSize                            : 250
        AudioBitRateKb                            : 200
        VideoBitRateKb                            : 50000
        AppSharingBitRateKb                       : 50000
        FileTransferBitRateKb                     : 50000
        TotalReceiveVideoBitRateKb                : 6000
        EnableMultiViewJoin                       : True

Per ulteriori informazioni, vedere l'argomento della Guida per il cmdlet [Get-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsConferencingPolicy).

