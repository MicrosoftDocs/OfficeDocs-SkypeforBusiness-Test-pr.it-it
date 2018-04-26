---
title: Eseguire test case di routing vocale in Lync Server 2013
TOCTitle: Eseguire test case di routing vocale in Lync Server 2013
ms:assetid: fb4d32df-b9ea-4944-8cd7-a6102c78c465
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413068(v=OCS.15)
ms:contentKeyID: 49302549
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire test case di routing vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

È possibile eseguire tutti i test case nel gruppo di test case di routing vocale oppure eseguire uno o più test case selezionati.

## Per eseguire tutti i test case di routing vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Test routing vocale**.

4.  Nella pagina **Test routing vocale** fare clic su **Azione** e quindi su **Esegui tutti**.
    
    Lo stato superato o non superato di ogni test case viene visualizzato nella colonna **Superato/Non superato**. Se un test case non è ancora stato eseguito, nella colonna **Superato/Non superato** viene visualizzato N/D.

5.  (Facoltativo) Per visualizzare i risultati dettagliati per ogni test case, fare doppio clic sul nome del test case. I risultati verranno visualizzati nell'area ombreggiata sul lato destro della pagina **Modifica test case**:
    
    1.  **Risultati test:** stato generale superato o non superato del test case eseguito.
    
    2.  **Regola di normalizzazione:** la prima regola di normalizzazione nel dial plan selezionato per questo test case corrispondente al numero composto (valore nel campo **Numero da testare**).
    
    3.  **Numero normalizzato:** valore del numero composto dopo la conversione da parte della regola di normalizzazione.
    
    4.  **Primo utilizzo PSTN:** record del primo utilizzo di PSTN (Public Switched Telephone Network) nel criterio vocale selezionato per questo test corrispondente al numero composto.
    
    5.  **Prima route:** prima route vocale nel primo record di utilizzo di PSTN corrispondente al numero composto.
        

        > [!NOTE]
        > I campi <STRONG>Utilizzo PSTN previsto</STRONG> e <STRONG>Route prevista</STRONG> sono facoltativi nella configurazione del test case di routing vocale. Se il test case non specifica questi valori, il campo corrispondente nei risultati del test sarà vuoto.



## Per eseguire uno o più test case di routing vocale

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Test routing vocale**.

4.  Nella pagina **Test routing vocale** fare clic sui nomi dei test case che si desidera eseguire.

5.  Scegliere **Esegui selezionati** dal menu **Azione**.
    
    Lo stato superato o non superato di ogni test case viene visualizzato nella colonna **Superato/Non superato**. Se un test case non è ancora stato eseguito, nella colonna **Superato/Non superato** viene visualizzato N/D.

6.  (Facoltativo) Per visualizzare i risultati dettagliati per ogni test case, fare doppio clic sul nome del test case. I risultati verranno visualizzati nell'area ombreggiata sul lato destro della pagina **Modifica test case**:
    
    1.  **Risultati test:** stato generale superato o non superato del test case eseguito.
    
    2.  **Regola di normalizzazione:** la prima regola di normalizzazione nel dial plan selezionato per questo test case corrispondente al numero composto (valore nel campo **Numero da testare**).
    
    3.  **Numero normalizzato:** valore del numero composto dopo la conversione da parte della regola di normalizzazione.
    
    4.  **Primo utilizzo PSTN:** record del primo utilizzo di PSTN nel criterio vocale selezionato per questo test corrispondente al numero composto.
    
    5.  **Prima route:** prima route vocale nel primo record di utilizzo di PSTN corrispondente al numero composto.
        

        > [!NOTE]
        > I campi <STRONG>Utilizzo PSTN previsto</STRONG> e <STRONG>Route prevista</STRONG> sono facoltativi nella configurazione del test case di routing vocale. Se il test case non specifica questi valori, il campo corrispondente nei risultati del test sarà vuoto.



## Vedere anche

#### Ulteriori risorse

[Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)  
[Esecuzione di test del routing vocale in Lync Server 2013](lync-server-2013-running-voice-routing-tests.md)

