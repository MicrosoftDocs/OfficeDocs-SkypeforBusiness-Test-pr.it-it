---
title: 'Lync Server 2013: (Facoltativo) Abilitare e disabilitare gli annunci di partecipazione e abbandono delle conferenze'
TOCTitle: (Facoltativo) Abilitare e disabilitare gli annunci di partecipazione e abbandono delle conferenze
ms:assetid: c9529568-e66c-48d8-aef2-9072f9c336ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398834(v=OCS.15)
ms:contentKeyID: 49301972
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (Facoltativo) Abilitare e disabilitare gli annunci di partecipazione e abbandono delle conferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-30_

Quando gli utenti connessi tramite chiamata in ingresso partecipano a una conferenza o la abbandonano, l' applicazione Annuncio conferenza può annunciarne l'ingresso o l'uscita riproducendo un segnale o indicandone i nomi. Il funzionamento degli annunci può essere modificato eseguendo i cmdlet. Questo passaggio è facoltativo.

## Per modificare il comportamento di partecipazione a una conferenza o di abbandono della stessa

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins o come membro del ruolo **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il comando seguente al prompt:
    
        Get-CsDialinConferencingConfiguration
    
    Questo cmdlet consente di recuperare informazioni sull'invio o meno della richiesta ai partecipanti di registrare il loro nome per accedere a una conferenza e sul tipo di risposta fornito da Lync Server quando gli utenti partecipano a una conferenza telefonica con accesso esterno o la abbandonano.

4.  Eseguire il comando seguente al prompt:
    
        Set-CsDialinConferencingConfiguration -Identity <identity of dial-in conferencing settings to be modified>
        [-EnableNameRecording <$true | $false>]
        [-EntryExitAnnouncementsEnabledByDefault <$true | $false>]
        [-EntryExitAnnouncementsType <UseNames | ToneOnly]
    
    **EnableNameRecording**   Determina se richiedere o meno ai partecipanti anonimi di registrare il loro nome prima di accedere alla conferenza. Il valore predefinito è "$true" e indica che ai partecipanti anonimi viene richiesto di specificare il proprio nome durante l'accesso a una conferenza. I partecipanti autenticati non registrano il proprio nome perché viene utilizzato il nome visualizzato.
    
    **EntryExitAnnouncementsEnabledByDefault**   Indica se gli annunci sono attivati o disattivati per impostazione predefinita. Il valore predefinito è "$false" e indica che per impostazione predefinita non vengono visualizzati annunci quando gli utenti partecipano a una conferenza o la abbandonano. L'organizzatore della riunione può sostituire questa impostazione durante la pianificazione della riunione.
    
    **EntryExitAnnouncementsType**   Indica l'azione che viene intrapresa ogni volta che un utente partecipa o abbandona una conferenza per la quale sono abilitati gli annunci. Il valore predefinito è "UseNames" e indica la visualizzazione di un annuncio simile al seguente: "Davide Garghentini si è unito alla conferenza" quando gli annunci sono attivati.
    
    È possibile configurare queste impostazioni a livello globale o di sito. Le impostazioni configurate a livello di sito hanno la precedenza su quelle configurate a livello globale.
    
    Ad esempio:
    
        Set-CsDialinConferencingConfiguration -Identity site:Redmond
        -EnableNameRecording $false
        -EntryExitAnnouncementsEnabledByDefault $true
        -EntryExitAnnouncementsType ToneOnly
    
    In questo esempio le impostazioni vengono configurate al livello del sito di Redmond. Gli annunci sono attivati ma ai partecipanti non viene richiesto di specificare il proprio nome durante l'accesso a una conferenza. Quando i partecipanti accedono a una conferenza o la abbandonano viene riprodotto un segnale acustico.

