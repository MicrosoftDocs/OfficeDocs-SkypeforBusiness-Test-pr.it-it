---
title: 'Lync Server 2013: Creare un dial plan'
TOCTitle: Creare un dial plan
ms:assetid: d2fef3d0-7e78-4591-b712-d62ac71d71a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398909(v=OCS.15)
ms:contentKeyID: 49302061
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un dial plan in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-24_

Per creare un nuovo dial plan, eseguire i passaggi illustrati nella procedura seguente. Se si desidera modificare un dial plan, vedere [Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md).

## Per creare un dial plan

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Routing vocale** e quindi su **Dial plan** .

4.  Nella pagina **Dial plan** fare clic su **Nuovo** e selezionare un ambito per il dial plan:
    
      - **Dial plan sito** è applicabile a un intero sito, ad eccezione degli eventuali utenti o gruppi assegnati a un dial plan utente. Se si seleziona **Sito** come ambito di un dial plan, è necessario scegliere il sito nella finestra di dialogo **Seleziona un sito** . Se per un sito è stato già creato un dial plan, il sito non viene visualizzato nella finestra di dialogo **Seleziona un sito** .
    
      - **Dial plan pool** può essere applicabile a un gateway PSTN (Public Switched Telephone Network) o a una funzione di registrazione. Se si seleziona **Pool** come ambito di un dial plan, scegliere il gateway PSTN o la funzione di registrazione nella finestra di dialogo **Seleziona un servizio** . Se è stato già creato un dial plan per un servizio (gateway PSTN o funzione di registrazione), il servizio non viene visualizzato nell'elenco.
    
      - **Dial plan utente** può essere applicato a utenti o gruppi specificati.
    

    > [!NOTE]
    > Dopo aver selezionato l'ambito del dial plan, non è più possibile modificarlo.



5.  Se si crea un dial plan utente, immettere un nome descrittivo nel campo **Nome** della finestra di dialogo **Nuovo dial plan** . Dopo aver salvato tale nome, non è più possibile modificarlo.
    

    > [!NOTE]
    > Per i dial plan sito, il campo <STRONG>Nome</STRONG> viene prepopolato con il nome del sito e non può essere modificato.<BR>Per i dial plan pool, il campo <STRONG>Nome</STRONG> viene prepopolato con il nome del gateway PSTN o della funzione di registrazione e non può essere modificato.



6.  Il campo **Nome semplice** viene prepopolato con lo stesso nome visualizzato nel campo **Nome** . Se si desidera, è possibile modificare il campo per specificare un nome più descrittivo che rifletta il sito, il servizio o l'utente al quale viene applicato il dial plan.
    
    > [!IMPORTANT]  
    > Il <strong>Nome semplice</strong> deve essere univoco tra tutti i dial plan all'interno della distribuzione di Lync Server e può contenere al massimo 256 caratteri Unicode. Sono supportati i caratteri alfabetici e numerici, il trattino (-), il punto (.) o il carattere di sottolineatura (_).<br />    <strong>Non sono supportati</strong> gli spazi e i caratteri riservati indicati in RFC 3966 (http://www.ietf.org/rfc/rfc3966.txt). I caratteri riservati <strong>non supportati</strong> nel <strong>Nome semplice</strong> includono i seguenti:<br />    &quot;;&quot; &quot;/&quot; &quot;?&quot; &quot;:&quot; &quot;@&quot; &quot;&amp;&quot; &quot;=&quot; &quot;+&quot; &quot;$&quot; &quot;,&quot;

7.  (Facoltativo) Nel campo **Descrizione** è possibile digitare ulteriori informazioni descrittive sul dial plan.

8.  (Facoltativo) Se si desidera utilizzare questo dial plan come area per i numeri di accesso esterno, specificare un' **Area conferenza telefonica con accesso esterno** . Se non si desidera utilizzare questo dial plan per i numeri di accesso esterno, lasciare vuoto il campo.
    

    > [!NOTE]
    > Le aree di conferenza telefonica con accesso esterno sono necessarie per associare i numeri di accesso alla conferenza telefonica con accesso esterno a uno o più dial plan.



9.  (Facoltativo) Nel campo **Prefisso accesso esterno** specificare un valore solo se gli utenti devono comporre una o più cifre iniziali aggiuntive, ad esempio 9, per accedere a una linea esterna. È possibile digitare un valore di prefisso con al massimo quattro caratteri (\#, \* e i numeri da 0 a 9).
    

    > [!NOTE]
    > Se si specifica un prefisso di accesso esterno, non è necessario creare una nuova regola di normalizzazione per includerlo.



10. Associare e configurare le regole di normalizzazione per il dial plan nel modo seguente:
    
      - Per scegliere una o più regole da un elenco di regole di normalizzazione disponibili nella distribuzione di VoIP aziendale, fare clic su **Seleziona** . In **Seleziona regole di normalizzazione** evidenziare le regole da associare al dial plan e fare clic su **OK** .
    
      - Per definire una nuova regola di normalizzazione e associarla al dial plan, fare clic su **Nuova** . Per informazioni dettagliate sulla definizione di una nuova regola, vedere [Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md).
    
      - Per modificare una regola di normalizzazione già associata al dial plan, evidenziare il nome della regola e fare clic su **Mostra dettagli** . Per informazioni dettagliate sulla modifica della regola, vedere [Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md).
    
      - Per copiare una regola di normalizzazione esistente da utilizzare come punto di partenza per la definizione di una nuova regola, evidenziare il nome della regola e fare clic su **Copia** e quindi su **Incolla** . Per informazioni dettagliate sulla modifica della copia, vedere [Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md).
    
      - Per rimuovere una regola di normalizzazione dal dial plan, evidenziarne il nome e fare clic su **Rimuovi** .
    

    > [!NOTE]
    > A ogni dial plan deve essere associata almeno una regola di normalizzazione. Per informazioni su come determinare tutte le regole di normalizzazione necessarie per un dial plan, vedere <A href="lync-server-2013-dial-plans-and-normalization-rules.md">Dial plan e regole di normalizzazione in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



11. Verificare che le regole di normalizzazione del dial plan siano disposte nell'ordine corretto. Per modificare la posizione di una regola nell'elenco, evidenziare il nome della regola e fare clic sulla freccia su o giù.
    
    > [!IMPORTANT]  
    > Lync Server scorre l'elenco di regole di normalizzazione dall'alto verso il basso e utilizza la prima regola corrispondente al numero composto. Se si configura un dial plan in modo che un numero composto possa corrispondere a più regole di normalizzazione, assicurarsi che le regole più restrittive vengano ordinate prima di quelle meno restrittive.<br />    La regola di normalizzazione predefinita <strong>Mantieni tutti</strong> , <strong>^(\d{11})$</strong> , corrisponde a qualsiasi numero a 11 cifre. Se ad esempio si aggiunge una regola di normalizzazione corrispondente ai numeri a 11 cifre che iniziano con 1425, assicurarsi che la regola <strong>Mantieni tutti</strong> sia disposta al di sotto della regola più restrittiva <strong>^(1425\d{7})$</strong> .

12. (Facoltativo) Immettere un numero per testare il dial plan e quindi fare clic su **Vai** . I risultati del test vengono visualizzati in **Numero composto da testare** .
    

    > [!NOTE]
    > È possibile salvare un dial plan che non ha superato ancora il test e quindi riconfigurarlo successivamente. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



13. Fare clic su **OK** .

14. Nella pagina **Dial plan** fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si crea un dial plan, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Ulteriori risorse

[Definizione di regole di normalizzazione in Lync Server 2013](lync-server-2013-defining-normalization-rules.md)

