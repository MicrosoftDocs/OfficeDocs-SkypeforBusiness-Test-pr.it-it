---
title: 'Lync Server 2013: Modifica dei certificati per i dispositivi mobili'
TOCTitle: Modifica dei certificati per i dispositivi mobili
ms:assetid: 4e9107af-20f4-4c2a-8c98-ca35b39a4e2d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690015(v=OCS.15)
ms:contentKeyID: 49300501
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifica dei certificati per i dispositivi mobili in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-06-20_

Per supportare connessioni sicure tra l'ambiente Lync e i client mobili, sarà necessario aggiornare i certificati SSL (Secure Socket Layer) per il pool di server Director, il pool Front End e il proxy inverso con alcune voci SAN (nome alternativo soggetto) aggiuntive. Se sono necessari ulteriori dettagli sui requisiti relativi ai certificati per le funzionalità per dispositivi mobili, vedere la sezione dedicata a questo argomento in [Requisiti tecnici per i dispositivi mobili in Lync Server 2013](lync-server-2013-technical-requirements-for-mobility.md). È però fondamentalmente necessario ottenere nuovi certificati dall'Autorità di certificazione con incluse le voci SAN aggiuntive e quindi aggiungere tali certificati seguendo le istruzioni in questo articolo.

Naturalmente, prima di iniziare è utile sapere quali sono i nomi alternativi soggetto già assegnati ai certificati. In caso di dubbi su cosa è già stato configurato, esistono molti modi per appurare le informazioni necessarie. Anche se esiste la possibilità di eseguire il cmdlet **Get-CsCertificate** e altri comandi di PowerShell per visualizzare queste informazioni (come descritto di seguito), per impostazione predefinita tali dati saranno troncati, quindi non tutte le proprietà necessarie potrebbero essere visibili. Per ottenere una buona visualizzazione del certificato e di tutte le relative proprietà, è possibile utilizzare Microsoft Management Console (MMC) e caricare lo snap-in Certificati (anche in questo caso sono disponibili istruzioni dettagliate di seguito) oppure controllare semplicemente nella Distribuzione guidata di Lync Server.

Come già indicato, le procedure seguenti illustrano come aggiornare i certificati tramite Lync Server Management Shell e MMC. Se si preferisce usare la Configurazione guidata certificati nella Distribuzione guidata di Lync Server, vedere [Configurare i certificati per il server Director in Lync Server 2013](lync-server-2013-configure-certificates-for-the-director.md) per il server Director o il pool di server Director, se configurati (non è obbligatorio). Per il server Front End o il pool Front End, vedere [Configurare i certificati per i server in Lync Server 2013](lync-server-2013-configure-certificates-for-servers.md).

Un ultimo aspetto da tenere presente è la possibilità che esista un singolo certificato predefinito nell'ambiente Lync Server 2013 oppure certificati separati per gli usi Default (tutto tranne i servizi Web), WebServicesExternal e WebServicesInternal. Qualunque sia la configurazione, le procedure seguenti dovrebbero essere di aiuto.

## Per aggiornare i certificati con nuovi nomi alternativi soggetto usando Lync Server Management Shell

1.  È necessario accedere al server Lync Server 2013 con un account con diritti e autorizzazioni di amministratore locale. Se si esegue il cmdlet di PowerShell **Request-CsCertificate** nei passaggi 12 e oltre, l'account deve anche disporre dei diritti per l'Autorità di certificazione (CA) specificata.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Prima di poter assegnare un certificato aggiornato, è necessario individuare i certificati assegnati al server e i relativi tipi di utilizzo. Nella riga di comando digitare:
    
        Get-CsCertificate

4.  Controllare l'output del passaggio precedente per scoprire se un certificato singolo è stato assegnato per più usi oppure se sono stati assegnati certificati diversi per ogni uso. Esaminare il parametro Use per individuare la modalità di utilizzo di un certificato. Confrontare il parametro Thumbprint per i certificati visualizzati per stabilire se lo stesso certificato presenta più utilizzi. Tenere sott'occhio il parametro Thumbprint.

5.  Aggiornare il certificato. Nella riga di comando digitare:
    
        Set-CsCertificate -Type <type of certificate as displayed in the Use parameter> -Thumbprint <unique identifier>
    
    Ad esempio, se il cmdlet **Get-CsCertificate** visualizza un certificato con Use Default, un altro con Use WebServicesInternal e un altro con Use WebServicesExternal, e se tutti i certificati hanno lo stesso valore Thumbprint, nella riga di comando digitare:
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
    
    **Importante:**
    
    Se viene assegnato un certificato separato per ogni uso (il valore Thumbprint controllato prima è diverso per ogni certificato), è fondamentale **non** eseguire il cmdlet **Set-CsCertificate** con più tipi, come nell'esempio precedente. In questo caso, eseguire il cmdlet **Set-CsCertificate** separatamente per ogni uso. Ad esempio:
    
        Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>

6.  Per visualizzare il certificato (o i certificati), fare clic sul pulsante **Start**, scegliere **Esegui** e digitare MMC per aprire Microsoft Management Console.

