---
title: 'Lync Server 2013: Creare o modificare manualmente una regola di normalizzazione'
TOCTitle: Creare o modificare manualmente una regola di normalizzazione
ms:assetid: fc0335e6-8830-4cfb-8c64-6aeb98c0a992
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413074(v=OCS.15)
ms:contentKeyID: 49302568
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare manualmente una regola di normalizzazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-22_

Effettuare le operazioni seguenti se si desidera creare o modificare manualmente una regola di normalizzazione. Se invece si desidera creare o modificare una regola di normalizzazione utilizzando Crea una regola di normalizzazione nel Pannello di controllo di Lync Server, vedere [Creare o modificare una regola di normalizzazione utilizzando Crea regola di normalizzazione in Lync Server 2013](lync-server-2013-create-or-modify-a-normalization-rule-by-using-build-a-normalization-rule.md).

## Per definire manualmente una regola di normalizzazione

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  (Facoltativo) Seguire la procedura in [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md) o [Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md).

4.  Nel campo **Nome** in **Nuova regola di normalizzazione** o **Modifica regola di normalizzazione** digitare un nome descrittivo del formato del numero da normalizzare (ad esempio, denominare la regola di normalizzazione **5DigitExtension** ).

5.  (Facoltativo) Nel campo **Descrizione** digitare una descrizione della regola di normalizzazione (ad esempio "Translates 5-digit extensions").

6.  In **Crea regola di normalizzazione** fare clic su **Modifica** .

7.  Immettere i valori seguenti in **Digita espressione regolare** :
    
      - In **Trova corrispondenza per questo formato** specificare il formato che si desidera utilizzare per individuare il numero di telefono composto.
    
      - In **Regola di conversione** specificare un formato per i numeri di telefono E.164 convertiti.
    
    Ad esempio, se si immette **^(\\d{7})$** in **Trova corrispondenza per questo formato** e **+1425$1** in **Regola di conversione** , la regola normalizza 5550100 in +14255550100.

8.  (Facoltativo) Se la regola di normalizzazione restituisce un numero di telefono interno all'organizzazione, selezionare **Estensione interna** .

9.  (Facoltativo) Immettere un numero per testare la regola di normalizzazione e quindi fare clic su **Vai** . I risultati del test verranno visualizzati in **Immettere numero da testare** .
    

    > [!NOTE]
    > È possibile salvare una regola di normalizzazione che non ha ancora superato il test e riconfigurarla successivamente. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



10. Fare clic su **OK** per salvare la regola di normalizzazione.

11. Fare clic su **OK** per salvare il dial plan.

12. Nella pagina **Dial plan** fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si crea o modifica una regola di normalizzazione, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Creare o modificare una regola di normalizzazione utilizzando Crea regola di normalizzazione in Lync Server 2013](lync-server-2013-create-or-modify-a-normalization-rule-by-using-build-a-normalization-rule.md)  
[Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md)  
[Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Ulteriori risorse

[Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

