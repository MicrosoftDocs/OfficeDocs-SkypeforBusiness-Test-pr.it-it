---
title: Creare o modificare una regola di conversione utilizzando lo strumento Crea regola di conversione
TOCTitle: Creare o modificare una regola di conversione utilizzando lo strumento Crea regola di conversione
ms:assetid: ba112df8-3bb4-48e4-a353-4bf9110ccd71
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412909(v=OCS.15)
ms:contentKeyID: 49301778
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una regola di conversione utilizzando lo strumento Crea regola di conversione

 

_**Ultima modifica dell'argomento:** 2012-10-05_

Eseguire questa procedura se si desidera definire una regola di conversione immettendo un insieme di valori nello strumento **Crea una regola di conversione** e consentendo al Pannello di controllo di Lync Server di generare automaticamente il formato e la regola di conversione corrispondenti. In alternativa, è possibile scrivere manualmente un'espressione regolare per definire il formato e la regola di conversione corrispondenti. Per informazioni dettagliate, vedere [Creare o modificare manualmente una regola di conversione](lync-server-2013-create-or-modify-a-translation-rule-manually.md).

## Per definire una regola tramite lo strumento Crea regola di conversione

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Per iniziare a definire una regola di conversione, eseguire la procedura in [Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md) fino al passaggio 10 oppure in [Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md) fino al passaggio 9.

4.  In **Nome** nella pagina **Nuova regola di conversione** o **Modifica regola di conversione** digitare un nome descrittivo del formato del numero da convertire.

5.  (Facoltativo) In **Descrizione** digitare una descrizione della regola di conversione, ad esempio **Chiamate interurbane internazionali**.

6.  Nella sezione **Crea regola di conversione** della finestra di dialogo immettere i valore nei campi seguenti:
    
      - **Cifre iniziali**: (facoltativo) specificare le cifre iniziali dei numeri a cui si desidera corrisponda il formato. Ad esempio, immettere **+** in questo campo per specificare una corrispondenza con i numeri nel formato E.164, che iniziano con +.
    
      - **Lunghezza**: specificare il numero di cifre nel formato e specificare se si desidera applicare il formato ai numeri esattamente di questa lunghezza, almeno di questa lunghezza o di qualsiasi lunghezza. Ad esempio, immettere **11** e selezionare **Almeno** nell'elenco a discesa per specificare una corrispondenza con i numeri con una lunghezza di almeno 11 cifre.
    
      - **Cifre da rimuovere**: (facoltativo) specificare il numero di cifre iniziali da rimuovere. Ad esempio, immettere **1** per rimuovere il **+** all'inizio del numero.
    
      - **Prefisso**: (facoltativo) specificare le cifre da aggiungere all'inizio dei numeri convertiti. Ad esempio, immettere **011** se si desidera aggiungere 011 all'inizio dei numeri convertiti quando si applica questa regola.
    
    I valori immessi in questi campi vengono riportati nei campi **Formato per corrispondenza** e **Regola di conversione**. Se si specificano i valori di esempio precedenti, ad esempio, l'espressione regolare risultante nel campo **Formato per corrispondenza** sarà:
    
    **^\\+(\\d{9}\\d+)$**
    
    Nel campo **Regola di conversione** specificare un modello per il formato dei numeri convertiti. Il modello è composto da due parti:
    
      - Un valore (ad esempio **$1**) che rappresenta il numero di cifre nel formato corrispondente
    
      - (Facoltativo) Un valore che è possibile aggiungere all'inizio del numero immettendolo nel campo **Prefisso**
    
    In base ai valori di esempio precedenti, nel campo **Regola di conversione** viene visualizzato **011$1**.
    
    Con l'applicazione di questa regola di conversione il numero +441235551010 diventa 011441235551010.

7.  Fare clic su **OK** per salvare la regola di conversione.

8.  Fare clic su **OK** per salvare la configurazione del trunk.

9.  Nella pagina **Configurazione trunk** fare clic su **Commit** e quindi su **Salva tutto**.
    

    > [!NOTE]
    > Ogni volta che si crea o modifica una regola di conversione, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Creare o modificare manualmente una regola di conversione](lync-server-2013-create-or-modify-a-translation-rule-manually.md)  
[Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Concetti

[Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md)

