---
title: 'Lync Server 2013: Configurazione dei criteri per dispositivi mobili'
TOCTitle: Configurazione dei criteri per dispositivi mobili
ms:assetid: 595536e0-9bb3-49a3-8d13-1a77351ebc62
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690018(v=OCS.15)
ms:contentKeyID: 49300666
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei criteri per dispositivi mobili in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-13_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Lync Server 2013 offre criteri per dispositivi mobili che consentono di stabilire chi può utilizzare le funzionalità per i dispositivi mobili e chi può utilizzare le funzionalità Chiamata tramite ufficio, VoIP (Voice over IP) o video e se sarà necessaria una connessione Wi-Fi per le funzionalità VoIP o video. La funzionalità Chiamata tramite ufficio consente a un utente mobile di effettuare e ricevere chiamate su un cellulare tramite un numero di telefono dell'ufficio anziché il numero del cellulare. In questo modo, la parte chiamata non vede il numero di cellulare del chiamante e un utente può evitare i costi per chiamate in uscita. La configurazione delle funzionalità VoIP e video consente agli utenti di ricevere ed effettuare chiamate VoIP e chiamate video. Le impostazioni per l'utilizzo della rete Wi-Fi stabiliscono se il dispositivo di un utente dovrà utilizzare una rete Wi-Fi anziché una rete dati cellulare.

Per impostazione predefinita sono abilitate le funzionalità per dispositivi mobili, Chiamata tramite ufficio, VoIP e video. Le impostazioni per richiedere una rete Wi-Fi per le funzionalità VoIP e video sono disabilitate. Gli amministratori possono stabilire chi ha accesso a tali funzionalità eseguendo un cmdlet. È possibile disattivare le opzioni globalmente, a livello di sito o a livello di singoli utenti.

Per poter utilizzare le funzionalità di mobilità e Chiama da ufficio, gli utenti devono soddisfare i prerequisiti seguenti:

  - Gli utenti devono essere abilitati per Lync Server 2013.

  - Gli utenti devono essere abilitati per VoIP aziendale.

  - Agli utenti devono essere assegnati criteri di mobilità con l'opzione **EnableMobility** impostata su True.

Affinché gli utenti siano in grado di utilizzare Chiama da ufficio, è necessario che soddisfino i due prerequisiti aggiuntivi seguenti:

  - Agli utenti devono essere assegnati criteri vocali con l'opzione **Abilita squillo simultaneo dei telefoni** selezionata.

  - Agli utenti devono essere assegnati criteri di mobilità con l'opzione **EnableOutsideVoice** impostata su True.


> [!NOTE]
> Gli utenti non abilitati per VoIP aziendale possono utilizzare i dispositivi mobili per effettuare chiamate VoIP da Lync a Lync o partecipare a conferenze tramite il collegamento Fare clic per partecipare nei dispositivi, se a tali utenti vengono assegnate le opzioni appropriate per i criteri vocali. Per informazioni dettagliate, vedere <A href="lync-server-2013-defining-your-mobility-requirements.md">Definizione dei requisiti per dispositivi mobili per Lync Server 2013</A>.



Per informazioni dettagliate sull'abilitazione degli utenti per Lync Server 2013, vedere [Disabilitare o abilitare nuovamente gli account utente per Lync Server](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md). Per informazioni dettagliate sull'abilitazione degli utenti per VoIP aziendale, vedere [Abilitare gli utenti per VoIP aziendale in Lync Server 2013](lync-server-2013-enable-users-for-enterprise-voice.md). Per informazioni dettagliate sull'impostazione delle opzioni per i criteri vocali, vedere [Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md).

## Per modificare i criteri di mobilità globali

1.  Accedere a qualsiasi computer in cui Lync Server Management Shell e Ocscore sono installati come membro del ruolo CsAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Disattivare globalmente l'accesso alle funzionalità di mobilità e Chiama da ufficio. Nella riga di comando digitare:
    
        Set-CsMobilityPolicy -EnableMobility $False -EnableOutsideVoice $False
    

    > [!NOTE]
    > È possibile disattivare Chiama da ufficio senza disattivare l'accesso alla funzionalità di mobilità. Non è tuttavia possibile disattivare le funzionalità di mobilità senza disattivare anche Chiama da ufficio.



## Per modificare i criteri di mobilità a livello di sito

1.  Accedere a qualsiasi computer in cui Lync Server Management Shell e Ocscore sono installati come membro del ruolo CsAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Creare criteri a livello di sito e disattivare le funzionalità VoIP e video, quindi richiedere la connessione Wi-Fi per l'audio IP e il video IP per un sito. Nella riga di comando digitare:
    
        New-CsMobilityPolicy -Identity site:<site identifier> -EnableIPAudioVideo $False -RequireWiFiForIPAudio $True -RequireWiFiForIPVideo $True

## Per modificare i criteri di mobilità a livello di utente

1.  Accedere a qualsiasi computer in cui Lync Server Management Shell e Ocscore sono installati come membro del ruolo CsAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Creare nuovi criteri di mobilità a livello di utente e disattivare le funzionalità di mobilità e Chiama da ufficio per un utente specifico. Nella riga di comando digitare:
    
        New-CsMobilityPolicy -Identity <policy name> -EnableMobility $False -EnableOutsideVoice $False
        Grant-CsMobilityPolicy -Identity <user identifier> -PolicyName <policy name>
    
    È possibile disattivare Chiama da ufficio senza disattivare l'accesso alla funzionalità di mobilità. Non è tuttavia possibile disattivare le funzionalità di mobilità senza disattivare anche Chiama da ufficio.
    
    Ad esempio:
    
        New-CsMobilityPolicy "tag:disableOutsideVoice" -EnableOutsideVoice $False
        Grant-CsMobilityPolicy -Identity -MobileUser1@contoso.com -PolicyName Tag:disableOutsideVoice

## Vedere anche

#### Attività

[Disabilitare o abilitare nuovamente gli account utente per Lync Server](lync-server-2013-disable-or-re-enable-user-account-for-lync-server.md)  
[Abilitare gli utenti per VoIP aziendale in Lync Server 2013](lync-server-2013-enable-users-for-enterprise-voice.md)  
[Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)  

#### Concetti

[Definizione dei requisiti per dispositivi mobili per Lync Server 2013](lync-server-2013-defining-your-mobility-requirements.md)  

#### Ulteriori risorse

[New-CsMobilityPolicy](new-csmobilitypolicy.md)  
[Set-CsMobilityPolicy](set-csmobilitypolicy.md)  
[Get-CsMobilityPolicy](get-csmobilitypolicy.md)  
[Grant-CsMobilityPolicy](grant-csmobilitypolicy.md)  
[Remove-CsMobilityPolicy](remove-csmobilitypolicy.md)

