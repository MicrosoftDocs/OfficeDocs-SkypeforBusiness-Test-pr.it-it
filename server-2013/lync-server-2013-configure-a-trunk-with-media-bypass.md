---
title: 'Lync Server 2013: Configurare un trunk con bypass multimediale'
TOCTitle: Configurare un trunk con bypass multimediale
ms:assetid: 99d729ea-5a4c-4ff2-a4a3-93a24368da6d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398792(v=OCS.15)
ms:contentKeyID: 49301440
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare un trunk con bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-07_

Eseguire la procedura seguente per configurare un trunk con la funzionalità di bypass multimediale abilitata. Per configurare un trunk con la funzionalità di bypass multimediale disabilitata, vedere [Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md). La funzionalità bypass multimediale è utile se si vuole ridurre il numero dei Mediation Server distribuiti. Un pool Mediation Server viene in genere distribuito in un sito centrale e controlla i gateway nei siti di succursale. Abilitando il bypass multimediale, gli elementi multimediali per chiamate PSTN da client dei siti di succursale possono attraversare direttamente i gateway di tali siti. Le route delle chiamate in uscita e i criteri di VoIP aziendale di Lync Server 2013 devono essere configurati correttamente in modo che le chiamate PSTN dai client nel sito di succursale vengano instradate verso il gateway appropriato.

È consigliabile abilitare il bypass multimediale, tuttavia prima di abilitare tale funzionalità su un trunk SIP, verificare che il proprio provider di trunk SIP qualificato la supporti e sia in grado di soddisfare i requisiti per il funzionamento corretto dello scenario. In particolare, il provider deve disporre di indirizzi IP dei server nella rete interna dell'organizzazione. Se il provider non è in grado di supportare questo scenario, non sarà possibile utilizzare il bypass multimediale. Per informazioni dettagliate, vedere [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md) nella documentazione relativa alla pianificazione.


> [!NOTE]
> Il bypass multimediale non funziona con tutti i gateway PSTN, i sistemi IP-PBX e i Session Border Controller (SBC). Microsoft ha testato una serie di gateway PSTN con partner certificati e ha eseguito alcuni test con i sistemi IP-PBX di Cisco. Il bypass multimediale è supportato solo con i prodotti e le versioni elencate nel sito Web Unified Communications Open Interoperability Program – Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=214406">http://go.microsoft.com/fwlink/p/?linkId=214406</A>.



In una configurazione trunk come quella descritta di seguito viene raggruppato un set di parametri applicati ai trunk assegnati alla configurazione. Un specifica configurazione trunk può avere ambito globale (ovvero essere applicata a tutti i trunk che non prevedono una diversa configurazione di sito o pool) oppure essere destinata a un sito o a un pool. La configurazione trunk a livello di pool viene utilizzata per destinare una specifica configurazione a un singolo trunk.

## Per configurare un trunk con bypass multimediale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Configurazione trunk** .

4.  Nella pagina **Configurazione trunk** utilizzare uno dei metodi seguenti per configurare un trunk:
    
      - Fare doppio clic su un trunk esistente, ad esempio il trunk **Globale** per visualizzare la finestra di dialogo **Modifica configurazione trunk** .
    
      - Fare clic su **Nuovo** e quindi selezionare un ambito per la nuova configurazione trunk:
        
          - **Trunk sito :** selezionare il sito per la configurazione trunk da **Seleziona un sito** e quindi fare clic su **OK** . Tenere presente che se è già stata creata una configurazione trunk per un sito, quest'ultimo non risulta presente in **Seleziona un sito** . Questa configurazione trunk verrà applicata a tutti i trunk nel sito.
        
          - **Trunk pool :** scegliere il nome del trunk a cui si applica la configurazione. Questo trunk può essere quello radice o qualsiasi altro trunk definito in Generatore di topologie. Da **Seleziona un servizio** fare clic su **OK** . Tenere presente che se è già stata creata una configurazione per uno specifico trunk, quest'ultimo non risulta presente in **Seleziona un servizio** .
    

    > [!NOTE]
    > Dopo aver selezionato l'ambito della configurazione trunk non è possibile modificarlo.<BR>Il campo <STRONG>Nome</STRONG> contiene già il nome del sito o del servizio associato alla configurazione trunk e non è possibile modificarlo.



