---
title: Modificare una route vocale in Lync Server 2013
TOCTitle: Modificare una route vocale in Lync Server 2013
ms:assetid: afc562cc-8807-489b-8850-dbbe1c1ab9f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412838(v=OCS.15)
ms:contentKeyID: 49301665
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare una route vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

In questo argomento viene illustrato come modificare una route vocale. Per creare una nuova route, vedere [Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md).

## Per modificare una route vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Route**.

4.  Nella pagina **Route** utilizzare uno dei metodi seguenti per modificare una route vocale:
    
      - Fare clic sul nome di una route vocale, fare clic su **Modifica**, quindi su **Mostra dettagli**.
    
      - Fare clic sul nome di una route vocale, fare clic su **Modifica**, su **Copia**, quindi su **Incolla**. Fare clic sulla nuova copia della route vocale appena creata, fare clic su **Modifica**, quindi su **Mostra dettagli**.

5.  Nel campo **Nome** della pagina **Modifica route vocale** digitare un nome descrittivo per la route vocale.

6.  Nel campo **Descrizione** digitare altre informazioni descrittive per la route vocale (facoltativo).

7.  Per specificare i formati che questa route deve includere, è possibile utilizzare lo strumento **Formato per corrispondenza** per generare un'espressione regolare oppure scrivere tale espressione manualmente.
    
      - Per utilizzare lo strumento **Formato per corrispondenza** per generare un'espressione regolare, immettere i valori come indicato di seguito. È possibile specificare due tipi di corrispondenze di formato:
        
          - **Cifre iniziali per i numeri da consentire:** immettere i valori di prefisso che la route deve includere, incluso il segno + iniziale, se necessario. Digitare, ad esempio, **+425** e quindi fare clic su **Aggiungi**. Ripetere questa operazione per ogni valore di prefisso da includere nella route.
        
          - **Eccezioni:** se si desidera specificare una o più eccezioni per un valore di prefisso, evidenziare il prefisso e fare clic su **Eccezioni**. Digitare uno o più valori per i formati di corrispondenza che la route *non* deve includere. Per escludere ad esempio i numeri che iniziano con +425237 dalla route, immettere il valore **+425237** nel campo **Eccezioni** e quindi fare clic su **OK**.
    
      - Per definire manualmente il formato di corrispondenza, fare clic su **Modifica** nello strumento **Formato per corrispondenza** e quindi digitare un'espressione regolare .NET Framework per specificare il formato di corrispondenza per i numeri di telefono di destinazione ai quali viene applicata la route. Per informazioni su come scrivere le espressioni regolari, vedere "Espressioni regolari di .NET Framework" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=140927\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=140927%26clcid=0x410).

8.  Selezionare **Ometti ID chiamante** se non si desidera che l'ID del telefono che effettua la chiamata in uscita venga visualizzato al destinatario della chiamata. Se si seleziona questa opzione, è necessario specificare un **ID chiamante alternativo** che comparirà nella visualizzazione dell'ID chiamante del destinatario.

9.  Per associare uno o più trunk PSTN (Public Switched Telephone Network) alla route vocale, fare clic su **Aggiungi** e quindi selezionare un trunk nell'elenco.
    

    > [!NOTE]
    > Se la distribuzione include Mediation Server di Microsoft Office Communications Server 2007 R2, saranno anch'essi disponibili nell'elenco.



10. Per associare uno o più utilizzi PSTN alla route vocale, fare clic su **Seleziona** e selezionare un record nell'elenco di record di utilizzo PSTN definiti per la distribuzione di VoIP aziendale.
    

    > [!NOTE]
    > Per visualizzare le proprietà di ognuno dei record di utilizzo PSTN disponibili, vedere <A href="lync-server-2013-view-pstn-usage-records.md">Visualizzare record utilizzo PSTN in Lync Server 2013</A>.<BR>Per creare o modificare record di utilizzo PSTN, vedere <A href="lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md">Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013</A> o <A href="lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md">Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013</A>.



11. Disporre i record di utilizzo PSTN in modo da garantire prestazioni ottimali. Per modificare la posizione di un record nell'elenco, evidenziare il nome del record e fare clic sulla freccia su o giù.
    

    > [!NOTE]
    > Diversamente dai criteri vocali in cui l'ordine in cui sono elencati i record di utilizzo PSTN è importante, in una route vocale l'ordine dei record di utilizzo PSTN è irrilevante. È tuttavia consigliabile organizzare l'elenco per frequenza di utilizzo, ad esempio: RedmondLocal, RedmondLongDist, RedmondInternational, RedmondBackup. Lync Server scorre l'elenco dall'alto verso il basso.



12. Digitare un valore nel campo **Numero convertito da testare** e fare clic su **Vai**. I risultati del test vengono visualizzati nel campo (facoltativo).
    

    > [!NOTE]
    > È possibile salvare una route vocale che non passa ancora il test e quindi riconfigurarla successivamente. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



13. Fare clic su **OK**.

14. Nella pagina **Route** fare clic su **Commit** e quindi su **Salva tutto**.
    

    > [!NOTE]
    > Ogni volta che si crea o modifica una route vocale, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Creare una route vocale in Lync Server 2013](lync-server-2013-create-a-voice-route.md)  
[Visualizzare record utilizzo PSTN in Lync Server 2013](lync-server-2013-view-pstn-usage-records.md)  
[Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Ulteriori risorse

[Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

