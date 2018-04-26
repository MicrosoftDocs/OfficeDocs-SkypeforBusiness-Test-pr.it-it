---
title: Eseguire test informali del routing vocale in Lync Server 2013
TOCTitle: Eseguire test informali del routing vocale in Lync Server 2013
ms:assetid: ea0e6059-bf04-4b03-b6d3-8f5534b731e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399049(v=OCS.15)
ms:contentKeyID: 49302336
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire test informali del routing vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-07_

È possibile utilizzare la finestra di dialogo **Crea informazioni test case routing vocale** per eseguire test informativi prima di creare un test case vero e proprio. Quando si è soddisfatti del risultato di un test, è possibile salvarlo come test case formale.

## Per eseguire un test informale del routing vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Test routing vocale**.

4.  Nella pagina **Test routing vocale** fare clic su **Crea informazioni test case routing vocale**.

5.  Nel campo **Numero composto** digitare il numero di telefono da utilizzare per il test. Questo numero verrà normalizzato e visualizzato nel campo **Numero normalizzato** del riquadro **Risultati**.

6.  Nell'elenco **Dial plan** selezionare il dial plan da utilizzare per il test del numero composto. Per impostazione predefinita viene utilizzato il dial plan globale.
    
    Quando si esegue il test, la prima regola di normalizzazione del dial plan che corrisponde al numero composto verrà visualizzata nel campo **Regola di normalizzazione** del riquadro **Risultati**.

7.  Nell'elenco **Criteri vocali** selezionare i criteri vocali da utilizzare per il test del numero composto. Per impostazione predefinita vengono utilizzati i criteri vocali globali.
    
    Quando si esegue il test, il primo record di utilizzo PSTN dei criteri vocali verrà visualizzato nel campo **Primo utilizzo PSTN** del riquadro **Risultati**. Inoltre, la prima route vocale corrispondente associata a questo record di utilizzo PSTN verrà visualizzata nel campo **Prima route**.

8.  (Facoltativo) Selezionare la casella di controllo **Popola da utente** se si desidera testare il numero composto rispetto ai criteri vocali assegnati a un determinato utente.
    
    1.  Fare clic su **Sfoglia** per visualizzare la finestra di dialogo **Seleziona utenti VoIP aziendale**.
    
    2.  Fare clic su **Trova** per visualizzare l'elenco di utenti abilitati per VoIP aziendale.
    
    3.  Fare doppio clic dell'utente a cui sono assegnati i criteri vocali da utilizzare per il test. Il campo **Criteri** viene ora popolato con i criteri vocali assegnati all'utente selezionato.
    
    Quando si esegue il test, il primo record di utilizzo PSTN (Public Switched Telephone Network) dei criteri vocali corrispondente verrà visualizzato nel campo **Primo utilizzo PSTN** del riquadro **Risultati**. Inoltre, la prima route vocale corrispondente associata a questo record di utilizzo PSTN verrà visualizzata nel campo **Prima route**.

9.  Fare clic su **Esegui** per eseguire il test case. I risultati verranno visualizzati nel pannello destro della finestra di dialogo.

10. (Facoltativo) Fare clic su **Salva con nome** se si desidera salvare questa configurazione di test come test case formale.
    
    1.  Nel campo **Nome** della finestra di dialogo **Salva informazioni test case routing vocale** digitare un nome univoco per il test case.
        
        Il nome deve essere univoco in tutti i test case di routing vocale nella distribuzione di VoIP aziendale. Può essere composto da un massimo di 32 caratteri alfanumerici, oltre alla barra rovesciata (\\), al punto (.) o al carattere di sottolineatura (\_).
    
    2.  Si noti che i campi rimanenti della finestra di dialogo **Salva informazioni test case routing vocale** sono di sola lettura e vengono compilati preventivamente dai risultati *e* dalla configurazione di test informale. Verificare che la configurazione sia quella che si desidera salvare per il test case.
        

        > [!NOTE]
        > I valori dei risultati vengono utilizzati per prepopolare i campi nella finestra di dialogo <STRONG>Salva informazioni test case routing vocale</STRONG> come indicato di seguito: 
        > <UL>
        > <LI>
        > <P>Il campo <STRONG>Conversione prevista</STRONG> è prepopolato con il valore del campo <STRONG>Numero normalizzato</STRONG>.</P>
        > <LI>
        > <P>Il campo <STRONG>Route prevista</STRONG> è prepopolato con il valore del campo <STRONG>Prima route</STRONG>.</P>
        > <LI>
        > <P>Il campo <STRONG>Utilizzo PSTN previsto</STRONG> è prepopolato con il valore del campo <STRONG>Primo utilizzo PSTN</STRONG>.</P></LI></UL>Se durante l'esecuzione del test non vengono trovate corrispondenze per uno di questi valori, il campo corrispondente sarà vuoto nella finestra di dialogo <STRONG>Salva informazioni test case routing vocale</STRONG>.

    
    3.  Fare clic su **OK** per salvare il test case oppure su **Annulla** per tornare alla finestra di dialogo **Crea informazioni test case routing vocale** per sviluppare ulteriormente il test prima di salvarlo.

11. Fare clic su **Commit** e quindi su **Salva tutto**.
    

    > [!NOTE]
    > Ogni volta che si crea un test case di routing vocale, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicarlo. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Creare un test case di routing vocale in Lync Server 2013](lync-server-2013-create-a-voice-routing-test-case.md)  
[Eseguire test case di routing vocale in Lync Server 2013](lync-server-2013-run-voice-routing-test-cases.md)  
[Esportare test case di routing vocale in Lync Server 2013](lync-server-2013-export-voice-routing-test-cases.md)  
[Importare test case di routing vocale in Lync Server 2013](lync-server-2013-import-voice-routing-test-cases.md)  

#### Ulteriori risorse

[Configurazione dei dial plan in Lync Server 2013](lync-server-2013-configuring-dial-plans.md)  
[Configurazione di criteri vocali, record di utilizzo PSTN e route vocali in Lync Server 2013](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

