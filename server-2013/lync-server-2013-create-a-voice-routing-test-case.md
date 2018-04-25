---
title: 'Lync Server 2013: Creare un test case di routing vocale'
TOCTitle: Creare un test case di routing vocale
ms:assetid: 43a07a5b-2f20-462a-81e5-d628c18391e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425935(v=OCS.15)
ms:contentKeyID: 49300370
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un test case di routing vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-07_

## Per creare un test case

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Test routing vocale** .

4.  Nella pagina **Test routing vocale** fare clic su **Nuovo** per creare un nuovo test case.

5.  Nel campo **Nome** digitare un nome univoco per il test case.
    
    Il nome deve essere univoco nell'ambito di tutti i test case di routing vocale nella distribuzione di VoIP aziendale. La lunghezza massima consentita è 32 caratteri e possono essere inclusi tutti i caratteri alfanumerici oltre alla barra rovesciata (\\), al punto (.) o al carattere di sottolineatura (\_).

6.  Nel campo **Numero composto da testare** digitare il numero composto che si desidera utilizzare per testare la configurazione di routing specificata per il test case. A seconda del dial plan, della route e del criterio vocale, questo numero verrà normalizzato e visualizzato come output.

7.  Nell'elenco **Dial plan** selezionare il dial plan da utilizzare per eseguire il test. Il dial pan predefinito è quello globale.

8.  Nell'elenco **Criteri vocali** selezionare il criterio vocale da utilizzare per eseguire il test. Il criterio vocale predefinito è quello globale.

9.  Nel campo **Conversione prevista** digitare il numero di telefono nel formato previsto dopo la conversione. Questo è il valore del numero di telefono che si desidera testare, dopo la conversione da parte della prima regola di normalizzazione corrispondente nel dial plan selezionato. Se, quando si esegue il test case, il numero che si desidera testare non viene convertito nel valore riportato nel campo **Conversione prevista** , il test ha esito negativo.

10. (Facoltativo) Nell'elenco **Utilizzo PSTN previsto** è possibile selezionare il record di utilizzo PSTN (Public Switched Telephone Network) che si prevede venga utilizzato quando si esegue il test case, a seconda del dial plan e del criterio vocale selezionati. Se viene utilizzato un record di utilizzo PSTN diverso, il test ha esito negativo.

11. (Facoltativo) Nell'elenco **Route prevista** è possibile selezionare la route vocale che si prevede venga utilizzata quando si esegue il test case, a seconda del dial plan e del criterio vocale selezionati. Se viene utilizzata una route vocale diversa, il test ha esito negativo.

12. (Facoltativo) Fare clic su **Esegui** per eseguire il test case. I risultati verranno visualizzati nel riquadro destro della pagina.

13. Fare clic su **OK** .

14. Fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si crea un test case di routing vocale, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.

    
    Se il dial plan in uso nel test normalizza i numeri di telefono che iniziano con un segno più (+), ad esempio +12065551219, è possibile che il test del routing vocale non riesca. Il dial plan e la route vocale funzioneranno, come dimostrato dalla corretta esecuzione di Test-CsDialPlan, tuttavia il test di routing vocale potrebbe non riuscire. Tenere presente questo problema durante i test delle route vocali.

## Vedere anche

#### Attività

[Esportare test case di routing vocale in Lync Server 2013](lync-server-2013-export-voice-routing-test-cases.md)  
[Importare test case di routing vocale in Lync Server 2013](lync-server-2013-import-voice-routing-test-cases.md)  

#### Ulteriori risorse

[Configurazione dei dial plan in Lync Server 2013](lync-server-2013-configuring-dial-plans.md)  
[Configurazione di criteri vocali, record di utilizzo PSTN e route vocali in Lync Server 2013](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

