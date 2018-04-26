---
title: Creare o modificare manualmente una regola di conversione
TOCTitle: Creare o modificare manualmente una regola di conversione
ms:assetid: 049d1db3-af58-48c5-be89-52e1d068a4bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398099(v=OCS.15)
ms:contentKeyID: 49299538
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare manualmente una regola di conversione

 

_**Ultima modifica dell'argomento:** 2012-08-06_

Eseguire questa procedura se si desidera definire una regola di conversione scrivendo un'espressione regolare per il formato e la regola. In alternativa, è possibile immettere un insieme di valori nello strumento **Crea una regola di conversione** e lasciare che sia il Pannello di controllo di Lync Server a generare automaticamente il formato e la regola di conversione corrispondenti. Per informazioni dettagliate, vedere [Creare o modificare una regola di conversione utilizzando lo strumento Crea regola di conversione](lync-server-2013-create-or-modify-a-translation-rule-by-using-the-build-a-translation-rule-tool.md).

## Per definire manualmente una regola di conversione

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Per iniziare a definire una regola di conversione, eseguire la procedura descritta in [Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md) fino al passaggio 10 oppure la procedura descritta in [Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md) fino al passaggio 9.

4.  Nel campo **Nome** della pagina **Nuova regola di conversione** o **Modifica regola di conversione** digitare un nome che descriva il formato del numero da convertire.

5.  (Facoltativo) In **Descrizione** digitare una descrizione della regola di conversione, ad esempio **Chiamate internazionali Stati Uniti**.

6.  Fare clic su **Modifica** nella parte inferiore della sezione **Crea regola di conversione**.

7.  Immettere quanto segue in **Digita espressione regolare**:
    
      - In **Trova corrispondenza per questo formato** specificare il modello di formato da utilizzare per trovare corrispondenze con i numeri da convertire.
    
      - In **Regola di conversione** specificare un modello per il formato dei numeri convertiti.
    
    Ad esempio, se si immette **^\\+(\\d{9}\\d+)$** in **Trova corrispondenza per questo formato** e **011$1** in **Regola di conversione**, la regola convertirà +441235551010 in 011441235551010.

8.  Fare clic su **OK** per salvare la regola di conversione.

9.  Fare clic su **OK** per salvare la configurazione trunk.

10. Nella pagina **Configurazione trunk** fare clic su **Commit** e quindi su **Salva tutto**.
    

    > [!NOTE]
    > Ogni volta che si crea o modifica una regola di conversione, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica relativa alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Creare o modificare una regola di conversione utilizzando lo strumento Crea regola di conversione](lync-server-2013-create-or-modify-a-translation-rule-by-using-the-build-a-translation-rule-tool.md)  
[Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Concetti

[Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md)

