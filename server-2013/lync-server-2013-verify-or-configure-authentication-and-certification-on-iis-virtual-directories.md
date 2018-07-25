---
title: "Lync Server 2013: Verificare o configurare l'autenticazione e la certificazione nelle directory virtuali IIS"
TOCTitle: Verificare o configurare l'autenticazione e la certificazione nelle directory virtuali IIS
ms:assetid: 3ca90be0-1d64-447c-807a-3a2ee3bf625e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429702(v=OCS.15)
ms:contentKeyID: 49300265
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare o configurare l'autenticazione e la certificazione nelle directory virtuali IIS in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-05-25_

Per configurare il certificato nelle directory virtuali di Internet Information Services (IIS) o verificare che il certificato sia configurato correttamente, utilizzare la procedura seguente. Eseguire tale procedura in ogni server che esegue IIS nel pool di Lync Server interno e nei server Server Director o pool di server Director facoltativi.


> [!NOTE]
> La procedura seguente riguarda la richiesta di un certificato combinato utilizzato per tutte le attività di Lync Server, del sito Web interno e del sito Web esterno in IIS. In Lync Server 2010 viene introdotto un set di cmdlet Lync Server Management ShellWindows PowerShell per le attività specifiche di gestione dell'assegnazione, dell'importazione e della richiesta di certificati. La procedura parte dal presupposto che ci sia un'Autorità di certificazione (CA) distribuita internamente in grado di elaborare la richiesta. Se si utilizzano certificati pubblici per le attività di Lync Server o la CA necessita di una richiesta offline, vedere la sintassi dettagliata di questo argomento per informazioni sul parametro –Output . <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Request-CsCertificate">Request-CsCertificate</A>



## Per configurare l'autenticazione e i certificati nelle directory virtuali di IIS

1.  Per completare la procedura seguente, è necessario accedere al computer ( Front End Server o Server Director) in cui i servizi Web sono installati ed essere un amministratore locale. È necessario disporre delle autorizzazioni di **lettura** e **iscrizione** per l'Autorità di certificazione a cui verranno richiesti i certificati, se l'autorità di certificazione è quella dell'organizzazione. Non sono necessarie autorizzazioni per l'Autorità di certificazione se si intende configurare e inviare una richiesta di certificato offline.

2.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **Gestione Internet Information Services (IIS)** .

3.  In **Gestione Internet Information Services (IIS)** selezionare **NomeServer** . In **Visualizzazione funzionalità** selezionare **Certificati server** , fare clic con il pulsante destro del mouse e scegliere **Apri funzionalità** .
    
    > [!tip]  
    > Eventuali certificati assegnati al server appariranno nella visualizzazione delle funzionalità dei certificati server. Se un certificato corrisponde ai requisiti del sito Web esterno in IIS, è possibile riutilizzarlo. Per visualizzare un certificato, fare clic con il pulsante destro del mouse su di esso e scegliere <strong>Visualizza</strong>

4.  Nel Front End Server o Server Director per cui si sta richiedendo il certificato, fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

5.  In Lync Server Management Shell digitare quanto segue:
    
        Get-CsCertificate
    
    L'output è dato da un elenco dei certificati attualmente presenti nel server nell'archivio certificati personali del computer. Si noti che nel caso di un certificato combinato, in cui i servizi Web interni ed esterni predefiniti utilizzano lo stesso certificato, il valore della proprietà Use sarà Default, WebServicesInternal e WebServicesExternal. Inoltre, la proprietà Thumbprint sarà uguale per ogni tipo di Use. Di seguito viene mostrato un output di esempio per Get-CsCertificate.
    
    ![Informazioni Get-CsCertificate sullo stato del certificato corrente](images/Gg429702.664f6326-6cd5-48e2-8235-fc3950ea43b4(OCS.15).jpg "Informazioni Get-CsCertificate sullo stato del certificato corrente")

6.  In Lync Server Management Shell digitare quanto segue:
    
        Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -CA <CA Server FQDN\CA Instance> -Verbose -DomainName "<FQDN entries to be added to the Subject Alternative Name>"
    
    Dove il comando completo sarà simile all'esempio seguente:
    
        Request-CsCertificate -New -Type Default,WebServicesInternal,WebServicesExternal -CA dc01.contoso.net\contoso-DC01-CA -Verbose -DomainName "LyncdiscoverInternal.Contoso.com,Lyncdiscover.Contoso.com"
    
    > [!tip]  
    > Per impostazione predefinita, Request-CsCertificate inserirà nel nome soggetto il nome del server o del pool e nelle voci del nome soggetto alternativo gli FQDN del server, del pool, degli URL semplici e dei servizi Web interni ed esterni facendo riferimento al documento relativo alla topologia presente nella distribuzione. Se si specifica il parametro –Verbose nel caso di un valore mancante, l'utente verrà informato che i valori calcolati ed effettivi dei nomi alternativi sono diversi, ma non di quali siano i valori mancanti. All'utente viene fornito il valore intero calcolato cui fa riferimento il cmdlet. Utilizzare la stringa dei nomi alternativi calcolati nell'output per richiedere un nuovo certificato che includa tutti i valori.    
    ![Output della richiesta di certificato tramite Request-CsCertifica](images/Gg429702.9e59a657-fa75-4454-8fd3-57c81e829f7b(OCS.15).jpg "Output della richiesta di certificato tramite Request-CsCertifica")

7.  In Lync Server Management Shell digitare quanto segue:
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint <Thumbprint of certificate to use>
    
    Dove il comando completo sarà simile all'esempio seguente:
    
        Set-CsCertificate -Type Default,WebServicesInternal,WebServicesExternal -Thumbprint 466D9BB0E8B928B65AF38FA2D9F41E1B301ECE9D
    
    L'output del cmdlet Set-CsCertificate mostrerà che lo stesso certificato (con identificazione digitale) viene assegnato per l'utilizzo di Default, WebServicesExternal e WebServicesInternal.
    
    ![Output di Set-CsCertificate su IIS WebExt](images/Gg429702.dd451c9d-7b49-4408-8071-c868cb1e678c(OCS.15).jpg "Output di Set-CsCertificate su IIS WebExt")

## Per verificare o configurare l'autenticazione e i certificati nelle directory virtuali di IIS

1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **Gestione Internet Information Services (IIS)** .

2.  In **Gestione Internet Information Services (IIS)** espandere **NomeServer** e quindi **Siti** .

3.  Fare clic con il pulsante destro del mouse su **Lync Server External Web Site** e quindi scegliere **Modifica binding** .

4.  Verificare che https sia associato alla porta 4443 e quindi fare clic su **https** .

5.  Selezionare la voce HTTPS, fare clic su **Modifica** e quindi verificare che il certificato WebServicesExternalCertificate di Lync Server sia associato a questo protocollo. Confrontare l'identificazione digitale fornita dal cmdlet Set-CsCertificate per essere certi che il certificato previsto sia correttamente associato con binding HTTPS.

## Vedere anche

#### Ulteriori risorse

[Get-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsCertificate)  
[Set-CsCertificate](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCertificate)

