---
title: Creare una route vocale in Lync Server 2013
TOCTitle: Creare una route vocale in Lync Server 2013
ms:assetid: d189057d-cc9d-4622-9d10-f5385d703faf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398898(v=OCS.15)
ms:contentKeyID: 49302055
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare una route vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Nella procedura seguente viene illustrato come creare una nuova route vocale utilizzando il Pannello di controllo di Lync Server 2013. Per modificare una route esistente, vedere [Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md) per la procedura.

## Per creare una route vocale mediante il Pannello di controllo di Lync Server

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins o come membro del ruolo amministrativo **CsVoiceAdministrator**, **CsServerAdministrator** o **CsAdministrator**.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale**.

4.  Fare clic su **Route**.

5.  Fare clic su **Nuova** per visualizzare la finestra di dialogo **Route vocale**.

6.  In **Nome** digitare un nome descrittivo per la route vocale.

7.  (Facoltativo) In **Descrizione** digitare altre informazioni descrittive per la route vocale.

8.  Per specificare i formati che devono essere supportati dalla route, è possibile utilizzare lo strumento **Crea formato di cui creare una corrispondenza** per generare un'espressione regolare oppure scrivere tale espressione manualmente.
    
      - Per utilizzare lo strumento **Crea formato di cui creare una corrispondenza** per generare un'espressione regolare, immettere i valori come indicato di seguito. È possibile specificare due tipi di corrispondenze di formato:
        
          - **Cifre iniziali per i numeri da consentire:** immettere i valori di prefisso che la route deve supportare, incluso il segno + iniziale, se necessario. Digitare ad esempio **+425** e quindi fare clic su **Aggiungi**. Ripetere questa operazione per ogni valore di prefisso da includere nella route.
        
          - **Eccezioni:** se si desidera specificare una o più eccezioni per un valore di prefisso, evidenziare il prefisso e fare clic su **Eccezioni**. Digitare uno o più valori per i formati di corrispondenza che la route *non* deve includere. Per escludere ad esempio i numeri che iniziano con +425237 dalla route, immettere il valore **+425237** nel campo **Eccezioni** e quindi fare clic su **OK**.
    
      - Per definire manualmente il formato di corrispondenza, fare clic su **Modifica** nello strumento **Crea formato di cui creare una corrispondenza** e quindi digitare un'espressione regolare .NET Framework per specificare il formato di corrispondenza per i numeri di telefono di destinazione ai quali viene applicata la route. Per informazioni dettagliate su come scrivere le espressioni regolari, vedere "Espressioni regolari di .NET Framework" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=140927\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=140927%26clcid=0x410).

9.  Selezionare **Ometti ID chiamante** se non si desidera che l'ID del telefono che effettua la chiamata in uscita venga visualizzato al destinatario della chiamata. Se si seleziona questa opzione, è necessario specificare un **ID chiamante alternativo** che verrà visualizzato sullo schermo dell'ID chiamante del destinatario.

10. Per associare uno o più trunk alla route vocale, fare clic su **Aggiungi** e quindi selezionare un trunk nell'elenco.
    

    > [!NOTE]
    > Se la distribuzione include Mediation Server di Microsoft Office Communications Server 2007 R2, saranno anch'essi disponibili nell'elenco.



11. Per associare uno o più utilizzi PSTN (Public Switched Telephone Network) alla route vocale, fare clic su **Seleziona** e scegliere un record nell'elenco di record di utilizzo PSTN definiti per la distribuzione di VoIP aziendale.
    

    > [!NOTE]
    > Per visualizzare le proprietà di ognuno dei record di utilizzo PSTN disponibili, vedere <A href="lync-server-2013-view-pstn-usage-records.md">Visualizzare record utilizzo PSTN in Lync Server 2013</A>.<BR>Per creare o modificare record di utilizzo PSTN, vedere <A href="lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md">Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013</A> o <A href="lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md">Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013</A>.



12. Disporre i record di utilizzo PSTN in modo da garantire prestazioni ottimali. Per modificare la posizione di un record nell'elenco, evidenziare il nome del record e fare clic sulla freccia su o giù.
    

    > [!NOTE]
    > Diversamente dai criteri vocali, in cui l'ordine con cui sono elencati i record di utilizzo PSTN è importante, nella route vocale lo stesso ordine è irrilevante. È tuttavia consigliabile organizzare l'elenco per frequenza di utilizzo, ad esempio: RedmondLocal, RedmondLongDist, RedmondInternational, RedmondBackup (Lync Server scorre l'elenco dall'alto verso il basso).



13. (Facoltativo) Digitare un valore nel campo **Numero convertito da testare** e fare clic su **Vai**. I risultati del test vengono visualizzati nel campo.
    

    > [!NOTE]
    > È possibile salvare una route vocale che non passa ancora il test e quindi riconfigurarla successivamente. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



14. Fare clic su **OK** per salvare la route vocale.

> [!IMPORTANT]  
> Ogni volta che si crea una route vocale, è necessario eseguire il comando <strong>Salva tutto</strong> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <a href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</a>.

## Vedere anche

#### Attività

[Modificare una route vocale in Lync Server 2013](lync-server-2013-modify-a-voice-route.md)  
[Visualizzare record utilizzo PSTN in Lync Server 2013](lync-server-2013-view-pstn-usage-records.md)  
[Creare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-create-a-voice-policy-and-configure-pstn-usage-records.md)  
[Modificare criteri vocali e configurare record utilizzo PSTN in Lync Server 2013](lync-server-2013-modify-a-voice-policy-and-configure-pstn-usage-records.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Ulteriori risorse

[Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

