---
title: "Lync Server 2013: Imposta certificati per interfaccia perimetrale esterna"
TOCTitle: Impostare i certificati per l'interfaccia perimetrale esterna
ms:assetid: 5d78182c-88d8-4483-95ad-74b17f2d5fac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398409(v=OCS.15)
ms:contentKeyID: 49300702
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostare i certificati per l'interfaccia perimetrale esterna per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

> [!IMPORTANT]  
> Quando si esegue la Configurazione guidata certificati, verificare di aver effettuato l'accesso con un account membro di un gruppo che dispone delle autorizzazioni appropriate per il tipo di modello di certificato da utilizzare. Per impostazione predefinita, per una richiesta di certificato di Lync Server viene utilizzato il modello di certificato WebServer. Se per la richiesta di un certificato con questo modello si utilizza un account membro del gruppo RTCUniversalServerAdmins, verificare che al gruppo siano state assegnate le autorizzazioni di registrazione necessarie per l'utilizzo del modello.

Per ogni server perimetrale è necessario un certificato pubblico nell'interfaccia tra la rete perimetrale e Internet e il nome alternativo soggetto del certificato deve contenere i nomi esterni dei nomi di dominio completi (FQDN) del servizio Access Edge e del servizio Web Conferencing Edge.

Per i dettagli relativi ai requisiti di questo e altri certificati, vedere [Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013](lync-server-2013-certificate-requirements-for-external-user-access.md).

