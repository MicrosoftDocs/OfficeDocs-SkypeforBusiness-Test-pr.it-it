---
title: Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013
TOCTitle: Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013
ms:assetid: 6c53aaf5-218b-4bd4-8cea-31bc9d53f1bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398511(v=OCS.15)
ms:contentKeyID: 49300895
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Eseguire la procedura seguente se si desidera modificare criteri vocali. Per creare nuovi criteri vocali, fare riferimento alla procedura descritta in [Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md).


> [!NOTE]
> Se a un utente assegnato a criteri vocali non sono associati record di utilizzo PSTN, l'utente non può effettuare chiamate in uscita. Per visualizzare un elenco di tutti i record di utilizzo PSTN disponibili nella distribuzione VoIP aziendale e le relative proprietà, vedere <A href="lync-server-2013-view-pstn-usage-records.md">Visualizzare record utilizzo PSTN in Lync Server 2013</A>.



## Per modificare criteri vocali

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Criteri vocali**.

4.  Nella pagina **Criteri vocali** fare doppio clic sui nomi dei criteri vocali.
    

    > [!NOTE]
    > L'ambito e il nome sono stati impostati durante la creazione dei criteri vocali e non possono essere modificati.



5.  Facoltativo: in **Modifica criterio vocale** immettere informazioni descrittive aggiuntive per i criteri vocali.

6.  Selezionare o deselezionare le caselle di controllo seguenti per abilitare o disabilitare ogni opzione presente in **Funzionalità di chiamata**:
    
      - La **funzione di escape della segreteria telefonica** fa in modo che le chiamate non vengano immediatamente instradate al sistema di segreteria telefonica del dispositivo mobile dell'utente quando è attivo lo squillo simultaneo, e il telefono è spento, scarico o fuori copertura di rete.
        

        > [!NOTE]
        > Questa funzione può essere configurata soltanto attraverso Lync Server Management Shell

    
      - L'**Inoltro di chiamata** consente agli utenti di inoltrare chiamate ad altri telefoni e dispositivi client. Lync Server 2013 include un numero significativamente maggiore di opzioni di configurazione per l'inoltro di chiamata. Ad esempio, se l'organizzazione desidera evitare che le chiamate in entrata vengano inoltrate esternamente a PSTN, l'amministratore può applicare un criterio vocale specifico per la distribuzione di questa limitazione. La funzionalità è abilitata per impostazione predefinita.
    
      - La **delega** consente agli utenti di specificare altri utenti per l'invio e la ricezione delle chiamate per loro conto. In Lync Server 2013, un delegato può configurare squilli simultanei che consentono alle chiamate in entrata verso il proprio manager di far squillare simultaneamente i propri telefoni di destinazione. In questo modo, al delegato viene offerta una maggiore flessibilità quando si trova a dover rispondere a chiamate destinate al proprio manager. La funzionalità è abilitata per impostazione predefinita.
    
      - **Trasferimento chiamata:** consente agli utenti di trasferire chiamate ad altri utenti. Questa opzione è abilitata per impostazione predefinita.
    
      - **Parcheggio di chiamata:** consente agli utenti di eseguire il parcheggio di chiamate in attesa e quindi di rispondere alla chiamata da un telefono o un client diverso. Questa opzione è disabilitata per impostazione predefinita.
    
      - **Squillo simultaneo** consente lo squillo in telefoni aggiuntivi, ad esempio un telefono cellulare, o in altri dispositivi endpoint per le chiamate in arrivo. Lync Server 2013 include un numero significativamente maggiore di opzioni di configurazione per lo squillo simultaneo. La funzionalità è abilitata per impostazione predefinita.
    
      - **Intercettazione team:** consente agli utenti di un team definito di rispondere alle chiamate per altri membri del team. Questa opzione è abilitata per impostazione predefinita.
    
      - **Abilita reindirizzamento PSTN:** consente il rendirizzamento di chiamate effettuate da utenti assegnati ai criteri ad altri utenti aziendali nella rete PSTN in caso di congestione o non disponibilità della rete WAN. Questa opzione è abilitata per impostazione predefinita.
    
      - **Abilita override criteri larghezza di banda:** consente agli amministratori di eseguire l'override delle decisioni relative ai criteri di controllo di ammissione di chiamata per un utente specifico. Questa opzione è disabilitata per impostazione predefinita.
        

        > [!NOTE]
        > Verrà eseguito l'override dei criteri solo per le chiamate in arrivo all'utente e non per le chiamate in uscita effettuate dall'utente. Dopo che la sessione viene stabilita, l'utilizzo della larghezza di banda viene registrato accuratamente. Questa impostazione deve essere utilizzata con cautela.

    
      - **Abilita traccia chiamate moleste:** consente agli utenti di segnalare chiamate moleste, ad esempio minacce di attentato, utilizzando l'interfaccia utente client, tramite cui le chiamate vengono contrassegnate nella registrazione dettagli chiamata (CDR). Questa opzione è disabilitata per impostazione predefinita.

