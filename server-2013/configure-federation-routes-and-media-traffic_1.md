---
title: Configurare le route di federazione e il traffico multimediale
TOCTitle: Configurare le route di federazione e il traffico multimediale
ms:assetid: ed6cb922-7863-453a-adce-2ce0ba761d74
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721925(v=OCS.15)
ms:contentKeyID: 49887812
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le route di federazione e il traffico multimediale

 

_**Ultima modifica dell'argomento:** 2012-10-16_

La federazione è una relazione di trust tra due o più domini SIP che consente a utenti di organizzazioni distinte di comunicare attraverso i confini della rete. Dopo aver eseguito la migrazione nel pool pilota di Lync Server 2013, è necessario compiere la transizione dalla route di federazione dei server perimetrali Microsoft Office Communications Server 2007 R2 alla route di federazione dei server perimetrali Lync Server 2013.

Utilizzare le procedure riportate di seguito per la transizione della route di federazione e della route del traffico multimediale dal server perimetrale e dal Director Office Communications Server 2007 R2 al server perimetrale Lync Server 2013, per una distribuzione a sito singolo.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per modificare la route di federazione e la route del traffico multimediale, è necessario pianificare un intervallo di tempo di inattività per la manutenzione per i server perimetrali di Lync Server 2013 e Office Communications Server 2007 R2. L'intero processo di transizione comporta inoltre la non disponibilità dell'accesso federato per tutta la durata dell'interruzione dei servizi. È consigliabile pianificare il tempo di inattività nel periodo di attività minima degli utenti e inviare una notifica agli utenti finali. Eseguire le pianificazioni tenendo conto di questo periodo di interruzione e definire previsioni appropriate nell'organizzazione.</td>
</tr>
</tbody>
</table>


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se il server perimetrale Office Communications Server 2007 R2 legacy è configurato per utilizzare lo stesso FQDN per i servizi Access Edge, Web Conferencing Edge e A/V Edge, le procedure in questa sezione per la transizione dell'impostazione di federazione a un server perimetrale Lync Server 2013 non sono supportate. Se i servizi perimetrali legacy sono configurati per utilizzare lo stesso FQDN, è necessario innanzitutto eseguire la migrazione di tutti gli utenti da Office Communications Server 2007 R2 a Lync Server 2013 e quindi rimuovere le autorizzazioni per il server perimetrale Office Communications Server 2007 R2 prima di abilitare la federazione nel server perimetrale Lync Server 2013. Per informazioni dettagliate, vedere gli argomenti seguenti:
<ul>
<li><p><a href="move-remaining-users-to-lync-server-2013_1.md">Spostare gli utenti rimanenti in Lync Server 2013</a></p></li>
<li><p>&quot;Rimozione di server e ruoli del server&quot; all'indirizzo <a href="http://go.microsoft.com/fwlink/p/?linkid=268790">http://go.microsoft.com/fwlink/p/?linkId=268790</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se la federazione XMPP è instradata attraverso un server perimetrale Lync Server 2013, gli utenti legacy di Office Communications Server 2007 R2 non potranno comunicare con il partner federato XMPP finché tutti gli utenti non saranno stati spostati in Lync Server 2013, i certificati e i criteri XMPP non saranno stati configurati, il partner federato XMPP non sarà stato configurato in Lync Server 2013 e le voci DNS non saranno state aggiornate.</td>
</tr>
</tbody>
</table>


Per pubblicare, abilitare o disabilitare correttamente una topologia quando si aggiunge o si rimuove un ruolo del server, è necessario aver eseguito l'accesso come utente membro dei gruppi RTCUniversalServerAdmins e Domain Admins. È inoltre possibile delegare le autorizzazioni e i diritti utente appropriati per l'aggiunta di ruoli del server. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md) nella documentazione relativa alla distribuzione di server Standard Edition o Enterprise Edition. Per poter apportare altre modifiche alla configurazione, è necessaria solo l'appartenenza al gruppo RTCUniversalServerAdmins.

## Per rimuovere l'associazione di federazione legacy dai siti di Lync Server 2013

1.  Aprire la topologia pool pilota utilizzando Generatore di topologie.