Per l'elenco delle autorità di certificazione (CA) pubbliche che forniscono i certificati conformi ai requisiti specifici dei certificati per comunicazioni unificate e che hanno collaborato con Microsoft per garantire il supporto della Configurazione guidata certificati di Lync Server 2013, vedere l'articolo 929395 della Microsoft Knowledge Base "Partner certificato di comunicazioni unificate" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202834](http://go.microsoft.com/fwlink/p/?linkid=202834).

## Configurazione dei certificati nelle interfacce esterne

Per configurare un certificato sull'interfaccia perimetrale esterna di un sito, utilizzare le procedure in questa sezione per eseguire le operazioni seguenti:

  - Creare la richiesta di certificato per l'interfaccia esterna del server perimetrale.

  - Inviare la richiesta alla CA pubblica.

  - Importare il certificato per l'interfaccia esterna di ogni server perimetrale.

  - Assegnare il certificato per l'interfaccia esterna di ogni server perimetrale.

  - Se la distribuzione include più server perimetrali, esportare il certificato insieme alla relativa chiave privata, quindi copiarlo negli altri server perimetrali. Per ogni server perimetrale, quindi, importarlo e assegnarlo come descritto in precedenza. Ripetere questa procedura per ogni server perimetrale.

È possibile richiedere certificati pubblici direttamente a un'autorità di certificazione (CA) pubblica, ad esempio dal sito Web di una CA pubblica. Le procedure in questa sezione utilizzano la Configurazione guidata certificati per la maggior parte delle attività correlate ai certificati. Se si sceglie di richiedere un certificato direttamente a una CA pubblica, sarà necessario modificare ogni procedura nel modo appropriato per richiedere, trasferire e importare il certificato, nonché importare la catena di certificati.

Quando si richiede un certificato a una CA esterna, le credenziali fornite devono disporre dei diritti necessari per richiedere un certificato a tale CA. Per ogni CA esistono criteri di sicurezza che definiscono le credenziali, ovvero i nomi di utenti e gruppi specifici, cui è consentito richiedere, emettere, gestire o leggere certificati.

Se si decide di utilizzare la console MMC (Microsoft Management Console) Certificati per importare la catena di certificati e il certificato, è necessario importarli nell'archivio certificarti per il computer. Se li si importa nell'archivio certificati dell'utente o del servizio, il certificato non sarà disponibile per l'assegnazione nella Configurazione guidata certificati di Lync Server 2013.

## Per creare la richiesta di certificato per l'interfaccia esterna del server perimetrale

1.  Nel server perimetrale fare clic su **Riesegui** nella Distribuzione guidata accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** .
    

    > [!NOTE]
    > Se l'organizzazione desidera supportare la connettività di messaggistica istantanea pubblica con AOL, non è possibile utilizzare la Distribuzione guidata di Lync Server per richiedere il certificato. Eseguire invece i passaggi della procedura "Per creare una richiesta di certificato per l'interfaccia esterna del server perimetrale per il supporto della connettività di messaggistica istantanea pubblica con AOL" più avanti in questo argomento.<BR>Se sono presenti più server perimetrali in una stessa posizione in un pool, è possibile eseguire la Configurazione guidata certificati di Lync Server 2013 in uno qualsiasi dei server perimetrali.



2.  Nella pagina **Attività certificato disponibili** fare clic su **Crea una nuova richiesta di certificato** .

3.  Nella pagina **Richiesta di certificato** fare clic su **Certificato perimetro esterno** .

4.  Nella pagina **Richieste immediate o ritardate** selezionare la casella di controllo **Prepara la richiesta per l'invio posticipato** .

5.  Nella pagina **File richiesta di certificato** digitare il percorso completo e il nome del file in cui si desidera salvare la richiesta, ad esempio c:\\cert\_perimetro\_esterno.cer.

6.  Nella pagina **Specifica modello di certificato alternativo** , per utilizzare un modello diverso dal modello Web Server predefinito selezionare la casella di controllo **Utilizza modello di certificato alternativo per l'autorità di certificazione selezionata** .

7.  Nella pagina **Impostazioni nome e sicurezza** eseguire le operazioni seguenti:
    
      - In **Nome descrittivo** digitare un nome visualizzato per il certificato.
    
      - In **Lunghezza bit** specificare la lunghezza in bit (di solito, l'impostazione predefinita **2048** ).
    
      - Verificare che la casella di controllo **Contrassegna come esportabile la chiave di certificato privata** sia selezionata.

8.  Nella pagina **Informazioni sull'organizzazione** digitare il nome dell'organizzazione e dell'unità organizzativa, ad esempio una divisione o un reparto.

9.  Nella pagina **Dati geografici** specificare le informazioni sulla posizione.

10. Nella pagina **Nome soggetto / Nomi soggetto alternativi** verranno visualizzate le informazioni compilate automaticamente dalla procedura guidata. Se sono necessari ulteriori nomi alternativi soggetto, specificarli nei prossimi due passaggi.

11. Nella pagina **Impostazione del dominio SIP su nomi soggetto alternativi (SAN)** selezionare la casella di controllo del dominio per aggiungere una voce sip. *\<dominiosip\>* all'elenco dei nomi alternativi soggetto.

12. Nella pagina **Configura nomi alternativi soggetto aggiuntivi** specificare eventuali nomi alternativi del soggetto aggiuntivi necessari.

13. Nella pagina **Riepilogo richiesta** esaminare le informazioni sul certificato da utilizzare per generare la richiesta.

14. Al termine dell'esecuzione dei comandi, eseguire le operazioni seguenti:
    
      - Per visualizzare il log della richiesta di certificato, fare clic su **Visualizza log** .
    
      - Per completare la richiesta di certificato, fare clic su **Avanti** .

15. Nella pagina **File richiesta di certificato** eseguire le operazioni seguenti:
    
      - Per visualizzare il file richiesta di firma del certificato (CSR) generato, fare clic su **Visualizza** .
    
      - Per chiudere la procedura guidata, fare clic su **Fine** .

16. Copiare il file di output in un percorso da cui possa essere inoltrato alla CA pubblica.

## Per creare una richiesta di certificato per l'interfaccia esterna del server perimetrale per il supporto della connettività di messaggistica istantanea pubblica con AOL

1.  Quando il modello richiesto è disponibile per la CA, utilizzare il cmdlet Windows PowerShell seguente dal server perimetrale per richiedere il certificato:
    
        Request-CsCertificate -New -Type AccessEdgeExternal  -Output C:\ <certfilename.txt or certfilename.csr>  -ClientEku $true -Template <template name>
    
    Il nome predefinito del certificato del modello disponibile in Lync Server 2013 è Web Server. Specificare solo *\<nome modello\>* se è necessario utilizzare un modello diverso da quello predefinito.
    

    > [!NOTE]
    > Se l'organizzazione desidera supportare la messaggistica istantanea pubblica con AOL, è necessario utilizzare Windows PowerShell anziché la Configurazione guidata certificati per richiedere il certificato da assegnare al perimetro esterno per il servizio Access Edge. Il motivo è che il modello Web Server di Lync Server 2013 utilizzato dalla Configurazione guidata certificati per richiedere un certificato non supporta la configurazione dell'utilizzo chiavi avanzato (EKU) client. Prima di utilizzare Windows PowerShell per creare il certificato, l'amministratore della CA deve creare e distribuire un nuovo modello che supporta l'EKU client



## Per inviare una richiesta a un'autorità di certificazione pubblica

1.  Aprire il file di output.

2.  Copiare e incollare il contenuto della richiesta di firma del certificato (CSR).

3.  Se richiesto, specificare le impostazioni seguenti:
    
      - **Microsoft** come piattaforma server.
    
      - **IIS** come versione.
    
      - **Server Web** come tipo di utilizzo.
    
      - **PKCS7** come formato della risposta.

4.  Dopo la verifica delle informazioni da parte della CA pubblica, si riceverà un messaggio di posta elettronica contenente il testo richiesto per il certificato.

5.  Copiare il testo dal messaggio di posta elettronica e salvarne il contenuto in un file di testo (con estensione txt) nel computer locale.

## Per importare il certificato per l'interfaccia esterna del server perimetrale

1.  Accedere come membro del gruppo Administrators al server perimetrale in cui è stata creata la richiesta di certificato.

2.  Nella pagina **Distribuisci Edge Server** della Distribuzione guidata fare clic su **Riesegui** accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** .

3.  Nella pagina **Attività certificato disponibili** fare clic su **Importa un certificato da un file con estensione p7b, pfx o cer** .

4.  Nella pagina **Importa certificato** fare clic su **Sfoglia** per individuare e selezionare il certificato richiesto per l'interfaccia esterna del server perimetrale, In alternativa, è possibile digitare il percorso completo e il nome di file. Se il certificato contiene una chiave privata, selezionare **Il file di certificato contiene una chiave di certificato privata** e digitare la password per la chiave privata. Fare clic su **Avanti** .

5.  Nella pagina **Riepilogo importazione certificato** verificare le informazioni di riepilogo e quindi fare clic su **Avanti** .

6.  In **Esecuzione comandi in corso** controllare i risultati dell'impostazione, fare clic su **Visualizza log** per ulteriori informazioni eventualmente necessarie e quindi fare clic su **Fine** per completare l'importazione del certificato.

7.  Se si sta configurando un pool di server perimetrali, esportare il certificato con la relativa chiave privata come descritto nella procedura "Per esportare il certificato con la chiave privata per i server perimetrali in un pool" di seguito in questo argomento. Copiare il file del certificato esportato negli altri server perimetrali e importarlo nell'archivio del computer in ogni server perimetrale.

## Per esportare il certificato con la chiave privata per i server perimetrali in un pool

1.  Accedere con un account membro del gruppo Administrators allo stesso server perimetrale in cui è stato importato il certificato.

2.  Fare clic sul pulsante **Start** , scegliere **Esegui** e digitare **MMC** .

3.  Nella console MMC scegliere **Aggiungi/Rimuovi snap-in** dal menu **File** .

4.  In **Aggiungi o rimuovi snap-in** fare clic su **Certificati** e quindi su **Aggiungi** .

5.  Nella finestra di dialogo **Certificati** selezionare **Account computer** , fare clic su **Avanti** , selezionare **Computer locale (il computer su cui è in esecuzione questa console)** in **Selezione computer** , fare clic su **Fine** e quindi fare clic su **OK** per completare la configurazione della console MMC.

6.  Fare doppio clic su **Certificati (computer locale)** per espandere gli archivi di certificati, fare doppio clic su **Personale** e quindi doppio clic su **Certificati** .
    
    > [!IMPORTANT]  
    > Se nell'archivio personale dei certificati non sono presenti certificati per il computer locale, al certificato importato non è associata alcuna chiave privata. Rivedere i passaggi della richiesta e dell'impostazione. Se il problema persiste, rivolgersi all'amministratore o al provider dell'autorità di certificazione.

7.  Nell'archivio dei certificati personali per il computer locale fare clic con il pulsante destro del mouse sul certificato da esportare, scegliere **Tutte le attività** e quindi fare clic su **Esporta** .

8.  Nell'Esportazione guidata certificati fare clic su **Avanti** , selezionare **Sì, esporta la chiave privata** e quindi fare clic su **Avanti** .
    

    > [!NOTE]
    > Se l'opzione <STRONG>Sì, esporta la chiave privata</STRONG> non è disponibile, la chiave privata associata al certificato non è stata contrassegnata per l'esportazione. Per continuare l'esportazione, è necessario ripetere la richiesta di certificato, verificando che il certificato stesso sia contrassegnato per l'esportazione della chiave privata. Rivolgersi all'amministratore o al provider dell'autorità di certificazione.



9.  Nella finestra di dialogo Formato file di esportazione selezionare **Scambio di informazioni personali - PKCS\#12 (.PFX)** e quindi selezionare le opzioni seguenti:
    
      - Se possibile, includi tutti i certificati nel percorso di certificazione
    
      - Esporta tutte le proprietà estese
        

        > [!WARNING]
        > Quando si esporta un certificato da un server perimetrale, non selezionare <STRONG>Elimina la chiave privata se l'esportazione ha esito positivo</STRONG> . In caso contrario, è necessario importare nel server perimetrale il certificato e la chiave privata.



10. Fare clic su **Avanti** .

11. Digitare una password per la chiave privata, digitarla di nuovo per confermare e quindi fare clic su **Avanti** .

12. Digitare un percorso e un nome di file per il certificato esportato Assegnare al file l'estensione pfx. Il percorso deve essere accessibile per tutti gli altri server perimetrali del pool o disponibile per il trasporto mediante supporti rimovibili, ad esempio un'unità flash USB. Fare clic su **Avanti** .

13. Controllare le informazioni di riepilogo in **Completamento dell'Esportazione guidata certificati** e quindi fare clic su **Fine** .

14. Nella finestra di dialogo di completamento dell'esportazione fare clic su **OK** .

15. Importare il file del certificato esportato negli altri server perimetrali seguendo i passaggi descritti nella procedura “Per importare il certificato per l'interfaccia esterna del server perimetrale” più indietro in questo argomento.

## Per assegnare il certificato per l'interfaccia esterna del server perimetrale

1.  In ogni server perimetrale, nella Distribuzione guidata, accanto a **Passaggio 3: Richiesta, installazione o assegnazione dei certificati** , fare clic su **Riesegui** .

2.  Nella pagina **Attività certificato disponibili** fare clic su **Assegna un certificato esistente** .

3.  Nella pagina **Assegnazione certificato** fare clic su **Certificato perimetro esterno** e selezionare la casella di controllo **Utilizzi avanzati certificato** .

4.  Nella pagina **Utilizzi avanzati certificato** selezionare tutte le caselle di controllo per assegnare il certificato a tutti i tipi di utilizzo.

5.  Nella pagina **Archivio certificati** selezionare il certificato pubblico richiesto e importato per l'interfaccia esterna del server perimetrale.
    

    > [!NOTE]
    > Se il certificato richiesto e importato non è incluso nell'elenco, uno dei metodi per risolvere il problema consiste nel verificare che il nome soggetto e i nomi alternativi soggetto del certificato soddisfino tutti i requisiti per il certificato. Se il certificato e la catena di certificati sono stati importanti manualmente anziché tramite le procedure precedenti, è necessario verificare che il certificato si trovi nell'archivio corretto, ovvero l'archivio del computer e non quello dell'utente o del servizio.



6.  Nella pagina **Riepilogo assegnazione certificato** rivedere le impostazioni e quindi fare clic su **Avanti** per assegnare i certificati.

7.  Nella pagina finale della procedura guidata fare clic su **Fine** .

8.  Dopo aver assegnato il certificato del server perimetrale interno mediante questa procedura, aprire lo snap-in Certificati in ogni server, espandere **Certificati (computer locale)** , espandere **Personale** , fare clic su **Certificati** e quindi verificare che il certificato sia presente nel riquadro dei dettagli.

9.  Se la distribuzione include più server perimetrali, ripetere la procedura per ognuno di essi.