7.  Per associare e configurare record di utilizzo PSTN per i criteri vocali, eseguire una delle operazioni seguenti:
    
      - Per scegliere uno o più record da un elenco di record di utilizzo PSTN disponibile nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare i record da associare al criterio vocale e quindi fare clic su **OK**.
    
      - Per rimuovere un record di utilizzo PSTN dal criterio vocale, evidenziarlo e quindi fare clic su **Rimuovi**.
    
      - Per definire un nuovo record di utilizzo PSTN e associarlo ai criteri vocali, eseguire le operazioni seguenti:
        
        1.  Fare clic su **Nuovo**.
        
        2.  Nel campo **Nome** immettere un nome descrittivo univoco per il record. È possibile, ad esempio, creare un record di utilizzo PSTN denominato **Redmond** per dipendenti a tempo pieno che si trovano a Redmond e un altro record denominato **RedmondTemp** per i dipendenti temporanei.
            

            > [!NOTE]
            > Il nome del record di utilizzo PSTN deve essere univoco all'interno della distribuzione VoIP aziendale. Dopo avere salvato il record, il campo <STRONG>Nome</STRONG> non può più essere modificato.

        
        3.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
            
              - Per scegliere una o più route da un elenco di tutte le route disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare le route da associare al record di utilizzo PSTN e quindi fare clic su **OK**.
            
              - Per rimuovere una route dal record di utilizzo PSTN, evidenziare la route e fare clic su **Rimuovi**.
            
              - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Per modificare una route già associata al record di utilizzo PSTN, evidenziare la route e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        4.  Fare clic su **OK**.
    
      - Per modificare un record di utilizzo PSTN già associato ai criteri vocali, eseguire le operazioni seguenti:
        
        1.  Evidenziare il record di utilizzo PSTN da modificare e fare clic su **Mostra dettagli**.
        
        2.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
            
              - Per scegliere una o più route da un elenco di tutte le route disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare le route da associare al record di utilizzo PSTN e quindi fare clic su **OK**.
            
              - Per rimuovere una route dal record di utilizzo PSTN, selezionare la route e fare clic su **Rimuovi**.
            
              - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Per modificare una route già associata al record di utilizzo PSTN, evidenziarla e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        3.  Fare clic su **OK**.

8.  Disporre i record di utilizzo PSTN per garantire prestazioni ottimali. Per modificare la posizione di un record nell'elenco, evidenziare il nome del record e fare clic sulla freccia in su o in giù.
    

    > [!NOTE]
    > L'ordine in cui i record di utilizzo PSTN sono elencati nei criteri vocali è significativo. Lync Server consente di scorrere l'elenco dall'alto verso il basso. È consigliabile organizzare l'elenco in base a frequenza di utilizzo, ad esempio: RedmondLocal, RedmondLongDist, RedmondInternational, RedmondBackup.