5.  Specificare un valore in **Numero massimo di dialoghi anticipati supportati** . Si tratta del numero massimo di risposte instradate che un gateway PSTN/IP-PBX, oppure un Session Border Controller (SBC) di un provider di servizi di telefonia Internet (ITSP) può ricevere per una richiesta INVITE inviata al Mediation Server. Il valore predefinito è 20.
    

    > [!NOTE]
    > Prima di modificare questo valore, consultare il provider di servizi o il produttore delle apparecchiature per informazioni più dettagliate sulle capacità del sistema in uso.



6.  Selezionare una delle opzioni di **Livello di supporto crittografia** seguenti:
    
      - **Necessario :** è necessario utilizzare la crittografia SRTP (Secure Real-time Transport Protocol) per proteggere il traffico tra il Mediation Server e il gateway o il centralino (PBX).
    
      - **Facoltativo :** la crittografia SRTP verrà utilizzata se è supportata dal provider del servizio o dal produttore delle apparecchiature.
    
      - **Non supportato :** la crittografia SRTP non è supportata dal provider del servizio o dal produttore delle apparecchiature, pertanto non verrà utilizzata.

7.  Selezionare la casella di controllo **Abilita bypass multimediale** se si desidera che gli elementi multimediali ignorino il Mediation Server per l'elaborazione da parte del trunk peer.
    
    > [!IMPORTANT]  
    > Per un corretto funzionamento del bypass multimediale, è necessario che il gateway PSTN, il sistema IP-PBX o il Session Border Controller supporti determinate funzionalità. Per informazioni dettagliate, vedere <a href="lync-server-2013-planning-for-media-bypass.md">Pianificazione del bypass multimediale in Lync Server 2013</a> nella documentazione relativa alla pianificazione.

8.  Selezionare la casella di controllo **Elaborazione multimediale centralizzata** se esiste un punto di terminazione multimediale noto, ad esempio un gateway PSTN in cui la terminazione multimediale ha lo stesso IP della terminazione di segnalazione. Deselezionare la casella di controllo se il trunk non dispone di un punto di terminazione multimediale noto.

9.  Se il trunk peer supporta la ricezione di richieste SIP REFER dal Mediation Server, selezionare la casella di controllo **Abilita l'invio del riferimento al gateway** .
    

    > [!NOTE]
    > Se si disabilita questa opzione mentre è selezionata l'opzione <STRONG>Abilita bypass multimediale</STRONG> saranno necessarie ulteriori impostazioni. Se il trunk peer non supporta la ricezione di richieste SIP REFER dal Mediation Server ed è abilitato il bypass multimediale, sarà inoltre necessario eseguire il cmdlet <STRONG>Set-CsTrunkConfiguration</STRONG> per disabilitare RTCP per le chiamate attive e in attesa in modo da supportare le condizioni appropriate per il bypass multimediale. Per informazioni dettagliate, vedere la documentazione di <A href="lync-server-2013-lync-server-management-shell.md">Lync Server Management Shell</A>.<BR>In alternativa, è possibile selezionare <STRONG>Abilita il riferimento usando il controllo delle chiamate di terze parti</STRONG> se si vuole applicare il bypass multimediale alle chiamate trasferite e il gateway non supporta richieste SIP REFER.



