---
title: Configurazione dei certificati per l'individuazione automatica
TOCTitle: Configurazione dei certificati per l'individuazione automatica
ms:assetid: 1842191d-df9a-41e0-9286-08c25f9b5dca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945617(v=OCS.15)
ms:contentKeyID: 52062102
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei certificati per l'individuazione automatica

 

_**Ultima modifica dell'argomento:** 2012-12-12_

I certificati per il pool di server Director, il pool Front End e il proxy inverso richiedono voci aggiuntive per i nomi alternativi soggetto per il supporto di connessioni sicure con i client Lync.


> [!NOTE]
> È possibile usare il cmdlet <STRONG>Get-CsCertificate</STRONG> per visualizzare informazioni sui certificati assegnati. Tuttavia la visualizzazione predefinita tronca le proprietà dei certificati e non mostra tutti i valori della proprietà SubjectAlternativeNames. È possibile utilizzare i cmdlet <STRONG>Get-CsCertificate</STRONG> , <STRONG>Request-</STRONG>CsCertificate e <STRONG>Set-CsCertificate</STRONG> per visualizzare alcune informazioni e richiedere e assegnare certificati. Questo tuttavia non è il metodo migliore da utilizzare in caso di dubbi sulle proprietà dei nomi alternativi soggetto del certificato corrente. Per visualizzare il certificato e tutti i membri proprietà, è consigliabile utilizzare lo snap-in Certificati della <EM>Microsoft Management Console (MMC)</EM> o la Distribuzione guidata di Lync Server. Nella Distribuzione guidata di Lync Server è possibile visualizzare le proprietà del certificato mediante la Configurazione guidata certificati. Le procedure per la visualizzazione, la richiesta e l'assegnazione di un certificato tramite Lync Server Management Shell e la <EM>Microsoft Management Console (MMC)</EM> sono descritte in dettaglio nelle procedure seguenti. Per utilizzare la Distribuzione guidata di Lync Server, vedere i dettagli qui presenti se è stato distribuito il pool di server Server Director o il pool di server Director facoltativo: <A href="lync-server-2013-configure-certificates-for-the-director.md">Configurare i certificati per il server Director in Lync Server 2013</A>. Per il Front End Server o il pool Front End, vedere i dettagli in: <A href="lync-server-2013-configure-certificates-for-servers.md">Configurare i certificati per i server in Lync Server 2013</A><BR>I passaggi iniziali di questa procedura sono passaggi di preparazione e orientamento nella scelta del ruolo svolto dai certificati correnti. Per impostazione predefinita, nei certificati è presente una voce lyncdiscover.&lt;dominiosip&gt; o lyncdiscoverinternal.&lt;nome dominio interno&gt; solo se in precedenza si sono installati i servizi Mobility o si sono preparati i certificati in anticipo. Questa procedura utilizza il nome di dominio di esempio "contoso.com" e il nome di dominio interno di esempio "contoso.net".<BR>La configurazione predefinita per i certificati in Lync Server 2013 e Lync Server 2010 prevede l'utilizzo di un unico certificato (denominato "Default") con gli scopi Default (per tutti gli scopi ad eccezione dei servizi Web), WebServicesExternal e WebServicesInternal. Una configurazione facoltativa prevede l'uso di un certificato separato per ogni scopo. Per gestire i certificati è possibile utilizzare i cmdlet di Lync Server Management Shell e Windows PowerShell o la Configurazione guidata certificati della Distribuzione guidata di Lync Server.



## Per aggiornare i certificati con nuovi nomi alternativi soggetto utilizzando Lync Server Management Shell

1.  Accedere al computer con un account con diritti e autorizzazioni di amministratore locale.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Individuare i certificati assegnati al server e i relativi tipi di utilizzo. Queste informazioni sono necessarie nel passaggio successivo per assegnare il certificato aggiornato. Nella riga di comando digitare:
    
        Get-CsCertificate

4.  Controllare l'output del passaggio precedente per scoprire se un certificato singolo è assegnato a più utenti oppure se sono assegnati certificati diversi per ogni uso. Esaminare il parametro Use per individuare la modalità di utilizzo di un certificato. Confrontare il parametro Thumbprint per i certificati visualizzati per stabilire se lo stesso certificato presenta più utilizzi.

5.  Aggiornare il certificato. Nella riga di comando digitare:
    
        Set-CsCertificate -Type <type of certificate as displayed in the Use parameter> -Thumbprint <unique identifier>
    
    Ad esempio, se il cmdlet **Get-CsCertificate** visualizza un certificato con Use Default, un altro con Use WebServicesInternal e un altro con Use WebServicesExternal, e se tutti i certificati hanno lo stesso valore Thumbprint, nella riga di comando digitare:
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
    
    **Importante:**
    
    Se viene assegnato un certificato separato per ogni uso (il valore Thumbprint è diverso per ogni certificato), è importante non eseguire il cmdlet **Set-CsCertificate** con più tipi. In questo caso, eseguire il cmdlet **Set-CsCertificate** separatamente per ogni utilizzo. Ad esempio:
    
        Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
        Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>

6.  Per visualizzare il certificato, fare clic sul pulsante **Start**, scegliere **Esegui…** e digitare MMC per aprire la Microsoft Management Console.

7.  Dal menu MMC scegliere **File**, **Aggiungi/Rimuovi snap-in…**, Certificati. Fare clic su **Aggiungi**. Quando richiesto, selezionare **Account del computer** e quindi fare clic su **Avanti**.

