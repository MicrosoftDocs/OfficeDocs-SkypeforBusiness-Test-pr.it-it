---
title: 'Lync Server 2013: Modificare un dial plan'
TOCTitle: Modificare un dial plan
ms:assetid: a91f02df-cf60-40cf-82fe-e0342c118b91
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412797(v=OCS.15)
ms:contentKeyID: 49301603
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare un dial plan in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Per modificare un dial plan esistente, eseguire i passaggi illustrati nella procedura seguente. Se si desidera creare un nuovo dial plan, vedere [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md).

## Per modificare un dial plan

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Dial plan** .

4.  Nella pagina **Dial plan** fare doppio clic sul nome di un dial plan.
    

    > [!NOTE]
    > L'ambito e il nome del dial plan sono stati impostati al momento della creazione del dial plan e non possono essere modificati.



5.  (Facoltativo) In **Modifica dial plan** modificare il campo **Nome semplice** , in cui viene inserito automaticamente il nome visualizzato nel campo **Nome** , specificando un nome più descrittivo che rifletta il sito, il servizio o l'utente a cui si applica il dial plan.
    
    > [!IMPORTANT]  
    > Il <strong>Nome semplice</strong> deve essere univoco tra tutti i dial plan all'interno della distribuzione di Lync Server 2013 e può contenere al massimo 256 caratteri Unicode. Sono supportati i caratteri alfabetici e numerici, il trattino (-), il punto (.), il segno più (+) o il carattere di sottolineatura (_).<br />    Il campo <strong>Nome semplice</strong> non supporta gli spazi.

6.  (Facoltativo) Nel campo **Descrizione** digitare informazioni descrittive sul dial plan.

7.  (Facoltativo) Se si desidera utilizzare questo dial plan come area per i numeri di accesso esterno, specificare un' **Area conferenza telefonica con accesso esterno** . Se non si desidera utilizzare questo dial plan per i numeri di accesso esterno, lasciare vuoto il campo.
    

    > [!NOTE]
    > Le aree di conferenza telefonica con accesso esterno sono necessarie per associare i numeri di accesso alla conferenza telefonica con accesso esterno a uno o più dial plan.



8.  (Facoltativo) Nel campo **Prefisso accesso esterno** specificare un valore solo se gli utenti devono comporre una o più cifre iniziali aggiuntive, ad esempio 9, per accedere a una linea esterna. È possibile digitare un valore di prefisso con al massimo quattro caratteri (\#, \* e i numeri da 0 a 9).
    

    > [!NOTE]
    > Se si specifica un prefisso di accesso esterno, non è necessario creare una nuova regola di normalizzazione per includerlo.



9.  Associare e configurare le regole di normalizzazione per il dial plan:
    
      - Per scegliere una o più regole da un elenco di regole di normalizzazione disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . Nella finestra di dialogo **Seleziona regole di normalizzazione** evidenziare le regole da associare al dial plan e fare clic su **OK** .
    
      - Per definire una nuova regola di normalizzazione e associarla al dial plan, fare clic su **Nuova** . Per informazioni dettagliate sulla definizione di una nuova regola, vedere [Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md).
    
      - Per modificare una regola di normalizzazione già associata al dial plan, evidenziare il nome della regola e fare clic su **Mostra dettagli** . Per informazioni dettagliate sulla modifica della regola, vedere [Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md).
    
      - Per copiare una regola di normalizzazione esistente da utilizzare come punto di partenza per la definizione di una nuova regola, evidenziare il nome della regola e fare clic su **Copia** e quindi su **Incolla** . Per informazioni dettagliate sulla modifica della copia, vedere [Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md).
    
      - Per rimuovere una regola di normalizzazione dal dial plan, evidenziarne il nome e fare clic su **Rimuovi** .
    

    > [!NOTE]
    > A ogni dial plan deve essere associata almeno una regola di normalizzazione. Per i dettagli relativi a come determinare tutte le regole di normalizzazione necessarie per un dial plan, vedere <A href="lync-server-2013-dial-plans-and-normalization-rules.md">Dial plan e regole di normalizzazione in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



10. Verificare che le regole di normalizzazione del dial plan siano disposte nell'ordine corretto. Per modificare la posizione di una regola nell'elenco, evidenziare il nome della regola e fare clic sulla freccia su o giù.
    
    > [!IMPORTANT]  
    > Lync Server scorre l'elenco di regole di normalizzazione dall'alto verso il basso e utilizza la prima regola corrispondente al numero composto. Se si configura un dial plan in modo che un numero composto possa corrispondere a più regole di normalizzazione, assicurarsi che le regole più restrittive vengano ordinate prima di quelle meno restrittive.<br />    La regola di normalizzazione predefinita <strong>Mantieni tutti</strong> <strong>^(\d{11})$</strong> corrisponde a qualsiasi numero di 11 cifre. Se ad esempio si aggiunge una regola di normalizzazione che corrisponde ai numeri da 11 cifre che iniziano con 1425, verificare che la regola <strong>Mantieni tutti</strong> sia posta al di sotto della regola più restrittiva <strong>^(1425\d{7})$</strong> .

11. (Facoltativo) Immettere un numero per testare il dial plan e quindi fare clic su **Vai** . I risultati del test vengono visualizzati in **Numero composto da testare** .
    

    > [!NOTE]
    > È possibile salvare un dial plan che non ha superato ancora il test e quindi riconfigurarlo successivamente. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



12. Fare clic su **OK** .

13. Nella pagina **Dial plan** fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si crea o si modifica un dial plan, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Ulteriori risorse

[Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md)