10. (Facoltativo) Per abilitare il routing tra trunk, associare e configurare i record sull'uso della rete PSTN nella configurazione trunk. Gli utilizzi PSTN associati alla configurazione trunk verranno applicati per tutte le chiamate in arrivo tramite il trunk e non provenienti da un endpoint Lync. Per gestire i record sull'utilizzo della rete PSTN associati a una configurazione trunk, usare uno dei metodi seguenti:
    
      - Per selezionare uno o più record da un elenco di tutti i record sull'utilizzo della rete PSTN disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . Evidenziare i record da associare alla configurazione trunk e quindi fare clic su **OK** .
    
      - Per rimuovere un record sull'utilizzo PSTN dalla configurazione trunk, selezionarlo e fare clic su **Rimuovi** .
    
      - Per definire un nuovo record sull'utilizzo PSTN e associarlo alla configurazione trunk, eseguire le operazioni seguenti:
        
        1.  Fare clic su **Nuovo** .
        
        2.  Nel campo **Nome** specificare un nome descrittivo univoco per il record.
            

            > [!NOTE]
            > Il record sull'utilizzo PSTN deve essere univoco all'interno della distribuzione di VoIP aziendale. Dopo aver salvato il record, il campo <STRONG>Nome</STRONG> non può essere modificato.

        
        3.  Usare uno o più dei metodi seguenti per associare e configurare route per il record sull'utilizzo PSTN:
            
              - Per selezionare una o più route dall'elenco di tutte quelle disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . Evidenziare le route da associare al record sull'utilizzo PSTN e fare clic su **OK** .
            
              - Per rimuovere una route dal record sull'utilizzo PSTN, selezionare la route e fare clic su **Rimuovi** .
            
              - Per definire una nuova route e associarla al record sull'utilizzo PSTN, fare clic su **Nuovo** . Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Per modificare una route associata al record sull'utilizzo PSTN, selezionare la route e fare clic su **Mostra dettagli** . Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        4.  Fare clic su **OK** .
    
      - Per modificare un record sull'utilizzo PSTN già associato alla configurazione trunk, effettuare le operazioni seguenti:
        
        1.  Selezionare il record sull'utilizzo PSTN da modificare e fare clic su **Mostra dettagli** .
        
        2.  Usare uno o più dei metodi seguenti per associare e configurare route per il record sull'utilizzo PSTN:
            
              - Per selezionare una o più route dall'elenco di tutte quelle disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . Evidenziare le route da associare al record sull'utilizzo PSTN e fare clic su **OK** .
            
              - Per rimuovere una route dal record sull'utilizzo PSTN, selezionare la route e fare clic su **Rimuovi** .
            
              - Per definire una nuova route e associarla al record sull'utilizzo PSTN, fare clic su **Nuovo** . Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Per modificare una route associata al record sull'utilizzo PSTN, selezionare la route e fare clic su **Mostra dettagli** . Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        3.  Fare clic su **OK** .
    
    > [!IMPORTANT]  
    > È importante associare i record sull'utilizzo PSTN al peer Mediation Server associato al trunk in corso di configurazione. Se il peer Mediation Server è un gateway PSTN o un Session Border Controller (SBC), è consigliabile che la configurazione trunk non venga associata a un record sull'utilizzo PSTN con routing a una destinazione PSTN o a qualsiasi altro sistema downstream connesso tramite Lync Server.

11. Disporre i record sull'utilizzo PSTN in modo da garantire prestazioni ottimali. Per modificare la posizione di un record nell'elenco, selezionare il record sull'utilizzo PSTN e fare clic sulla freccia verso il basso o verso l'alto.
    
    > [!IMPORTANT]  
    > L'ordine in cui sono elencati i record sull'utilizzo PSTN nella configurazione trunk è significativo. Lync Server usa l'elenco dall'alto verso il basso.

12. È consigliabile selezionare l'opzione **Abilita latch RTP** per abilitare il bypass multimediale per i client dietro NAT o firewall e uno SBC che supporta il latch.

13. È consigliabile selezionare l'opzione **Abilita cronologia inoltro di chiamata** per abilitare l'invio delle informazioni di cronologia delle chiamate al peer gateway del Mediation Server.

14. È consigliabile selezionare l'opzione **Abilita inoltro dati P-Asserted-Identity** per abilitare l'inoltro delle informazioni sull'origine della chiamata P-Asserted-Identity (PAI) tra il lato del Mediation Server e il lato gateway (e viceversa), se presente.

