---
title: Uso dell'autenticazione a due fattori con il client Lync
TOCTitle: Uso dell'autenticazione a due fattori con il client Lync
ms:assetid: d4136e61-c3ab-4b26-85c8-c1b2c24f5ee3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn338071(v=OCS.15)
ms:contentKeyID: 56269985
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uso dell'autenticazione a due fattori con il client Lync

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento viene descritto come utilizzare l'autenticazione a due fattori con il client Lync 2013.

## Accedere a Lync 2013 per la prima volta

Le informazioni di accesso vengono in genere configurate automaticamente al momento dell'installazione di Lync 2013. La prima volta che si usa Lync, tuttavia, può essere necessario avviare manualmente il client.

**Per accedere a Lync per la prima volta**

1.  Accedere alla rete dell'organizzazione.

2.  Fare clic su **Start** \> **Tutti i programmi** \> **Microsoft Lync \> Lync 2013**.
    
    Verrà visualizzata la schermata di accesso di Lync.
    
      - Se la casella dell'indirizzo di accesso è già compilata, verificare che l'indirizzo sia corretto.
    
      - Se non è corretto o la casella è vuota, immettere l'indirizzo di iscrizione a Lync, che in genere corrisponde al proprio indirizzo di posta elettronica.
    
      - Se viene visualizzata una casella della password vuota, inserire la propria password.

3.  Selezionare **Accedi**.

## Disconnettersi da Lync

Per uscire da Lync, è possibile chiudere la visualizzazione, disconnettere la sessione o uscire dal programma. Le opzioni sono disponibili nel menu File. Nella tabella seguente sono illustrate le differenze tra le opzioni.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Opzione</th>
<th>Risultato</th>
<th>Operazioni da eseguire</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chiudi</p></td>
<td><p>Chiude la visualizzazione di Lync, ma la sessione identificata dall'ID utente rimane in esecuzione. In questo modo è possibile continuare a ricevere notifiche e a interagire con gli altri utenti.</p>
<p>È possibile ripristinare la visualizzazione in qualsiasi momento facendo clic sull'icona di Lync sulla barra delle applicazioni o nell'area di notifica nella parte inferiore dello schermo.</p></td>
<td><p>Nella finestra principale di Lync effettuare una delle operazioni seguenti:</p>
<ol>
<li><p>Fare clic sul pulsante <strong>Opzioni</strong> e quindi selezionare <strong>File</strong> &gt; <strong>Chiudi</strong>.</p></li>
<li><p>Fare clic sul pulsante <strong>Chiudi</strong> (X) nell'angolo superiore destro della finestra.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Disconnetti</p></td>
<td><p>Termina la sessione di Lync associata all'ID utente, ma Lync rimane in esecuzione in background. Quando ci si disconnette, viene visualizzata la finestra di accesso.</p>
<div class="alert">
<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Selezionare <strong>Elimina le informazioni di accesso</strong> dopo la disconnessione per rimuovere i dati relativi a ID e password di accesso dal computer. Questa operazione consente al personale del supporto tecnico di risolvere più facilmente i problemi di accesso e può anche essere utile per garantire una maggiore sicurezza delle informazioni di accesso, limitando la possibilità che utenti non autorizzati accedano con le proprie credenziali.</td>
</tr>
</tbody>
</table>

</div></td>
<td><p>Nella finestra principale di Lync fare clic sul pulsante <strong>Opzioni</strong> e quindi selezionare <strong>File</strong> &gt; <strong>Disconnetti</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Esci</p></td>
<td><p>Termina la sessione di Lync e chiude Lync nel computer. Per riavviare Lync dopo averlo chiuso, fare clic su <strong>Start</strong> &gt; <strong>Tutti i programmi</strong> &gt; <strong>Microsoft Lync</strong> &gt; <strong>Lync 2013</strong>.</p></td>
<td><p>Nella finestra principale di Lync fare clic sul pulsante <strong>Opzioni</strong> e quindi selezionare <strong>File</strong> &gt; <strong>Esci</strong>.</p></td>
</tr>
</tbody>
</table>


## Accedere a Lync con una smart card

Alcune organizzazioni oggi si servono di una procedura di accesso in più fasi, denominata autenticazione a due fattori, per aumentare la sicurezza degli utenti di Lync 2013. Se viene utilizzata questa procedura, per accedere a Lync è necessaria una smart card. Le smart card sono di due tipi, fisiche e virtuali:

  - **Fisica**   Circa delle dimensioni di una carta di credito, va inserita in un lettore di smart card al momento dell'accesso.

  - **Virtuale**   Non si tratta di un oggetto fisico, ma di un identificatore elettronico che viene scritto in uno speciale chip del computer. In sostanza, la smart card viene creata all'interno del computer. Disponibile solo per l'uso nei computer Windows 8 che contengono il chip TPM (Trusted Platform Module).