7.  Dal menu MMC scegliere **File** , **Aggiungi/Rimuovi snap-in…** , Certificati. Fare clic su **Aggiungi** . Quando richiesto, selezionare **Account del computer** e quindi fare clic su **Avanti** .

8.  Se il certificato si trova nel server in uso, selezionare **Computer locale**. Se il certificato si trova in un altro computer, selezionare **Altro computer** e quindi digitare il nome di dominio completo del computer oppure fare clic su **Sfoglia** in **Immettere il nome dell'oggetto da selezionare** e digitare il nome del computer. Fare clic su **Controlla nomi**. Dopo la risoluzione, il nome del computer viene sottolineato. Fare clic su **OK** e quindi su **Fine**. Fare clic su **OK** per eseguire il commit della selezione e chiudere la finestra di dialogo **Aggiungi/Rimuovi snap-in**.

9.  Per visualizzare le proprietà del certificato, espandere **Certificati** , espandere **Personali** e selezionare **Certificati** . Selezionare il certificato da visualizzare, fare clic con il pulsante destro del mouse sul certificato e scegliere **Apri** .

10. Nella visualizzazione **Certificati** selezionare **Dettagli** . Da qui è possibile scegliere il nome soggetto certificato selezionando **Soggetto** . Verranno visualizzati il nome soggetto assegnato e le proprietà associate.

11. Per visualizzare i nomi alternativi soggetto, selezionare **Nome alternativo soggetto**. Verranno visualizzati tutti i nomi alternativi soggetto assegnati. Per impostazione predefinita, i nomi alternativi soggetto trovati in questa posizione sono di tipo **Nome DNS**. Dovrebbero essere visibili i membri seguenti, tutti nomi di dominio completi rappresentati nei record host DNS (A o, se IPv6, AAAA):
    
      - Nome pool per i pool, o nome del singolo server, se non sono pool
    
      - Nome del server a cui il certificato è assegnato
    
      - Record URL semplici, di solito meet e dialin
    
      - Nome servizi Web interni e nome servizi Web esterni (ad esempio, webpool01.contoso.net, webpool01.contoso.com) in base alle scelte effettuate nel Generatore di topologie e ai servizi Web selezionati per la sostituzione.
    
      - Se già assegnati, i record lyncdiscover.\<dominiosip\> e lyncdiscoverinternal.\<dominiosip\>.
    
    L'ultimo elemento è il più interessante, se è presente una voce relativa al nome alternativo soggetto lyncdiscover e lyncdiscoverinternal.
    
    Ripetere questi passaggi se devono essere controllati più certificati. Dopo aver trovato queste informazioni, si può chiudere la visualizzazione del certificato e la MMC.

12. Se un nome alternativo soggetto del servizio di individuazione automatica risulta mancante e si usa un unico certificato predefinito per i tipi Default, WebServicesInternal e WebServiceExternal, eseguire le operazioni seguenti:
    
      - Al prompt dei comandi di Lync Server Management Shell digitare:
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        Se ci sono molti domini SIP, non si può usare il parametro AllSipDomain e si deve usare invece il parametro DomainName. Quando si usa il parametro DomainName, è necessario definire il nome FQDN per i record lyncdiscoverinternal e lyncdiscover. Ad esempio:
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - Per assegnare il certificato, digitare:
        
            Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        Dove “Thumbprint” è l'identificazione digitale visualizzata per il certificato appena rilasciato.

13. Per una voce SAN interna del servizio di individuazione automatica mancante, se si usano certificati separati per i tipi Default, WebServicesInternal e WebServicesExternal, eseguire le operazioni seguenti:
    
      - Al prompt dei comandi di Lync Server Management Shell digitare:
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -AllSipDomain -verbose
        
        Se ci sono molti domini SIP, non si può usare il parametro AllSipDomain e si deve usare invece il parametro DomainName. Quando si usa il parametro DomainName, è necessario usare un prefisso appropriato per il nome FQDN del dominio SIP. Ad esempio:
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - Per un nome alternativo soggetto del servizio di individuazione automatica esterno, nella riga di comando digitare:
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        Se ci sono molti domini SIP, non si può usare il parametro AllSipDomain e si deve usare invece il parametro DomainName. Quando si usa il parametro DomainName, è necessario usare un prefisso appropriato per il nome FQDN del dominio SIP. Ad esempio:
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -DomainName "Lyncdiscover.contoso.com, Lyncdiscover.contoso.net" -verbose
    
      - Per assegnare i tipi di certificato singoli, digitare:
        
            Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        Dove “Thumbprint” è l'identificazione digitale visualizzata per i singoli certificati appena rilasciati.
    

    > [!NOTE]
    > Notare che i passaggi 12 e 13 dovrebbero essere eseguiti solo se l'account usato per l'esecuzione ha accesso all'Autorità di certificazione con le autorizzazioni appropriate. Se non è possibile eseguire l'accesso con un account con tali autorizzazioni oppure se si usa un'Autorità di certificazione pubblica o remota per i certificati, è necessario richiederli tramite la Distribuzione guidata di Lync Server, a cui si è accennato all'inizio dell'articolo.


