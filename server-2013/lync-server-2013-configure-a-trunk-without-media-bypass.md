---
title: 'Lync Server 2013: Configurare un trunk senza bypass multimediale'
TOCTitle: Configurare un trunk senza bypass multimediale
ms:assetid: 3422e93e-7bd2-4470-968c-dc38345b18ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425831(v=OCS.15)
ms:contentKeyID: 49300136
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare un trunk senza bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

Per configurare un trunk con il bypass multimediale disabilitato, attenersi alla procedura che segue. Per configurare un trunk con tale funzionalità abilitata, vedere [Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md).

Una configurazione trunk, come quella descritta di seguito, raggruppa un set di parametri che vengono applicati ai trunk assegnati a questa configurazione trunk. Per una determinata configurazione trunk è possibile specificare un ambito globale (corrispondente a tutti i trunk che non presentano una configurazione di sito o di pool più specifica) o un ambito di sito o di pool. La configurazione trunk a livello di pool viene usata per definire un singolo trunk come ambito di una determinata configurazione trunk.

## Per configurare un trunk senza bypass multimediale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Configurazione trunk** .

4.  Nella pagina **Configurazione trunk** utilizzare uno dei metodi seguenti per configurare un trunk:
    
      - Fare doppio clic su un trunk esistente, ad esempio il trunk **Globale** per visualizzare la finestra di dialogo **Modifica configurazione trunk** .
    
      - Fare clic su **Nuovo** e quindi selezionare un ambito per la nuova configurazione trunk:
        
          - **Trunk sito :** scegliere il sito per questa configurazione trunk in **Seleziona un sito** e quindi fare clic su **OK** . Si noti che se è già stata creata una configurazione trunk per un sito, tale sito non verrà visualizzato in **Seleziona un sito** . La configurazione trunk verrà applicata a tutti i trunk presenti nel sito.
        
          - **Trunk pool :** scegliere il nome del trunk al quale si applica questa configurazione trunk in **Seleziona un servizio** e fare clic su **OK** . Questo trunk può essere il trunk radice o qualsiasi trunk aggiuntivo definito nel Generatore di topologie. Si noti che se è già stata creata una configurazione trunk per un trunk specifico, tale trunk non verrà visualizzato in **Seleziona un servizio** .
    

    > [!NOTE]
    > Dopo aver selezionato l'ambito della configurazione trunk non è possibile modificarlo.<BR>Il campo <STRONG>Nome</STRONG> contiene già il nome del sito o del servizio associato alla configurazione trunk e non è possibile modificarlo.



5.  Selezionare una delle opzioni di **Livello di supporto crittografia** seguenti:
    
      - **Necessario :** è necessario utilizzare la crittografia SRTP (Secure Real-time Transport Protocol) per proteggere il traffico tra il Mediation Server e il gateway o il centralino (PBX).
    
      - **Facoltativo :** la crittografia SRTP verrà utilizzata se è supportata dal provider del servizio o dal produttore delle apparecchiature.
    
      - **Non supportato :** la crittografia SRTP non è supportata dal provider del servizio o dal produttore delle apparecchiature, pertanto non verrà utilizzata.

6.  Verificare che la casella di controllo **Abilita bypass multimediale** sia deselezionata.

7.  Selezionare la casella di controllo **Elaborazione multimediale centralizzata** se è presente un media termination point noto, ad esempio un gateway PSTN (Public Switched Telephone Network) in cui l'IP della terminazione multimediale e quello della terminazione dei segnali coincidono. Deselezionare questa casella di controllo se il trunk non dispone di un media termination point noto.

8.  Se il trunk peer supporta la ricezione di richieste SIP REFER dal Mediation Server, selezionare la casella di controllo **Abilita l'invio del riferimento al gateway** .

9.  (Facoltativo) Per abilitare il routing tra trunk, associare e configurare i record sull'uso della rete PSTN nella configurazione trunk. Gli utilizzi PSTN associati alla configurazione trunk verranno applicati per tutte le chiamate in arrivo tramite il trunk e non provenienti da un endpoint Lync. Per gestire i record sull'utilizzo della rete PSTN associati a una configurazione trunk, usare uno dei metodi seguenti:
    
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
    
    > [!important]  
    > È importante associare i record sull'utilizzo PSTN al peer Mediation Server associato al trunk in corso di configurazione. Se il peer Mediation Server è un gateway PSTN o un Session Border Controller (SBC), è consigliabile che la configurazione trunk non venga associata a un record sull'utilizzo PSTN con routing a una destinazione PSTN o a qualsiasi altro sistema downstream connesso tramite Lync Server.

10. Disporre i record sull'utilizzo PSTN in modo da garantire prestazioni ottimali. Per modificare la posizione di un record nell'elenco, selezionare il record sull'utilizzo PSTN e fare clic sulla freccia verso il basso o verso l'alto.
    
    > [!important]  
    > L'ordine in cui sono elencati i record sull'utilizzo PSTN nella configurazione trunk è significativo. Lync Server usa l'elenco dall'alto verso il basso.

