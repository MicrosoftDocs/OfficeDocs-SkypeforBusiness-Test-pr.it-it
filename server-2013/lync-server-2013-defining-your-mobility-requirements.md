---
title: 'Lync Server 2013: Definizione dei requisiti per dispositivi mobili'
TOCTitle: Definizione dei requisiti per dispositivi mobili
ms:assetid: b7608335-cdeb-4aae-8e4b-d80c55f0d62b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690039(v=OCS.15)
ms:contentKeyID: 49301760
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dei requisiti per dispositivi mobili per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

    Some information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Durante la fase di pianificazione per la funzionalità di mobilità di Lync Server 2013, quando si utilizzano i client Lync 2010 Mobile e Lync 2013 Mobile, si prendono alcune decisioni che determinano i passaggi per la distribuzione.

Di seguito sono elencate le decisioni da considerare:

  - **Utilizzo dell'individuazione automatica per i client mobili di Lync**
    
    Se si desidera supportare l'individuazione automatica, è necessario creare nuovi record DNS (Domain Name System) interni ed esterni, aggiungere nomi alternativi del soggetto ai certificati nei Front End Server, nei Director e nel proxy inverso, nonché modificare le regole di pubblicazione esistenti nel proxy inverso. Per informazioni dettagliate, vedere [Requisiti tecnici per i dispositivi mobili in Lync Server 2013](lync-server-2013-technical-requirements-for-mobility.md). Con l'individuazione automatica gli utenti possono individuare automaticamente i servizi Web di Lync Server 2013 da qualsiasi posizione all'interno o all'esterno della rete aziendale senza dover immettere URL nelle impostazioni dei dispositivi mobili.
    
    Se si utilizzano impostazioni manuali anziché l'individuazione automatica, gli utenti di dispositivi mobili devono immettere manualmente gli URL seguenti nei dispositivi:
    
      - https://\<FQDNPoolEst\>/Autodiscover/autodiscoverservice.svc/root per l'accesso esterno
    
      - https://\<FQDNPoolIn\>/AutoDiscover/ autodiscoverservice.svc/root per l'accesso interno
    
    È consigliabile utilizzare l'individuazione automatica. Le impostazioni manuali devono essere utilizzate principalmente per attività di risoluzione dei problemi.

  - **Se si decide di supportare l'individuazione automatica, aggiornamento dei certificati nel proxy inverso con nomi alternativi soggetto per ogni dominio SIP**
    
    In presenza di numerosi domini SIP, l'aggiornamento dei certificati pubblici nel proxy inverso può diventare molto oneroso. In questo caso, è possibile scegliere di implementare l'individuazione automatica in modo che la richiesta iniziale del servizio di individuazione automatica utilizzi HTTP sulla porta 80, anziché HTTPS sulla porta 443. Questo approccio non è tuttavia consigliato. Se si decide di scegliere questa alternativa, non è necessario aggiornare i certificati nel proxy inverso, ma occorre creare una regola di pubblicazione Web per HTTP sulla porta 80. Per ulteriori dettagli, vedere [Requisiti tecnici per i dispositivi mobili in Lync Server 2013](lync-server-2013-technical-requirements-for-mobility.md).

  - **Supporto di client mobili di Lync sia all'interno che all'esterno della rete aziendale o solo all'interno**
    
    Se si desidera supportare client mobili interni ed esterni alla rete, i dispositivi mobili possono accedere alle funzionalità di mobilità da qualsiasi posizione. La configurazione predefinita prevede il supporto di client sia all'interno che all'esterno della rete aziendale.
    
    Sebbene la configurazione predefinita consenta il passaggio del traffico dei client mobili attraverso il sito esterno, è possibile limitare questo traffico alla rete aziendale interna. In questo caso, gli utenti possono utilizzare le applicazioni per dispositivi mobili Lync nei rispettivi dispositivi mobili solo quando si trovano all'interno della rete.
    
    Per le distribuzioni che supportano i dispositivi mobili mediante il servizio Mobility Mcx e Lync 2010 Mobile, si esegue il cmdlet **Set-CsMcxConfiguration**. Per impostare i dispositivi mobili solo per l'utilizzo interno, si utilizzerà un comando analogo al seguente:
    
        Set-CsMcxConfiguration -Identity site:Redmond -ExposedWebURL Internal
    

    > [!NOTE]
    > Non sono necessarie altre configurazioni per UCWA. UCWA non dispone di una configurazione solo interna equivalente.

    
    > [!IMPORTANT]  
    > Se si utilizza un Front End Server o un pool Front End di Lync Server 2013 e <strong>non si dispone</strong> di Front End Server o pool Front End di Lync Server 2010, <strong>non vi sono requisiti relativi al salvataggio permanente dei cookie</strong>. Se è necessario mantenere Front End Server o pool Front End di Lync Server 2010, per il salvataggio permanente dei cookie si applicheranno le stesse regole valide in Lync Server 2010.

  - **Supporto delle notifiche push per dispositivi Apple iOS e Windows Phone**
    
    Se si supportano notifiche push, i dispositivi Apple iOS e Windows Phone supportati riceveranno una notifica degli eventi che si verificano quando l'applicazione mobile è inattiva. È necessario configurare il server perimetrale per impostare una relazione federativa con il servizio di notifica Push di Lync Server basato su cloud, disponibile nel centro dati di Lync Online, ed eseguire un cmdlet per abilitare le notifiche Push.
    
    Se si desidera supportare notifiche Push nella rete Wi-Fi, oltre a supportare le notifiche Push su reti dati o 3G dei provider di dispositivi mobili, è necessario aprire la porta 5223 in uscita nella rete Wi-Fi aziendale. Il supporto delle notifiche Push nella rete Wi-Fi consente di supportare dispositivi mobili che utilizzano solo Wi-Fi e quelli con una ricezione di scarsa qualità in ambienti chiusi.
    
    > [!IMPORTANT]  
    > L'apertura della porta TCP 5223 è necessaria solo quando si supportano dispositivi Apple che eseguono il client Lync 2010 Mobile.   
     
    Se non si supportano le notifiche Push, gli utenti di dispositivi mobili Apple e di Windows Phone non riceveranno informazioni sugli eventi che si verificano quando l'applicazione mobile è inattiva, come inviti di messaggistica istantanea o messaggi persi.
    

    > [!NOTE]
    > I client Lync 2013 Mobile su dispositivi Apple non richiedono la notifica Push. I client Lync 2013 Mobile su Windows Phone utilizzano la notifica Push. La pianificazione della notifica Push e il fornitore di servizi di accesso a terze parti della notifica Push sono gli stessi per Lync Mobile su dispositivi Windows Phone e Apple non in grado di eseguire il client Lync 2013 Mobile.



  - **Accesso alle funzionalità di mobilità per tutti gli utenti o selezione degli utenti con accesso a queste funzionalità**
    
    Nella tabella seguente vengono descritte le funzionalità disponibili per gli utenti in Lync Server 2013. Le impostazioni predefinite consentono la chiamata tramite ufficio e VoIP (Voice over IP) e abilitano il servizio Mobility. Di seguito sono elencate tutte le opzioni disponibili:
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Funzionalità/Nome parametro/Ambito (è possibile che i nomi di parametro dei criteri non corrispondano)</th>
    <th>Descrizione</th>
    <th>Introduzione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Abilita il servizio Mobility</p>
    <p>Nome parametro: <code>EnableMobility</code></p>
    <p>Ambito: globale/sito/utente</p></td>
    <td><p>Impostazione amministrativa per controllare gli utenti di un determinato ambito che hanno installato Lync Mobile. Se il criterio è impostato su False, l'utente non sarà in grado di accedere al client.</p>
    <p>L'impostazione predefinita è True.</p></td>
    <td><p>Aggiornamento cumulativo per Lync Server 2010: novembre 2011</p></td>
    </tr>
    <tr class="even">
    <td><p>Abilita controllo vocale esterno</p>
    <p>Nome parametro: <code>EnableOutsideVoice</code></p>
    <p>Ambito: globale/sito/utente</p></td>
    <td><p>Controlla la possibilità di un utente di utilizzare la chiamata tramite ufficio, una funzionalità che consente agli utenti di effettuare e ricevere chiamate utilizzando il numero dell'ufficio anziché quello del cellulare. Se impostato su False, l'utente non sarà in grado di effettuare o ricevere chiamate utilizzando il numero dell'ufficio dal dispositivo mobile.</p>
    <p>L'impostazione predefinita è True.</p></td>
    <td><p>Aggiornamento cumulativo per Lync Server 2010: novembre 2011</p></td>
    </tr>
    <tr class="odd">
    <td><p>Abilita audio e video IP</p>
    <p>Nome parametro: <code>EnableIPAudioVideo</code></p>
    <p>Ambito: globale/sito/utente</p></td>
    <td><p>Controlla se un utente può utilizzare VoIP per effettuare o ricevere chiamate vocali o videochiamate sul dispositivo mobile. Se impostato su False, l'utente non sarà in grado di effettuare o ricevere chiamate VoIP o videochiamate sul dispositivo.</p>
    <p>L'impostazione predefinita è True.</p></td>
    <td><p>Microsoft Lync Server 2013</p></td>
    </tr>
    <tr class="even">
    <td><p>Richiedi Wi-Fi per audio IP</p>
    <p>Nome parametro: <code>RequireWiFiForIPAudio</code></p>
    <p>Ambito: globale/sito/utente</p></td>
    <td><p>Questa impostazione definisce se il client dovrà effettuare e ricevere le chiamate tramite VoIP su Wi-Fi anziché sulla rete dati cellulare. Se impostato su True, l'utente sarà in grado di effettuare e ricevere chiamate VoIP solo se connesso a una rete Wi-Fi.</p>
    <p>L'impostazione predefinita è False.</p></td>
    <td><p>Microsoft Lync Server 2013</p></td>
    </tr>
    <tr class="odd">
    <td><p>Richiedi Wi-Fi per video IP</p>
    <p>Nome parametro: <code>RequireWiFiForIPVideo</code></p>
    <p>Ambito: globale/sito/utente</p></td>
    <td><p>Questa impostazione definisce se il client dovrà effettuare e ricevere le videochiamate su Wi-Fi anziché sulla rete dati cellulare. Se impostato su True, l'utente sarà in grado di effettuare e ricevere videochiamate solo se connesso a una rete Wi-Fi.</p>
    <p>L'impostazione predefinita è False.</p></td>
    <td><p>Microsoft Lync Server 2013</p></td>
    </tr>
    </tbody>
    </table>
    
    Per una descrizione delle impostazioni criteri configurabili e della gestione dei criteri, vedere [New-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsMobilityPolicy), [Set-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMobilityPolicy), [Get-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMobilityPolicy), [Grant-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Grant-CsMobilityPolicy) e [Remove-CsMobilityPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsMobilityPolicy).

  - **Partecipazione alle conferenze con un clic da parte degli utenti non abilitati per VoIP aziendale**
    
    Per poter accedere alle funzionalità di mobilità e alla chiamata tramite ufficio, gli utenti devono essere abilitati per VoIP aziendale. Gli utenti non abilitati per VoIP aziendale, tuttavia, possono partecipare alle conferenze facendo clic sul collegamento nel dispositivo mobile, se sono loro assegnati criteri vocali appropriati. È possibile assegnare criteri vocali specifici a questi utenti o assicurarsi che esistano criteri globali o a livello di sito applicati a tali utenti. I criteri vocali assegnati devono disporre di record di utilizzo PSTN e route che definiscono le aree che possono chiamare gli utenti per partecipare a una conferenza. Per informazioni dettagliate sull'impostazione dei criteri vocali, dei record di utilizzo PSTN e delle route, vedere [Configurazione di criteri vocali, record di utilizzo PSTN e route vocali in Lync Server 2013](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md).
    

    > [!NOTE]
    > Per gli utenti mobili che desiderano partecipare con un clic devono essere disponibili criteri vocali insieme ai record di utilizzo PSTN e alle route vocali correlati, perché il clic sul collegamento nel dispositivo mobile dà origine a una chiamata in uscita da Lync Server 2013.



## Vedere anche

#### Concetti

[Requisiti tecnici per i dispositivi mobili in Lync Server 2013](lync-server-2013-technical-requirements-for-mobility.md)  

#### Ulteriori risorse

[Configurazione di criteri vocali, record di utilizzo PSTN e route vocali in Lync Server 2013](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

