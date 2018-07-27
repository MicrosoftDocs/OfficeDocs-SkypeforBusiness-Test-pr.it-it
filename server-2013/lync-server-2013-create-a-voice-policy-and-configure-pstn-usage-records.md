---
title: Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013
TOCTitle: Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013
ms:assetid: e6ff27e0-e2d1-4445-840f-08f738200c20
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399027(v=OCS.15)
ms:contentKeyID: 49302293
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Eseguire la procedura seguente se si desidera creare un nuovo criterio vocale. Se si desidera modificare un criterio vocale, vedere [Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md) per la procedura.


> [!NOTE]
> Ogni criterio vocale deve essere associato ad almeno un record di utilizzo PSTN (Public Switched Telephone Network). Per visualizzare un elenco di tutti i record di utilizzo PSTN disponibili nella distribuzione di VoIP aziendale, insieme alle relative proprietà, vedere <A href="lync-server-2013-view-pstn-usage-records.md">Visualizzare record utilizzo PSTN in Lync Server 2013</A>.



## Per creare un criterio vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Criteri vocali**.

4.  Nella pagina **Criteri vocali** fare clic su **Nuovo** e quindi selezionare un ambito per il nuovo criterio:
    
      - **Criteri sito** è applicabile a un intero sito, ad eccezione degli eventuali utenti o gruppi assegnati a un criterio utente. Se si seleziona Sito come ambito di un criterio, è necessario scegliere il sito nella finestra di dialogo **Seleziona un sito**. Se per un sito è già stato creato un criterio vocale, il sito non viene visualizzato nella finestra di dialogo **Seleziona un sito**.
    
      - **Criteri utente** è applicabile a specifici utenti o gruppi.

5.  Se l'ambito del criterio vocale è Utente, immettere un nome descrittivo nel campo **Nome**.
    

    > [!NOTE]
    > Se l'ambito è Sito, il campo <STRONG>Nome</STRONG> in <STRONG>Criteri vocali</STRONG> è prepopolato con il nome del sito e non può essere modificato.



6.  (Facoltativo) Immettere informazioni descrittive aggiuntive per il criterio vocale.

7.  Selezionare o deselezionare le caselle di controllo seguenti per abilitare o disabilitare ogni funzionalità di chiamataper il criterio vocale:
    
      - L'**escape della segreteria telefonica** impedisce che le chiamate vengano instradate immediatamente al sistema di segreteria telefonica del cellulare dell'utente quando è configurato lo squillo simultaneo e il telefono è spento, scarico o non riceve il segnale.
        

        > [!NOTE]
        > Questa funzionalità può essere configurata solo tramite Lync Server Management Shell

    
      - L'**inoltro di chiamata** consente agli utenti di inoltrare chiamate ad altri telefoni e dispositivi client. Lync Server 2013 offre una gamma molto più ampia di opzioni di configurazione per l'inoltro di chiamata. Se un'organizzazione non desidera consentire l'inoltre delle chiamate in arrivo all'esterno sulla rete PSTN, ad esempio, un amministratore può applicare criteri vocali speciali per distribuire questa restrizione. Funzionalità abilitata per impostazione predefinita.
    
      - La **delega** consente agli utenti di specificare altri utenti per l'invio e la ricezione delle chiamate per loro conto. In Lync Server 2013, un delegato può configurare lo squillo simultaneo in modo che le chiamate in arrivo per il responsabile generino uno squillo simultaneo per tutte le destinazioni del delegato. In questo modo il delegato può contare su una maggiore flessibilità per la risposta alle chiamate indirizzate al responsabile. Funzionalità abilitata per impostazione predefinita.
    
      - Il **trasferimento di chiamata** consente agli utenti di trasferire chiamate ad altri utenti. Funzionalità abilitata per impostazione predefinita.
    
      - Il **parcheggio di chiamata** consente agli utenti di parcheggiare le chiamate e quindi di rispondere da un telefono o client diverso. Funzionalità disabilitata per impostazione predefinita.
    
      - Lo **squillo simultaneo** consente lo squillo su telefoni aggiuntivi (ad esempio, un cellulare) o altri dispositivi endpoint per le chiamate in arrivo. In Lync Server 2013 è disponibile una gamma molto più ampia di opzioni di configurazione per lo squillo simultaneo. Funzionalità abilitata per impostazione predefinita.
    
      - L'**intercettazione team** consente agli utenti in uno team specificato di rispondere alle chiamate per gli altri membri del team. Funzionalità abilitata per impostazione predefinita.
    
      - Il **reindirizzamento PSTN** consente di reindirizzare le chiamate effettuate dagli utenti assegnati a questo criterio ad altri utenti dell'organizzazione sulla rete PSTN, in caso di congestione o non disponibilità della rete WAN. Funzionalità abilitata per impostazione predefinita.
    
      - L'**override dei criteri di larghezza di banda** consente agli amministratori di ignorare le decisioni per i criteri di controllo di ammissione di chiamata per un particolare utente. Funzionalità disabilitata per impostazione predefinita.
        

        > [!NOTE]
        > L'override dei criteri verrà eseguito solo per le chiamate in arrivo indirizzate all'utente, ma non per le chiamate in uscita effettuate dall'utente. Dopo l'attivazione della sessione, il consumo di larghezza di banda verrà registrato accuratamente. Questa impostazione dovrebbe essere utilizzata raramente e riservata per decisioni appropriate di controllo di ammissione di chiamata.

    
      - La **traccia delle chiamate moleste** consente agli utenti di segnalare chiamate moleste (ad esempio minacce di bomba) tramite l'interfaccia utente del client che a sua volta contrassegna tali chiamate nelle registrazioni dei dettagli delle chiamate (CDR). Questa funzionalità è disabilitata per impostazione predefinita.