15. È consigliabile selezionare l'opzione **Abilita timer di failover del routing in uscita** per abilitare il failover veloce. Il gateway associato al trunk può notificare entro 10 secondi che sta elaborando una chiamata in uscita. Il rerouting a un altro trunk si verifica se la notifica non viene ricevuta dal Mediation Server. Nelle reti in cui la latenza può allungare il tempo di risposta oppure il gateway impiega più di 10 secondi a rispondere, il failover veloce deve essere disabilitato.

16. (Facoltativo) Associare e configurare le **regole di conversione per il numero del chiamante** per il trunk. Le regole di conversione si applicano al numero del chiamante per le chiamate in uscita
    
      - Per selezionare una o più regole in un elenco di tutte le regole di conversione disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . In **Seleziona regole di conversione** selezionare le regole da associare al trunk e quindi fare clic su **OK** .
    
      - Per definire una nuova regola di conversione e associarla al trunk, fare clic su **Nuovo** . Per informazioni dettagliate sulla definizione di una nuova regola, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per modificare una regola di conversione già associata al trunk, fare clic sul nome della regola e quindi fare clic su **Mostra dettagli** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per copiare una regola di conversione esistente in modo da utilizzarla come punto di partenza per definire una nuova regola, fare clic sul nome della regola, fare clic su **Copia** e quindi su **Incolla** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md).
    
      - Per rimuovere una regola di conversione dal trunk, evidenziare il nome della regola e fare clic su **Rimuovi** .
    

    > [!WARNING]
    > Non associare regole di conversione a un trunk se sono state configurate regole di conversione nel trunk peer associato, perché le due regole potrebbero essere in conflitto.



17. (Facoltativo) Associare e configurare **regole di conversione per il numero chiamato** per il trunk. Le regole di conversione si applicano al numero chiamato in una chiamata in uscita.
    
      - Per selezionare una o più regole in un elenco di tutte le regole di conversione disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . In **Seleziona regole di conversione** selezionare le regole da associare al trunk e quindi fare clic su **OK** .
    
      - Per definire una nuova regola di conversione e associarla al trunk, fare clic su **Nuovo** . Per informazioni dettagliate sulla definizione di una nuova regola, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per modificare una regola di conversione già associata al trunk, fare clic sul nome della regola e quindi fare clic su **Mostra dettagli** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per copiare una regola di conversione esistente in modo da utilizzarla come punto di partenza per definire una nuova regola, fare clic sul nome della regola, fare clic su **Copia** e quindi su **Incolla** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md).
    
      - Per rimuovere una regola di conversione dal trunk, evidenziare il nome della regola e fare clic su **Rimuovi** .
    

    > [!WARNING]
    > Non associare regole di conversione a un trunk se sono state configurate regole di conversione nel trunk peer associato, perché le due regole potrebbero essere in conflitto.



18. Verificare che le regole di conversione del trunk siano disposte nell'ordine corretto. Per modificare la posizione di una regola nell'elenco, evidenziare il nome della regola e quindi fare clic sulla freccia su o giù.
    
    > [!IMPORTANT]  
    > Lync Server 2013 scorre l'elenco delle regole di conversione dall'alto verso il basso e utilizza la prima regola corrispondente al numero composto. Se si configura un trunk in modo che un numero composto possa soddisfare più di una regola di conversione, assicurarsi che le regole più restrittive risultino al di sopra di quelle meno restrittive. Se ad esempio sono state definite una regola di conversione relativa a qualsiasi numero di 11 cifre e una regola di conversione relativa solo ai numeri di 11 cifre che iniziano con +1425, assicurarsi che la regola relativa a qualsiasi numero di 11 cifre risulti <em>sotto</em> la regola più restrittiva.

19. Al termine della configurazione del trunk, fare clic su **OK** .

20. Nella pagina **Configurazione trunk** fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si crea o modifica una configurazione trunk, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



Dopo avere configurato il trunk, continuare a configurare il bypass multimediale scegliendo fra le relative opzioni globali, come spiegato in [Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md) nella documentazione relativa alla distribuzione.

## Vedere anche

#### Attività

[Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md)  

#### Concetti

[Configurare il bypass multimediale in Lync Server 2013](lync-server-2013-configure-media-bypass.md)  
[Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md)  

#### Ulteriori risorse

[Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md)