8.  Se il certificato si trova nel computer in uso, selezionare **Computer locale**. Se il certificato si trova in un altro computer, selezionare **Altro computer**, digitare il nome di dominio completo del computer o fare clic su **Sfoglia**. In **Immettere il nome dell'oggetto da selezionare** digitare il nome del computer. Fare clic su **Controlla nomi**. Dopo la risoluzione, il nome del computer viene sottolineato. Fare clic su **OK** e quindi su **Fine**. Fare clic su **OK** per eseguire il commit della selezione e chiudere la finestra di dialogo **Aggiungi/Rimuovi snap-in**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se il certificato non viene visualizzato nella console, verificare di non avere selezionato Utente o Servizio. È necessario selezionare Computer, altrimenti non sarà possibile individuare il certificato corretto.</td>
    </tr>
    </tbody>
    </table>


9.  Per visualizzare le proprietà del certificato, espandere **Certificati**, espandere **Personali** e selezionare **Certificati**. Selezionare il certificato da visualizzare, fare clic con il pulsante destro del mouse sul certificato e scegliere **Apri**.

10. Nella visualizzazione **Certificati** selezionare **Dettagli**. Da qui è possibile scegliere il nome soggetto certificato selezionando **Soggetto**. Verranno visualizzati il nome soggetto assegnato e le proprietà associate.

11. Per visualizzare i nomi alternativi soggetto, selezionare **Nome alternativo soggetto**. Verranno visualizzati tutti i nomi alternativi soggetto. Per impostazione predefinita, i nomi alternativi soggetto trovati nella proprietà sono di tipo **Nome DNS**. Dovrebbero essere visibili i membri seguenti, tutti nomi di dominio completi rappresentati nei record host DNS (A o, se IPv6, AAAA):
    
      - Nome pool per il pool, o nome del singolo server, se non è un pool
    
      - Nome del server a cui è assegnato il certificato
    
      - Record URL semplici, di solito meet e dialin
    
      - Nomi servizi Web interni e servizi Web esterni (ad esempio, webpool01.contoso.net, webpool01.contoso.com) in base alle scelte effettuate nel Generatore di topologie e ai servizi Web selezionati per la sostituzione.
    
      - Se già assegnati, i record lyncdiscover.\<dominiosip\> e lyncdiscoverinternal.\<dominiosip\>.
    
    L'ultimo elemento è il più interessante: la presenza di una voce relativa al nome alternativo soggetto lyncdiscover e lyncdiscoverinternal.
    
    Dopo aver trovato questa informazione, si può chiudere la visualizzazione certificato e la MMC.

12. Se un nome alternativo soggetto (lyncdiscover.\>nome dominio\> e lyncdiscoverinternal.\<nome dominio\> in base al tipo di certificato esterno o interno) del servizio di individuazione automatica risulta mancante e si utilizza un unico certificato predefinito per i tipi Default, WebServicesInternal e WebServiceExternal, eseguire le operazioni seguenti:
    
      - Al prompt dei comandi di Lync Server Management Shell digitare:
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        Se ci sono molti domini SIP, non si può utilizzare il parametro AllSipDomain, è invece necessario utilizzare il parametro DomainName. Quando si utilizza il parametro DomainName, è necessario definire il nome FQDN per i record lyncdiscoverinternal e lyncdiscover. Ad esempio:
        
            Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - Per assegnare il certificato, digitare:
        
            Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        Dove "Thumbprint" è l'identificazione digitale visualizzata per il certificato appena rilasciato.

13. Per un nome alternativo soggetto del servizio di individuazione automatica interno mancante, se si utilizzano certificati separati per i tipi Default, WebServicesInternal e WebServicesExternal, eseguire le operazioni seguenti:
    
      - Al prompt dei comandi di Lync Server Management Shell digitare:
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -AllSipDomain -verbose
        
        Se sono presenti più domini SIP non è possibile utilizzare il nuovo parametro AllSipDomain, ma è invece necessario utilizzare il parametro DomainName. Quando si utilizza il parametro DomainName è necessario utilizzare un prefisso appropriato per l'FQDN del dominio SIP. Ad esempio:
        
            Request-CsCertificate -New -Type WebServicesInternal -Ca dc\myca -DomainName "LyncdiscoverInternal.contoso.com, LyncdiscoverInternal.contoso.net" -verbose
    
      - Per un nome alternativo soggetto del servizio di individuazione automatica esterno, nella riga di comando digitare:
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -AllSipDomain -verbose
        
        Se sono presenti più domini SIP non è possibile utilizzare il nuovo parametro AllSipDomain, ma è invece necessario utilizzare il parametro DomainName. Quando si utilizza il parametro DomainName è necessario utilizzare un prefisso appropriato per l'FQDN del dominio SIP. Ad esempio:
        
            Request-CsCertificate -New -Type WebServicesExternal -Ca dc\myca -DomainName "Lyncdiscover.contoso.com, Lyncdiscover.contoso.net" -verbose
    
      - Per assegnare i tipi di certificato singoli, digitare:
        
            Set-CsCertificate -Type Default -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesInternal -Thumbprint <Certificate Thumbprint>
            Set-CsCertificate -Type WebServicesExternal -Thumbprint <Certificate Thumbprint>
        
        Dove "Thumbprint" è l'identificazione digitale visualizzata per i singoli certificati appena rilasciati.

