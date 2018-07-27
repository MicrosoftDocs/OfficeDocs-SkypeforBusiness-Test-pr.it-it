---
title: Eseguire l'unione mediante la procedura di unione guidata di Generatore di topologie
TOCTitle: Eseguire l'unione mediante la procedura di unione guidata di Generatore di topologie
ms:assetid: c3f3c425-dab6-4dcd-bf0e-d7fde05f2ebf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205243(v=OCS.15)
ms:contentKeyID: 49301884
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire l'unione mediante la procedura di unione guidata di Generatore di topologie

 

_**Ultima modifica dell'argomento:** 2012-10-02_

1.  Eseguire il download della distribuzione esistente utilizzando Generatore di topologie.

2.  Scegliere **Unisci Office Communications Server 2007 R2** dal menu **Azione** .

3.  Fare clic su **Avanti** .

4.  In **Specificare installazione server perimetrale** fare clic su **Aggiungi** .
    
    ![Procedura guidata per l'unione delle topologie - Pagina Specificare installazione server perimetrale](images/JJ205243.cdca609d-d4d5-47d9-9ff8-8b1daa4106e1(OCS.15).jpg "Procedura guidata per l'unione delle topologie - Pagina Specificare installazione server perimetrale")  

5.  In **Specificare il tipo di server perimetrale** immettere il tipo di configurazione del server perimetrale e quindi fare clic su **Avanti** . In questo esempio viene utilizzata l'opzione **Server perimetrale singolo** .
    
    > [!IMPORTANT]  
    > <strong>Distribuzione server perimetrale espanso</strong> non è una configurazione supportata. Un <strong>Server perimetrale espanso</strong> deve essere prima convertito in un <strong>Server perimetrale singolo</strong> o in un <strong>Server perimetrale consolidato con carico bilanciato</strong> .

6.  In **Specificare le impostazioni del perimetro interno** immettere le informazioni necessarie per le porte e l'FQDN interno del pool di server perimetrali e quindi fare clic su **Avanti** .
    
    ![Finestra di dialogo Specificare le impostazioni del perimetro interno](images/JJ205243.dd664761-839c-4ac8-bd1a-5525589dfbb0(OCS.15).jpg "Finestra di dialogo Specificare le impostazioni del perimetro interno")  

7.  In **Specificare il perimetro esterno** immettere le informazioni relative all'FQDN di Web Conferencing per il server perimetrale.
    
    > [!IMPORTANT]  
    > Prima di fare clic su <strong>Avanti</strong> , eseguire il passaggio successivo di questa procedura. È molto importante non ignorare questo passaggio.

8.  Selezionare la casella di controllo **Questo pool di server perimetrali è utilizzato per la federazione e la connettività per messaggistica istantanea pubblica** se si intende utilizzare il server perimetrale Office Communications Server 2007 R2 legacy per la federazione. Se sono distribuiti più server perimetrali, solo uno di essi sarà abilitato per la federazione. Se non si seleziona questa casella di controllo e si decide successivamente di abilitare la federazione, sarà necessario eseguire l'unione guidata di Generatore di topologie e ripubblicare la topologia.
    
    ![Finestra di dialogo Server perimetrale - Pagina Specificare il perimetro esterno](images/JJ205243.32e97ce5-92f0-477e-8125-5d2ece237b13(OCS.15).jpg "Finestra di dialogo Server perimetrale - Pagina Specificare il perimetro esterno")  

9.  In **Specificare hop successivo** immettere il nome di dominio completo (FQDN) della posizione dell'hop successivo nell'ambiente. Fare clic su **Fine** .
    
    ![Finestra di dialogo Server perimetrale - Pagina Specificare hop successivo](images/JJ205243.e734ee0d-f91c-4f3f-8ae6-248ecabcf678(OCS.15).jpg "Finestra di dialogo Server perimetrale - Pagina Specificare hop successivo")  

10. Se sono stati aggiunti tutti i server perimetrali Office Communications Server 2007 R2, in **Specificare installazione server perimetrale** fare clic su **Avanti** . Se invece si desidera aggiungere ulteriori server perimetrali Office Communications Server 2007 R2, ripetere questa procedura a partire dal passaggio 4.

11. In **Specificare la porta SIP interna** selezionare l'impostazione predefinita, se non è stata modificata la porta SIP predefinita. Se invece non si sta utilizzando la porta predefinita 5061, modificare l'impostazione in base alle proprie esigenze e quindi fare clic su **Avanti** .

12. In **Riepilogo** fare clic su **Avanti** per iniziare a unire le topologie.

13. Nella pagina della procedura guidata viene confermato l'esito positivo dell'unione delle topologie.

14. Nella colonna **Stato** verificare che il valore sia **Esito positivo** e quindi fare clic su **Fine** .

15. Nel riquadro sinistro di Generatore di topologie ora dovrebbe essere visualizzato **BackCompatSite** , che indica che l'ambiente Office Communications Server 2007 R2 è stato unito a Lync Server 2013.
    
    ![Unione di topologie visualizzata nel Generatore di topologie](images/JJ205243.62751c76-f018-4c6d-bb48-c61ef8974d31(OCS.15).jpg "Unione di topologie visualizzata nel Generatore di topologie")  

16. Scegliere **Pubblica topologia** dal menu **Azione** e quindi fare clic su **Avanti** .

17. Al termine della Pubblicazione guidata fare clic su **Fine** .
    

    > [!NOTE]
    > È importante eseguire la procedura descritta nell'argomento successivo, <A href="import-policies-and-settings.md">Importare criteri e impostazioni</A>, per assicurarsi che le impostazioni dei criteri legacy vengano importate in Lync Server 2013.