11. Per abilitare il bypass multimediale per i client protetti da NAT o firewall, selezionare **Abilita latch RTP** e un SBC che supporti il latch.

12. È consigliabile selezionare l'opzione **Abilita cronologia inoltro di chiamata** per abilitare l'invio delle informazioni di cronologia delle chiamate al peer gateway del Mediation Server.

13. Per abilitare l'inoltro delle eventuali informazioni disponibili sull'iniziatore delle chiamate PAI tra il lato Mediation Server e il lato gateway (e viceversa), selezionare **Abilita inoltro dati P-Asserted-Identity** .

14. È consigliabile selezionare l'opzione **Abilita timer di failover del routing in uscita** per abilitare il failover veloce. Il gateway associato al trunk può notificare entro 10 secondi che sta elaborando una chiamata in uscita. Il rerouting a un altro trunk si verifica se la notifica non viene ricevuta dal Mediation Server. Nelle reti in cui la latenza può allungare il tempo di risposta oppure il gateway impiega più di 10 secondi a rispondere, il failover veloce deve essere disabilitato.

15. (Facoltativo) Associare e configurare le **regole di conversione per il numero del chiamante** per il trunk. Le regole di conversione si applicano al numero del chiamante per le chiamate in uscita
    
      - Per selezionare una o più regole in un elenco di tutte le regole di conversione disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . In **Seleziona regole di conversione** selezionare le regole da associare al trunk e quindi fare clic su **OK** .
    
      - Per definire una nuova regola di conversione e associarla al trunk, fare clic su **Nuovo** . Per informazioni dettagliate sulla definizione di una nuova regola, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per modificare una regola di conversione già associata al trunk, fare clic sul nome della regola e quindi fare clic su **Mostra dettagli** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per copiare una regola di conversione esistente in modo da utilizzarla come punto di partenza per definire una nuova regola, fare clic sul nome della regola, fare clic su **Copia** e quindi su **Incolla** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md).
    
      - Per rimuovere una regola di conversione dal trunk, evidenziare il nome della regola e fare clic su **Rimuovi** .
    
    > [!security]  
    > Non associare regole di conversione a un trunk se sono state configurate regole di conversione nel trunk peer associato, perché le due regole potrebbero essere in conflitto.

16. (Facoltativo) Associare e configurare **regole di conversione per il numero chiamato** per il trunk. Le regole di conversione si applicano al numero chiamato in una chiamata in uscita.
    
      - Per selezionare una o più regole in un elenco di tutte le regole di conversione disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . In **Seleziona regole di conversione** selezionare le regole da associare al trunk e quindi fare clic su **OK** .
    
      - Per definire una nuova regola di conversione e associarla al trunk, fare clic su **Nuovo** . Per informazioni dettagliate sulla definizione di una nuova regola, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per modificare una regola di conversione già associata al trunk, fare clic sul nome della regola e quindi fare clic su **Mostra dettagli** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md) nella documentazione relativa alla distribuzione.
    
      - Per copiare una regola di conversione esistente in modo da utilizzarla come punto di partenza per definire una nuova regola, fare clic sul nome della regola, fare clic su **Copia** e quindi su **Incolla** . Per informazioni dettagliate, vedere [Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md).
    
      - Per rimuovere una regola di conversione dal trunk, evidenziare il nome della regola e fare clic su **Rimuovi** .
    
    > [!Caution]  
    > Non associare regole di conversione a un trunk se sono state configurate regole di conversione nel trunk peer associato, perché le due regole potrebbero essere in conflitto.

17. Verificare che le regole di conversione del trunk siano disposte nell'ordine corretto. Per modificare la posizione di una regola nell'elenco, evidenziare il nome della regola e quindi fare clic sulla freccia su o giù.
    
    > [!important]  
    > Lync Server scorre l'elenco delle regole di conversione dall'alto verso il basso e utilizza la prima regola corrispondente al numero composto. Se si configura un trunk in modo che un numero composto possa soddisfare più di una regola di conversione, assicurarsi che le regole più restrittive precedano quelle meno restrittive nell'ordine. Se ad esempio sono state definite una regola di conversione relativa a qualsiasi numero di 11 cifre e una regola di conversione relativa solo ai numeri di 11 cifre che iniziano con +1425, assicurarsi che la regola relativa a qualsiasi numero di 11 cifre risulti <em>sotto</em> la regola più restrittiva.

18. Al termine della configurazione del trunk, fare clic su **OK** .

19. Nella pagina **Configurazione trunk** fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si crea o modifica una configurazione trunk, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  

#### Ulteriori risorse

[Definizione delle regole di conversione in Lync Server 2013](lync-server-2013-defining-translation-rules.md)