## Registrare la smart card

Prima che sia possibile accedere con una smart card è necessario registrarla, ovvero associare le credenziali dell'utente alla carta. Questa operazione va eseguita sia per le smart card fisiche che per quelle virtuali. È possibile che sia stata già eseguita dall'amministratore di Lync Server. In caso di dubbi, rivolgersi a quest'ultimo.


> [!NOTE]
> Poiché ogni smart card virtuale è associata solo al dispositivo in cui è installata, sarà necessario registrare una smart card distinta per ogni computer Windows 8 in uso.



**Per registrare manualmente la smart card**

1.  Accedere al computer in cui si userà Lync.

2.  Usando Internet Explorer, passare alla pagina Registrazione Web dell'Autorità di certificazione dell'organizzazione.
    
    Se non si dispone già dell'indirizzo Web di questa risorsa, chiederlo all'amministratore di Lync Server. L'URL sarà simile al seguente: https://MyCA.\[nomesocietà\].com/certsrv.
    

    > [!NOTE]
    > Se si usa Internet Explorer 10, potrebbe essere necessario visualizzare il sito Web in modalità di compatibilità.



3.  Quando viene richiesto di accedere alla pagina di certificazione, usare l'account di dominio anziché quello di amministratore del computer.

4.  Nella pagina di benvenuto del sito Web selezionare **Richiedi un certificato**.

5.  Selezionare **Richiesta avanzata di certificati**.

6.  Selezionare **Creare e inviare una richiesta a questa CA** e quindi fare clic su **Avanti**.

7.  Verrà visualizzata la pagina Stazione di registrazione di Smart Card. Accettare la richiesta di installazione del controllo ActiveX e quindi compilare il modulo Richiesta avanzata di certificati come segue:
    
    1.  Selezionare **Utente con smart card** nell'elenco **Modello di certificato**.
    
    2.  Selezionare **Crea nuovo set di chiavi**.
    
    3.  Trovare le informazioni sul produttore sull'etichetta della smart card e selezionare il produttore nell'elenco a discesa **CSP**.
    
    4.  Selezionare **CSP** come Formato richiesta, se non è già selezionato.
    
    5.  Selezionare **sha1** nell'elenco a discesa Algoritmo hash, se non è già selezionato.
    
    6.  Assegnare al certificato un nome riconoscibile e fare clic su **Invia**.

8.  Inserire quindi la smart card vuota nel lettore di smart card disponibile nella stazione di registrazione e fare clic su **Registra**.

9.  Quando richiesto, inserire il PIN e fare clic su **OK**.
    

    > [!NOTE]
    > Se il responsabile del supporto tecnico non ha fornito alcun PIN specifico da utilizzare per registrare la smart card, immettere il PIN predefinito, ovvero 12345678.



10. Selezionare l'opzione per fare in modo che sia obbligatorio cambiare il PIN al primo utilizzo della smart card.

11. Inserire quindi la smart card vuota nel lettore di smart card disponibile nella stazione di registrazione e fare clic su **Registra**.

12. Quando richiesto, inserire il PIN e fare clic su **OK**.
    

    > [!NOTE]
    > Se il responsabile del supporto tecnico non ha fornito alcun PIN specifico da utilizzare per registrare la smart card, immettere il PIN predefinito, ovvero 12345678.



13. Selezionare l'opzione per fare in modo che sia obbligatorio cambiare il PIN al primo utilizzo della smart card.

14. Fare clic su **OK** per confermare che il certificato visualizzato contiene le informazioni dell'utente.

15. Quando viene visualizzato l'avviso che il certificato è stato emesso, fare clic su **Installa questo certificato** per completare la procedura di registrazione.

## Accedere a Lync con le credenziali della smart card

Prima di usare la smart card per la prima volta, è consigliabile fare clic su **Elimina le informazioni di accesso** nella pagina di accesso di Lync. In questo modo le credenziali di accesso memorizzate nel computer verranno eliminate, eliminando di conseguenza una possibile fonte di errori.

**Per accedere a Lync con le credenziali della smart card**

1.  Avviare il client Lync.

2.  Nella schermata di accesso digitare il nome account utente utilizzato per l'iscrizione nella casella **Indirizzo di accesso** e quindi fare clic su **Accedi**.

3.  Se si usa una smart card virtuale, saltare questo passaggio.
    
    Se si usa una smart card fisica, inserirla nel lettore di smart card quando viene richiesto, quindi fare clic su **OK** quando la smart card viene rilevata.

4.  Digitare il PIN della smart card e fare clic su **OK**.
    

    > [!NOTE]
    > Se il responsabile del supporto tecnico non ha fornito alcun PIN specifico da utilizzare per la smart card, immettere il PIN predefinito, ovvero 12345678.