2.  Nel riquadro sinistro passare al nodo del sito.

3.  Fare clic con il pulsante destro del mouse sul sito e quindi scegliere **Modifica proprietà** .

4.  Selezionare **Route di federazione** nel riquadro sinistro.

5.  In Assegnazione route federazione sito deselezionare la casella di controllo accanto a **Abilita federazione SIP** per disabilitare la route di federazione tramite **BackCompatSite** .
    
    ![Finestra di dialogo Modifica proprietà - Route di federazione](images/JJ721925.2a80c103-c0cc-43ed-ba00-420f9add006a(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Route di federazione")

6.  Fare clic su **OK** per chiudere la pagina Modifica proprietà.

7.  In **Generatore di topologie** selezionare il nodo principale **Lync Server** .

8.  Nel menu **Azione** fare clic su **Pubblica topologia** e quindi completare la procedura guidata.

## Per configurare il server perimetrale legacy come server perimetrale non federato

1.  In **Generatore di tipologie** scegliere **Unisci la topologia Office Communications Server 2007 R2** dal menu **Azione** .

2.  Fare clic su **Avanti** per continuare.

3.  In **Specificare installazione server perimetrale** selezionare l' **FQDN interno del server perimetrale** attualmente configurato per la federazione e quindi fare clic su **Cambia** .
    
    ![Unisci topologia 2007 R2 - Specificare installazione server perimetrale](images/JJ721925.42c15aaf-c1ac-4fb1-a086-665835c57b23(OCS.15).jpg "Unisci topologia 2007 R2 - Specificare installazione server perimetrale")

4.  Fare clic su **Avanti** e accettare le impostazioni predefinite finché non viene visualizzata la pagina **Specificare il perimetro esterno** :
    
    ![Pagina Specificare il perimetro esterno in Generatore di topologie](images/JJ205243.32e97ce5-92f0-477e-8125-5d2ece237b13(OCS.15).jpg "Pagina Specificare il perimetro esterno in Generatore di topologie")

5.  In **Specificare il perimetro esterno** deselezionare la casella di controllo **Questo pool di server perimetrali è utilizzato per la federazione e la connettività di messaggistica istantanea pubblica** . In questo modo verrà rimossa l'associazione di federazione con BackCompatSite.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Questo passaggio è importante. È necessario deselezionare questa opzione per rimuovere l'associazione di federazione legacy.</td>
    </tr>
    </tbody>
    </table>


6.  Fare clic su **Avanti** e accettare le impostazioni predefinite delle pagine rimanenti della procedura guidata.

7.  In **Riepilogo** fare clic su **Avanti** per iniziare a unire le topologie.

8.  Nella colonna **Stato** verificare che sia riportato il valore **Esito positivo** e quindi fare clic su **Fine** per chiudere la procedura guidata.

9.  Scegliere **Pubblica topologia** dal menu **Azione** e quindi fare clic su **Avanti** .

10. Al termine della **Pubblicazione guidata** , fare clic su **Fine** per chiudere la procedura guidata.
    
    ![Generatore di topologie con sito visualizzato dopo l'unione](images/JJ721925.92b679ad-332f-49aa-b4e2-19f939b711ca(OCS.15).jpg "Generatore di topologie con sito visualizzato dopo l'unione")
    
    Come illustrato nella figura precedente, la **federazione SIP** presente in **Assegnazione route federazione sito** è impostata su **Disabilitata**.

## Per configurare i certificati nel server perimetrale Lync Server 2013

1.  Esportare il certificato esterno del proxy di accesso con la chiave privata dal server perimetrale Office Communications Server 2007 R2 legacy.

2.  Nel server perimetrale Lync Server 2013 importare il certificato esterno del proxy di accesso esportato nel passaggio precedente.

3.  Assegnare il certificato esterno del proxy di accesso all'interfaccia esterna Lync Server 2013 del server perimetrale.

4.  Il certificato dell'interfaccia interna del server perimetrale Lync Server 2013 non deve essere modificato.

## Per modificare la route di federazione di Office Communications Server 2007 R2 per l'utilizzo del server perimetrale Lync Server 2013

1.  Nel server Standard Edition o nel Front End Server di Office Communications Server 2007 R2 aprire lo strumento di amministrazione di Office Communications Server 2007 R2.

2.  Nel riquadro sinistro espandere il nodo principale e quindi fare clic con il pulsante destro del mouse sul nodo **Foresta** . Scegliere **Proprietà** e quindi fare clic su **Proprietà globali** .

3.  Fare clic sulla scheda **Federazione** .

4.  Selezionare la casella di controllo per abilitare la federazione e la connettività per messaggistica istantanea pubblica.

5.  Immettere l'FQDN del server perimetraleLync Server 2013 e quindi fare clic su **OK** .
    
    ![Proprietà globali di Office Communications Server - Scheda Federazione](images/JJ721925.da633f72-43c6-4dac-8d37-ccd0dcde79c9(OCS.15).jpg "Proprietà globali di Office Communications Server - Scheda Federazione")

## Per attivare la federazione del server perimetrale Lync Server 2013

1.  Nel riquadro sinistro di Generatore di topologie passare al nodo **Pool di server perimetrali** Lync Server 2013.

2.  Espandere il nodo, fare clic con il pulsante destro del mouse sul server perimetrale elencato e quindi scegliere **Modifica proprietà** .
    

    > [!NOTE]
    > È possibile abilitare la federazione solo per un singolo pool di server perimetrali. Se si dispone di più pool di server perimetrali, selezionarne uno da utilizzare come pool di server perimetrali federativo.



3.  Nella pagina **Generale** selezionare la casella di controllo **Abilita federazione per pool di server perimetrali (porta 5061)** .
    
    ![Modifica proprietà, Generale - Abilitazione della federazione perimetrale](images/JJ688121.cc79a88c-cce4-4cab-80ad-4f70325dc7c4(OCS.15).jpg "Modifica proprietà, Generale - Abilitazione della federazione perimetrale")

4.  Fare clic su **OK** per chiudere la pagina Modifica proprietà.

5.  Passare quindi al nodo del sito.

6.  Fare clic con il pulsante destro del mouse sul sito e quindi scegliere **Modifica proprietà** .

7.  Nel riquadro sinistro fare clic su **Route di federazione** .

8.  In **Assegnazione route federazione sito** selezionare **Abilita federazione SIP** e quindi nell'elenco selezionare il server perimetraleLync Server 2013 elencato.

9.  Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .
    
    ![Modifica proprietà, Generale - Associa pool di server perimetrali](images/JJ721925.33d43297-10cd-412e-bf4a-a1d9a84b9009(OCS.15).jpg "Modifica proprietà, Generale - Associa pool di server perimetrali")
    
    Nel caso di distribuzioni multisito, eseguire questa procedura in ogni sito.

## Per configurare il percorso del contenuto multimediale in uscita dei server perimetrali Lync Server 2013

1.  In **Generatore di topologie** passare al pool di Lync Server 2013 sotto **Standard Edition Front End Server** o **Pool Enterprise Edition Front End** .

2.  Fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

3.  Nella sezione **Associazioni** selezionare la casella di controllo **Associa pool di server perimetrali (per componenti multimediali)** .

4.  Nell'elenco a discesa selezionare il server perimetrale Lync Server 2013.
    
    ![Finestra di dialogo Modifica proprietà - Associa pool di server perimetrali](images/JJ721925.0cb76b08-5923-4972-8d7a-a829cb77136b(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Associa pool di server perimetrali")

5.  Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .

## Per pubblicare le modifiche di configurazione del server perimetrale

1.  In **Generatore di topologie** selezionare il nodo principale **Lync Server** .

2.  Scegliere **Pubblica topologia** dal menu **Azione** e quindi completare la procedura guidata.

3.  Attendere il completamento della replica di Active Directory in tutti i pool della distribuzione.
    

    > [!NOTE]
    > Potrebbe essere visualizzato il messaggio seguente:<BR><STRONG>Avviso: la topologia contiene più di un server perimetrale federato. Questa situazione può verificarsi durante la migrazione a una versione successiva del prodotto. In questo caso, per la federazione viene utilizzato attivamente un solo server perimetrale. Verificare che il record SRV DNS punti al server perimetrale corretto. Se si desidera distribuire più server perimetrali federati in modo che siano attivi contemporaneamente (ovvero non in uno scenario di migrazione), verificare che tutti i partner federati utilizzino Office Communications Server 2007 R2 o versione successiva e che il record SRV DNS esterno elenchi tutti i server perimetrali abilitati per la federazione.</STRONG><BR>Si tratta di un avviso previsto che può essere tranquillamente ignorato.



## Per verificare la federazione e l'accesso remoto per gli utenti esterni

1.  In Lync Server 2013 Front End Server aprire Lync Server Management Shell.

2.  Per verificare lo stato della federazione e dell'accesso remoto, digitare dalla riga di comando quanto segue:
    
        Get-CsAccessEdgeConfiguration

3.  Per abilitare la federazione e l'accesso remoto, digitare dalla riga di comando quanto segue:
    
        Set-CsAccessEdgeConfiguration
    
    Per ulteriori informazioni su questi cmdlet, vedere gli argomenti seguenti: [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md) e [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md).

4.  Attendere il completamento della replica prima di portare i server perimetrali Lync Server 2013 online e testare la federazione e l'accesso esterno.

## Per configurare il server perimetrale Lync Server 2013

1.  Portare online tutti i server perimetrali Lync Server 2013.

2.  Aggiornare le regole di routing del firewall esterno o le impostazioni del dispositivo di bilanciamento del carico hardware in modo da inviare il traffico SIP per l'accesso esterno (solitamente, porta 443) e la federazione (in genere, porta 5061) al server perimetraleLync Server 2013, anziché al server perimetrale legacy.
    

    > [!NOTE]
    > Se non si dispone di un servizio di bilanciamento del carico hardware, è necessario aggiornare il record DNS A per la federazione in modo che rimandi al nuovo server Lync Server Access Edge. Per eseguire questa operazione con il minimo impatto sul servizio, ridurre il valore TTL dell'FQDN del Lync Server Access Edge esterno in modo che quando il DNS viene aggiornato per puntare al nuovo server Lync Server Access Edge, la federazione e l'accesso remoto vengono aggiornati rapidamente.



3.  Arrestare quindi **Lync Server Access Edge** in ogni computer server perimetrale.

4.  In ogni computer server perimetrale legacy aprire l'applet **Servizi** in **Strumenti di amministrazione** .

5.  Nell'elenco dei servizi individuare **Office Communications Server Access Edge** .

6.  Fare clic con il pulsante destro del mouse sul nome del servizio e quindi scegliere **Arresta** per arrestare il servizio.

7.  Impostare il tipo di avvio su **Disabilitato** .

8.  Fare clic su **OK** per chiudere la finestra **Proprietà** .

## Per testare la connettività degli utenti esterni e dell'accesso esterno

  - Utenti di almeno un dominio federato, un utente interno in Lync Server 2013 e un utente in Office Communications Server 2007 R2. Testare la messaggistica istantanea, il traffico audio/video e la condivisione del desktop.

  - Utenti di ogni provider di servizi di messaggistica istantanea supportato dall'organizzazione (e per cui sia stato completato il provisioning) che comunicano con un utente in Lync Server 2013 e un utente in Office Communications Server 2007 R2.

  - Verificare che gli utenti anonimi siano in grado di partecipare alle conferenze.

  - Utente ospitato in Office Communications Server 2007 R2 che utilizza accesso utente remoto (accedendo a Office Communications Server 2007 R2 dall'esterno della rete Intranet ma senza VPN) con un utente in Lync Server 2013 e un utente in Office Communications Server 2007 R2. Testare la messaggistica istantanea, la presenza, il traffico audio/video e la condivisione del desktop.

  - Utente ospitato in Lync Server 2013 che utilizza accesso utente remoto (accedendo a Lync Server 2013 dall'esterno della rete Intranet ma senza VPN) con un utente in Lync Server 2013 e un utente in Office Communications Server 2007 R2. Testare la messaggistica istantanea, la presenza, il traffico audio/video e la condivisione del desktop.