8.  Per associare e configurare record di utilizzo PSTN per questo criterio vocale, eseguire una delle operazioni seguenti:
    
      - Per scegliere uno o più record da un elenco di record di utilizzo PSTN disponibile nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare i record da associare al criterio vocale e quindi fare clic su **OK**.
    
      - Per rimuovere un record di utilizzo PSTN dal criterio vocale, evidenziarlo e quindi fare clic su **Rimuovi**.
    
      - Per definire un nuovo record di utilizzo PSTN e associarlo al criterio vocale, eseguire le operazioni seguenti:
        
        1.  Fare clic su **Nuovo**.
        
        2.  Nel campo **Nome** immettere un nome descrittivo univoco per il record. È ad esempio possibile creare un record di utilizzo PSTN denominato **Redmond** per i dipendenti a tempo pieno ubicati a Redmond e un altro denominato **RedmondTemps** per i dipendenti a tempo determinato.
            

            > [!NOTE]
            > Il nome del record di utilizzo PSTN deve essere univoco all'interno della distribuzione di VoIP aziendale. Dopo il salvataggio del record, il campo <STRONG>Nome</STRONG> non può essere modificato.

        
        3.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
            
              - Per scegliere una o più route da un elenco di tutte le route disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare le route da associare al record di utilizzo PSTN e quindi fare clic su **OK**.
            
              - Per rimuovere una route dal record di utilizzo PSTN, evidenziarla e quindi fare clic su **Rimuovi**.
            
              - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Per modificare una route già associata al record di utilizzo PSTN, evidenziarla e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        4.  Fare clic su **OK**.
    
      - Per modificare un record di utilizzo PSTN già associato al criterio vocale, eseguire le operazioni seguenti:
        
        1.  Evidenziare il record di utilizzo PSTN che si desidera modificare e quindi fare clic su **Mostra dettagli**.
        
        2.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
            
              - Per scegliere una o più route da un elenco di tutte le route disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare le route da associare al record di utilizzo PSTN e quindi fare clic su **OK**.
            
              - Per rimuovere una route dal record di utilizzo PSTN, evidenziarla e quindi fare clic su **Rimuovi**.
            
              - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
            
              - Per modificare una route già associata al record di utilizzo PSTN, evidenziarla e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
        
        3.  Fare clic su **OK**.

9.  Disporre i record di utilizzo PSTN in modo da garantire prestazioni ottimali. Per modificare la posizione di un record nell'elenco, evidenziare il relativo nome e fare clic sulla freccia SU o GIÙ.
    
    > [!IMPORTANT]  
    > L'ordine in cui i record di utilizzo PSTN sono disposti nel criterio vocale è significativo. Lync Server attraversa l'elenco dall'alto verso il basso. È consigliabile organizzare l'elenco in base alla frequenza di utilizzo, ad esempio: RedmondLocal, RedmondLongDist, RedmondInternational, RedmondBackup.