9.  Per associare e configurare record di utilizzo PSTN per l'inoltro di chiamata e lo squillo simultaneo in questo criterio vocale, eseguire una delle operazioni seguenti:
    
      - Per utilizzare gli stessi record di utilizzo PSTN per l'inoltro di chiamata e lo squillo simultaneo di questo criterio vocale, selezionare l'opzione **Route tramite gli usi PSTN di chiamata** dal menu a discesa.
    
      - Per consentire l'inoltro di chiamata e lo squillo simultaneo soltanto agli utenti interni di Lync, selezionare **Route solo a utenti Lync interni** dal menu a discesa. Le chiamate non verranno inoltrare ai numeri PSTN esterni.
    
      - Per specificare record di utilizzo PSTN differenti per l'inoltro di chiamata e lo squillo simultaneo rispetto a quelli usati per questo criterio vocale, selezionare l'opzione **Route tramite gli usi PSTN di chiamata** dal menu a discesa. Questa opzione visualizza un controllo che consente di selezionare i record di utilizzo PSTN esistenti, o di crearne di nuovi, specifici per l'inoltro di chiamata e lo squillo simultaneo.
        
          - Per scegliere uno o più record in un elenco dei record di utilizzo PSTN per l'inoltro di chiamata e lo squillo simultaneo, fare clic su **Seleziona**. Evidenziare i record che si desidera associare ai criteri vocali dell'inoltro di chiamata e squillo simultaneo e quindi fare clic su **OK**.
        
          - Per rimuovere un record di utilizzo PSTN dal criterio vocale dell'inoltro di chiamata e squillo simultaneo, evidenziarlo e quindi fare clic su **Rimuovi**.
        
          - Per definire un nuovo record di utilizzo PSTN e associarlo al criterio vocale dell'inoltro di chiamata e squillo simultaneo, eseguire le operazioni seguenti:
            
            1.  Fare clic su **Nuovo**.
            
            2.  Nel campo **Nome** immettere un nome descrittivo univoco per il record.
                

                > [!NOTE]
                > Il nome del record di utilizzo PSTN deve essere univoco all'interno della distribuzione di VoIP aziendale. Dopo il salvataggio del record, il campo <STRONG>Nome</STRONG> non può essere modificato.

            
            3.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
                
                  - Per scegliere una o più route nell'elenco di tutte le route disponibili nella distribuzione VoIP aziendale, fare clic su **Seleziona**, evidenziare le route che si desidera associare al record di utilizzo PSTN e quindi fare clic su **OK**.
                
                  - Per rimuovere una route dal record di utilizzo PSTN, evidenziarla e fare clic su **Rimuovi**.
                
                  - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
                
                  - Per modificare una route già associata al record di utilizzo PSTN, evidenziarla e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
            
            4.  Fare clic su **OK**.
        
          - Per modificare un record di utilizzo PSTN già associato al criterio vocale, eseguire le operazioni seguenti:
            
            1.  Evidenziare il record di utilizzo PSTN da modificare e fare clic su **Mostra dettagli**.
            
            2.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
                
                  - Per scegliere una o più route nell'elenco di tutte le route disponibili nella distribuzione VoIP aziendale, fare clic su **Seleziona**, evidenziare le route che si desidera associare al record di utilizzo PSTN e quindi fare clic su **OK**.
                
                  - Per rimuovere una route dal record di utilizzo PSTN, evidenziare la route e fare clic su **Rimuovi**.
                
                  - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
                
                  - Per modificare una route già associata al record di utilizzo PSTN, evidenziare la route e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
            
            3.  Fare clic su **OK**.

10. (Facoltativo) Immettere un numero per testare il criteri vocale e quindi fare clic su **Vai**. I risultati del test vengono visualizzati in **Numero convertito da testare**.
    

    > [!NOTE]
    > È possibile salvare i criteri locali che non hanno ancora superato il test e quindi riconfigurarli in seguito. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



11. Fare clic su **OK**.

12. Nella pagina **Criteri vocali** fare clic su **Commit** e quindi su **Salva tutto**.
    

    > [!NOTE]
    > Quando si creano o modificano criteri vocali, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica di configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



13. (Facoltativo) La funzione di escape della segreteria telefonica rileva quando una chiamata viene risposta automaticamente dalla segreteria telefonica del dispositivo mobile dell'utente, e la disconnette dalla segreteria. In questo modo, la chiamata continua a squillare sugli altri endpoint dell'utente, consentendo a quest'ultimo di rispondere. Per informazioni dettagliate sulla configurazione di un criterio per la segreteria telefonica, vedere [Configurazione dell'escape della segreteria telefonica in Lync Server 2013](lync-server-2013-configuring-voice-mail-escape.md) nella documentazione relativa alla distribuzione.

## Vedere anche

#### Attività

[Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[Visualizzare record utilizzo PSTN in Lync Server 2013](lync-server-2013-view-pstn-usage-records.md)  
[Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md)  
[Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  
[Configurazione dell'escape della segreteria telefonica in Lync Server 2013](lync-server-2013-configuring-voice-mail-escape.md)  

#### Ulteriori risorse

[Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

