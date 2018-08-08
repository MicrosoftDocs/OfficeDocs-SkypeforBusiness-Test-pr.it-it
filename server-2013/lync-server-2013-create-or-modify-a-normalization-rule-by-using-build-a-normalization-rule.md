---
title: "Lync Server 2013: Crea/modif. regola di normalizz. con Crea regola di normalizz."
TOCTitle: Creare o modificare una regola di normalizzazione utilizzando Crea regola di normalizzazione
ms:assetid: e8547d7b-f74d-4a73-9a7d-df20d7a87fcd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399036(v=OCS.15)
ms:contentKeyID: 49302337
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una regola di normalizzazione utilizzando Crea regola di normalizzazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Eseguire le operazioni seguenti se si desidera creare o modificare una regola di normalizzazione nel Pannello di controllo di Lync Server. In alternativa, se si desidera creare o modificare manualmente una regola di normalizzazione, vedere [Creare o modificare manualmente una regola di normalizzazione in Lync Server 2013](lync-server-2013-create-or-modify-a-normalization-rule-manually.md).

## Per definire una regola mediante Crea regola di normalizzazione

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins oppure come membro del ruolo CsVoiceAdministrator, CsServerAdministrator o CsAdministrator. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md).

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  (Facoltativo) Eseguire le operazioni descritte in [Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md) fino al passaggio 11 o in [Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md) fino al passaggio 10.

4.  In **Nuova regola di normalizzazione** o **Modifica regola di normalizzazione** digitare un nome descrittivo del formato del numero da normalizzare in **Nome** , ad esempio **Prefisso5Cifre** .

5.  (Facoltativo) In **Descrizione** digitare una descrizione della regola di normalizzazione, ad esempio "Converte prefissi a 5 cifre".

6.  In **Crea regola di normalizzazione** immettere valori nei campi seguenti:
    
      - **Cifre iniziali**    (Facoltativo) Specificare le cifre iniziali dei numeri composti che si desidera corrispondano al formato. Digitare ad esempio **425** se si desidera che il formato corrisponda ai numeri composti che iniziano con 425.
    
      - **Lunghezza**    Specificare il numero di cifre nel formato corrispondente e specificare se si desidera applicare il formato ai numeri esattamente di questa lunghezza, almeno di questa lunghezza o di qualsiasi lunghezza.
    
      - **Cifre da rimuovere**    (Facoltativo) Specificare il numero di cifre iniziali da rimuovere dai numeri composti che si desidera corrispondano al formato.
    
      - **Prefisso**    (Facoltativo) Specificare le cifre da aggiungere ai numeri composti che si desidera corrispondano al formato.
    
    I valori immessi in questi campi vengono riportati nei campi **Formato per corrispondenza** e **Regola di conversione** . Se ad esempio il campo **Cifre iniziali** viene lasciato vuoto, si digita **7** nel campo **Lunghezza** e si seleziona **Esattamente** , quindi si specifica **0** in **Cifre da rimuovere** , l'espressione regolare risultante nel campo **Formato per corrispondenza** sarà:
    
    **^(\\d{7})$**

7.  In **Regola di conversione** specificare un modello per il formato dei numeri di telefono E.164 convertiti, come indicato di seguito:
    
      - Un valore che rappresenta il numero di cifri specificato nel formato della corrispondenza. Se ad esempio il formato è **^(\\d{7})$** , nella regola di conversione **$1** rappresenta numeri composti a 7 cifre.
    
      - (Facoltativo) Digitare un valore nel campo **Prefisso** per specificare le cifre da anteporre al numero convertito (ad esempio **+1425** ).
    
    Se ad esempio il campo **Formato per corrispondenza** contiene **^(\\d{7})$** come formato per i numeri composti e il campo **Regola di conversione** contiene **+1425$1** come formato per i numeri telefonici E.164, la regola normalizza 5550100 in +14255550100.

8.  (Facoltativo) Se la regola di normalizzazione restituisce un numero di telefono interno all'organizzazione, selezionare **Estensione interna** .

9.  (Facoltativo) Immettere un numero per testare la regola di normalizzazione e quindi fare clic su **Vai** . I risultati del test vengono visualizzati in **Immetti numero di telefono da testare** .
    

    > [!NOTE]
    > È possibile salvare una regola di normalizzazione che non ha ancora superato il test e riconfigurarla successivamente. Per informazioni dettagliate, vedere <A href="lync-server-2013-test-voice-routing.md">Testare il routing vocale in Lync Server 2013</A>.



10. Fare clic su **OK** per salvare la regola di normalizzazione.

11. Fare clic su **OK** per salvare il dial plan.

12. Nella pagina **Dial plan** fare clic su **Commit** e quindi su **Salva tutto** .
    

    > [!NOTE]
    > Ogni volta che si crea o modifica una regola di normalizzazione, è necessario eseguire il comando <STRONG>Salva tutto</STRONG> per pubblicare la modifica apportata alla configurazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md">Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Vedere anche

#### Attività

[Creare o modificare manualmente una regola di normalizzazione in Lync Server 2013](lync-server-2013-create-or-modify-a-normalization-rule-manually.md)  
[Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md)  
[Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md)  
[Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)  

#### Ulteriori risorse

[Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