10. Per associare e configurare record di utilizzo PSTN per l'inoltro di chiamata e lo squillo simultaneo in questo criterio vocale, eseguire una delle operazioni seguenti:
    
      - Per utilizzare gli stessi record di utilizzo PSTN per l'inoltro di chiamata e lo squillo simultaneo del criterio vocale, selezionare **Route tramite gli usi PSTN di chiamata** nel menu a discesa.
    
      - Per consentire l'inoltro di chiamata e lo squillo simultaneo solo per gli utenti di Lync interni, selezionare l'opzione **Route solo a utenti Lync interni** nel menu a discesa. Le chiamate non verranno inoltrate a numeri PSTN esterni.
    
      - Per specificare record di utilizzo PSTN diversi per l'inoltro di chiamata e lo squillo simultaneo rispetto a quelli utilizzati per il criterio vocale, selezionare l'opzione **Route tramite usi PSTN personalizzati** nell'elenco a discesa. Questa opzione consente di visualizzare un controllo per selezionare record di utilizzo PST esistenti o creare nuovi record di utilizzo PSTN specificatamente per l'inoltro di chiamata e lo squillo simultaneo.
        
          - Per scegliere uno o più record da un elenco di record di utilizzo PSTN per l'inoltro di chiamata e lo squillo simultaneo, fare clic su **Seleziona**. Evidenziare i record da associare al criterio per l'inoltro di chiamata e lo squillo simultaneo, quindi fare clic su **OK**.
        
          - Per rimuovere un record di utilizzo PSTN dai criteri per l'inoltro di chiamata e lo squillo simultaneo, evidenziarlo e quindi fare clic su **Rimuovi**.
        
          - Per definire un nuovo record di utilizzo PSTN e associarlo ai criteri per l'inoltro di chiamata e lo squillo simultaneo, eseguire le operazioni seguenti:
            
            1.  Fare clic su **Nuovo**.
            
            2.  Nel campo **Nome** immettere un nome descrittivo univoco per il record.
                

                > [!NOTE]
                > Il nome del record di utilizzo PSTN deve essere univoco all'interno della distribuzione di VoIP aziendale. Dopo il salvataggio del record, il campo <STRONG>Nome</STRONG> non può essere modificato.

            
            3.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
                
                  - Per scegliere una o più route da un elenco di tutte le route disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare le route da associare al record di utilizzo PSTN e quindi fare clic su **OK**.
                
                  - Per rimuovere una route dal record di utilizzo PSTN, evidenziarla e fare clic su **Rimuovi**.
                
                  - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
                
                  - Per modificare una route già associata al record di utilizzo PSTN, evidenziarla e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
            
            4.  Fare clic su **OK**.
        
          - Per modificare un record di utilizzo PSTN già associato al criterio vocale, eseguire le operazioni seguenti:
            
            1.  Evidenziare il record di utilizzo PSTN da modificare e fare clic su **Mostra dettagli**.
            
            2.  Utilizzare uno dei metodi seguenti per associare e configurare route per il record di utilizzo PSTN:
                
                  - Per scegliere una o più route da un elenco di tutte le route disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona**. Evidenziare le route da associare al record di utilizzo PSTN e quindi fare clic su **OK**.
                
                  - Per rimuovere una route dal record di utilizzo PSTN, evidenziarla e fare clic su **Rimuovi**.
                
                  - Per definire una nuova route e associarla al record di utilizzo PSTN, fare clic su **Nuovo**. Per informazioni dettagliate, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).
                
                  - Per modificare una route già associata al record di utilizzo PSTN, evidenziarla e fare clic su **Mostra dettagli**. Per informazioni dettagliate, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md).
            
            3.  Fare clic su **OK**.

11. (Facoltativo) Immettere un numero per testare il criteri vocale e quindi fare clic su **Vai**. I risultati del test vengono visualizzati in **Numero convertito da testare**.
    

    > [!NOTE]
    > È possibile salvare un criterio vocale che non passa ancora il test e quindi riconfigurarlo successivamente. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



12. Fare clic su **OK**.

13. Nella pagina **Criteri vocali** fare clic su **Commit** e quindi su **Salva tutto**.
    

    > [!NOTE]
    > Ogni volta che si crea o si modifica un criterio vocale, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



14. (Facoltativo) La funzionalità di escape della segreteria telefonica rileva la risposta immediata a una chiamata da parte della segreteria telefonica del cellulare dell'utente e disconnette la chiamata dalla segreteria telefonica. In questo modo la chiamata può continuare su altri endpoint dell'utente, in modo da offrirgli l'opportunità di rispondere. Per informazioni dettagliate su come configurare i criteri per la segreteria telefonica, vedere [Configurazione dell'escape della segreteria telefonica in Lync Server 2013](lync-server-2013-configuring-voice-mail-escape.md).

## Vedere anche

#### Attività

[Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)  
[Visualizzare record utilizzo PSTN in Lync Server 2013](lync-server-2013-view-pstn-usage-records.md)  
[Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md)  
[Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  
[Configurazione dell'escape della segreteria telefonica in Lync Server 2013](lync-server-2013-configuring-voice-mail-escape.md)  

#### Ulteriori risorse

[Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

