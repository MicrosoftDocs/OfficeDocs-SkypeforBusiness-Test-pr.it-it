---
title: 'Lync Server 2013: Scenari per i proxy inversi'
TOCTitle: Scenari per i proxy inversi
ms:assetid: 13108f59-a660-4ff1-8404-079d1cb646f2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204691(v=OCS.15)
ms:contentKeyID: 49299752
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Scenari per i proxy inversi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-01-21_

I proxy inversi sono necessari in Lync Server 2013 per fornire l'accesso ai servizi e alle risorse, ad esempio URL semplici per le riunioni e l'accesso esterno, rubrica, contenuto delle riunioni, espansione della lista di distribuzione e servizi per dispositivi mobili. Nello scenario tipico di proxy inverso in Lync Server 2013, i client esterni (ad esempio, il client desktop o il client Lync Web App) possono accedere ai servizi Web esterni di Server Director o Front End Server.

**Proxy inverso e servizi Web esterni**

![Proxy inverso e servizi Web esterni](images/JJ204932.13142405-d5c9-45b7-a8b7-a8c89f09c97c(OCS.15).jpg "Proxy inverso e servizi Web esterni")

Durante la fase di pianificazione è necessario definire i requisiti per il proxy inverso in una distribuzione di Lync Server 2013. Il proxy inverso consente di accedere alle funzionalità per i client esterni seguenti:

  - Client desktop Microsoft Lync 2013

  - Microsoft Lync Web App

  - Microsoft Lync Mobile

  - app Windows Store Lync

Durante la fase di pianificazione della distribuzione di Lync Server 2013, vengono mappati i requisiti effettivi per le funzionalità proxy inverso in Lync Server 2013.

1.  I client esterni si connetteranno al proxy inverso sulla porta TCP 443 e utilizzeranno SSL (Secure Sockets Layer) o TLS (Transport Layer Security). I client Microsoft Lync Mobile possono connettersi alla porta TCP 80, ma solo quando eseguono la connessione iniziale ai servizi di individuazione di Lync e l'amministratore ha configurato i record CNAME (o alias) corretti del DNS (Domain Name system) e accetta che la comunicazione non sia crittografata.

2.  I servizi Web esterni di Lync Server 2013 (distribuiti in Front End Server e/o Server Director) prevedono una connessione da un proxy inverso sulla porta TCP 4443 e che tale connessione sia SSL/TLS.
    
    > [!important]  
    > Le porte di attesa consigliate per i servizi Web sterni sono TCP 8080 per il traffico HTTP e TCP 4443 per il traffico HTTPS. Generatore di topologie offre la possibilità di sostituire i valori predefiniti e definire le proprie porte di attesa per i servizi Web esterni. È importante notare che il proxy inverso comunica con i servizi Web esterni e i client esterni comunicano con il proxy inverso. Il client esterno comunica con il proxy inverso sulla porta TCP 443, ma è possibile ridefinire su quale porta il proxy inverso comunica con i servizi Web esterni. Le opzioni in Generatore di topologie per sostituire le porte di attesa predefinite per i servizi Web consentono di risolvere i conflitti di porta di attesa che potrebbero verificarsi nell'infrastruttura.

3.  Per i servizi Web esterni di Lync Server 2013 è prevista un'intestazione host non modificata dal client per identificare il servizio e la directory server Web che il client sta tentando di utilizzare. Le richieste dovrebbero essere visualizzate come se provenissero dal proxy inverso

4.  I servizi Web esterni utilizzano directory virtuali del server Web (vDir) definite che forniscono i servizi offerti agli utenti. I servizi Web specifici identificabili dall'esterno sono:
    
      - vDir "Meet" per le riunioni in conferenza Web
    
      - vDir "Dialin" per l'accesso telefonico e la conferenza telefonica
    
      - vDir "AutoDiscover" per app Windows Store Lync, Lync Mobile e il client desktop di Lync 2013. L'individuazione automatica in Lync Server 2013 è nota con il nome DNS "lyncdiscover"
    
      - È possibile accedere ai servizi non definiti tramite il client esterno con chiamate dirette ai servizi Web esterni. È ad esempio possibile accedere all'espansione dei gruppi di distribuzione (DLX) e al servizio Rubrica (ABS) tramite chiamate dirette ai servizi Web esterni e alle directory vDir associate. Il client conosce il percorso della directory vDir e crea un URL (Uniform Record Locator) basato su queste informazioni. Il client accederà al servizio Rubrica utilizzando un URL simile a `https://externalweb.contoso.com/abs/handler`
    
      - Il Server Office Web Apps quando la conferenza è definita e configurata come parte della topologia di Lync Server
        

        > [!NOTE]
        > Il Server Office Web Apps è un server ruolo distinto e non è configurato come parte dei servizi Web esterni. Il server viene pubblicato separatamente per l'accesso client.



5.  Definire il bridging SSL per ogni servizio. La porta esterna TCP 443 è mappata alla porta TCP 4443 dei servizi Web esterni. Per HTTP non crittografato, la porta TCP 80 è mappata alla porta TCP 8080 dei servizi Web esterni

6.  Pianificare la pubblicazione delle risorse server Web da parte dei listener proxy inverso

7.  Richiedere e configurare il certificato per il proxy inverso in base ai servizi che verranno offerti. Se configurato con i nomi alternativi del soggetto corretti, questo certificato può essere condiviso da tutti i listener configurati nel server proxy inverso

Risorse disponibili per la pianificazione della distribuzione del proxy inverso:

  - [Raccolta dati in Lync Server 2013](lync-server-2013-data-collection.md)

  - [Riepilogo dei certificati - proxy inverso in Lync Server 2013](lync-server-2013-certificate-summary-reverse-proxy.md)

  - [Riepilogo delle porte - proxy inverso in Lync Server 2013](lync-server-2013-port-summary-reverse-proxy.md)

  - [Riepilogo di DNS - proxy inverso in Lync Server 2013](lync-server-2013-dns-summary-reverse-proxy.md)

