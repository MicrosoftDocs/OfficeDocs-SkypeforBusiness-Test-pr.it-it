---
title: Informazioni sull'individuazione automatica
TOCTitle: Informazioni sull'individuazione automatica
ms:assetid: d70a15b7-750b-4e0f-9a7f-0254d6d486c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945654(v=OCS.15)
ms:contentKeyID: 52062449
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Informazioni sull'individuazione automatica

 

_**Ultima modifica dell'argomento:** 2013-06-03_

Il servizio di individuazione automatica di Lync Server 2013 è una caratteristica introdotta in origine in Microsoft Lync Server 2010 all'interno dell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011. Oltre alle correzioni, questo aggiornamento cumulativo offre il supporto per i client Lync Mobile e Lync 2013.

In Lync Server 2013 il servizio di individuazione automatica è parte integrante del funzionamento dei client mobili esterni e interni e l'individuazione automatica viene inoltre estesa ai nuovi client, ad esempio l'app Windows Store Lync per Windows 8 introdotta di recente. L'individuazione automatica viene inoltre utilizzata dai client desktop Lync 2013. L'individuazione automatica viene riconosciuta in Lync Server dai record DNS (Domain Name System) necessari **lyncdiscover.\<dominio\>** e **lyncdiscoverinternal.\<dominio\>**. Le versioni più recenti dei client desktop Lync 2010 e Lync 2013 preferiscono inoltre l'individuazione automatica ai record SRV DNS (Domain Name System) e utilizzano i record SRV DNS solo se lyncdiscover.\<dominio\> o lyncdiscoverinternal.\<dominio\> non risponde o non viene risolto. L'app Windows Store Lync per Windows 8 e Lync Mobile utilizza l'individuazione automatica in modo esclusivo e non farà riferimento ai record SRV DNS tradizionali.

In Lync Server 2013 l'individuazione automatica viene espansa per comunicare al client quali elementi, funzionalità e metodi di comunicazione siano disponibili per il client. Le informazioni vengono comunicate tramite una richiesta inviata dal client e i servizi Web di Lync Server rispondono in modo chiaramente definito indicando ciò che è disponibile per il client e come contattare queste funzionalità utilizzando il documento di risposta di individuazione automatica.

Il modo migliore per comprendere il documento di risposta dell'individuazione automatica, incluso il modo in cui i servizi Web comunicano le funzionalità ai client tramite questo documento, consiste nell'analisi e nella definizione di ogni riga in una risposta tipica del documento di risposta dell'individuazione automatica dei servizi Web di Lync.


> [!NOTE]
> Nei dettagli seguenti l'utente è già stato autenticato dal server principale tramite la risposta a una richiesta di autenticazione.




> [!NOTE]
> Il servizio Web di individuazione automatica di Lync è definito in <STRONG>Microsoft Office Protocols</STRONG> nella sezione <STRONG>Open Specifications</STRONG> di MSDN (<STRONG>Microsoft Developer Network</STRONG>) Library. Per i dettagli, vedere il documento completo sulle specifiche, "Protocollo dei servizi Web di individuazione automatica di Lync", all'indirizzo: <A class=uri href="http://go.microsoft.com/fwlink/?linkid=273839">http://go.microsoft.com/fwlink/?linkid=273839</A>. Per i dettagli sull'autenticazione, vedere "Protocollo dei servizi Web di autenticazione OC" all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=279015">http://go.microsoft.com/fwlink/?linkid=279015</A>.



## Risposta dell'individuazione automatica dei servizi Web di Lync Server

La risposta restituita quando la richiesta dell'individuazione automatica viene inviata è la stessa per un client interno o per uno esterno. Potrebbero variare alcuni parametri con riconoscimento percorso. Se una richiesta client viene ricevuta, ma il pool effettivo è diverso da quello contattato, per ogni utente verrà impostato il rispettivo pool principale. Un collega il cui account utente si trova in un pool diverso, ma che effettua l'accesso dallo stesso ufficio, otterrà una risposta leggermente diversa. La risposta indica il Front End Server o il pool Front End corretto per tale utente.

Esempio di documento di risposta dell'individuazione automatica:

    <AutodiscoverResponse xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" AccessLocation="External">
       <User>
          <SipServerInternalAccess fqdn="pool01.contoso.com" port="5061"/>
          <SipClientInternalAccess fqdn=" pool01.contoso.com" port="443"/>
          <SipServerExternalAccess fqdn="sip.contoso.com" port="5061"/>
          <SipClientExternalAccess fqdn="sip.contoso.com " port="443"/>
          <Link token ="External/Autodiscover" href="https://webexternal.contoso.com/Autodiscover/AutodiscoverService.svc/root"/>
          <Link token="Internal/Autodiscover" href="https://webinternal.contoso.net/Autodiscover/AutodiscoverService.svc/root"/>
          <Link token="External/AuthBroker" href="https://webexternal.contoso.com/Reach/sip.svc"/>
          <Link token="Internal/AuthBroker" href="https://webinternal.contoso.net/Reach/sip.svc"/>
          <Link token="External/WebScheduler" href="https://webexternal.contoso.com/Scheduler"/>
          <Link token="Internal/WebScheduler" href="https://webinternal.contoso.net/Scheduler"/>
          <Link token="External/Mcx" href="https://webexternal.contoso.com/Mcx/McxService.svc"/>
          <Link token="Internal/Mcx" href="https://webexternal.contoso.net/Mcx/McxService.svc"/>
          <Link token="External/Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>
          <Link token="Internal/Ucwa" href="https://webinternal.contoso.net/ucwa/v1/applications"/>
          <Link token="Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>
          <Link token="External/XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>
          <Link token="Internal/XFrame" href="https://webinternal.contoso.net/Autodiscover/XFrame/XFrame.html"/>
          <Link token="XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>
          <Link token="Self" href="https://webexternal.contoso.net/Autodiscover/AutodiscoverService.svc/root/user"/>
       </User>
    </AutodiscoverResponse>

## Dettagli del documento di risposta dell'individuazione automatica

Esistono due formati del documento di risposta dell'individuazione automatica. Il formato predefinito è JSON (JavaScript Object Notation). L'altro formato è un documento XML (Extensible Markup Language). In questo esempio viene utilizzato XML. La richiesta e la risposta sono stimabili perché il documento ha uno schema definito che determina il formato. La riga del documento che descrive lo schema utilizzato è la prima della richiesta o della risposta:

    <AutodiscoverResponse xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" AccessLocation="External">

La definizione di **AccessLocation=”External”** indica che la richiesta è stata creata da un utente esterno.

    <SipServerInternalAccess fqdn="pool01.contoso.com" port="5061"/>

    <SipServerExternalAccess fqdn="sip.contoso.com" port="5061"/>

SipServerInternalAccess e SipServerExternalAccess non vengono attualmente utilizzati. Queste voci sono riservate per un utilizzo futuro.

    <SipClientInternalAccess fqdn=" pool01.contoso.com" port="443"/>

    <SipClientExternalAccess fqdn="sip.contoso.com " port="443"/>

SipClientInternalAccess e SipClientExternalAccess descrivono il nome di dominio completo e la porta che un client interno o esterno utilizzerà per accedere al server SIP definito. Il client desktop Lync e l'app Windows Store Lync utilizzano queste voci in base al percorso (interno o esterno), per trovare il Server Director o il Front End Server.

    <Link token="Internal/Autodiscover" href="https://webinternal.contoso.net/Autodiscover/AutodiscoverService.svc/root"/>

    <Link token ="External/Autodiscover" href="https://webexternal.contoso.com/Autodiscover/AutodiscoverService.svc/root"/>

I riferimenti ad `Autodiscover` contengono i punti di ingresso per il servizio di individuazione automatica. L'attributo token contiene il nome del servizio e l'attributo href è un URL che definisce dove sia possibile trovare il servizio per il client. I client di una rete esterna utilizzano `External/Autodiscover`. Il servizio di individuazione automatica viene installato durante il processo di distribuzione. `Internal/Autodiscover` non è attualmente utilizzato ed è riservato a un utilizzo futuro.

    <Link token="Internal/AuthBroker" href="https://webinternal.contoso.net/Reach/sip.svc"/>

    <Link token="External/AuthBroker" href="https://webexternal.contoso.com/Reach/sip.svc"/>

I riferimenti a `AuthBroker` contengono i punti di ingresso per il servizio broker di autenticazione interno ed esterno: in questo caso, sip.svc. L'attributo token contiene il nome del servizio e l'attributo href è un URL che definisce dove sia possibile trovare il servizio per il client. I client della rete interna utilizzano `Internal/AuthBroker`. I client di una rete esterna utilizzano `External/AuthBroker`. Il servizio AuthBroker viene installato durante il processo di distribuzione dei servizi Web di distribuzione di Lync Server 2013 interni.

    <Link token="Internal/WebScheduler" href="https://webinternal.contoso.net/Scheduler"/>

    <Link token="External/WebScheduler" href="https://webexternal.contoso.com/Scheduler"/>

Il token `WebScheduler` fa riferimento agli URL per l'accesso client alla pianificazione basata sul Web per le conferenze di Lync Server. Attualmente viene utilizzato solo `External/WebScheduler`. WebScheduler viene installato durante il processo di distribuzione dei servizi Web di distribuzione di Lync Server 2013 interni.

    <Link token="Internal/Mcx" href="https://webexternal.contoso.net/Mcx/McxService.svc"/>

    <Link token="External/Mcx" href="https://webexternal.contoso.com/Mcx/McxService.svc"/>

`Internal/Mcx` ed `External/Mcx` sono i percorsi dei servizi Mobility, introdotti nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011. Questi riferimenti continueranno a essere utilizzati da Lync 2010 Mobile in tutti i dispositivi supportati. Il servizio Mcx viene installato durante il processi di distribuzione dei servizi Web di distribuzione di Lync Server 2013 interni.

    <Link token="Internal/Ucwa" href="https://webinternal.contoso.net/ucwa/v1/applications"/>

    <Link token="External/Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>

    <Link token="Ucwa" href="https://webexternal.contoso.com/ucwa/v1/applications"/>

**Internal/Ucwa**, **External/Ucwa** e **Ucwa** consentono ai client di accedere all'API Web Unified Communications (API UCWA o semplicemente UCWA). Le directory virtuali `Internal/Ucwa` ed `External/Ucwa` sono punti di accesso riservati per un futuro miglioramento delle caratteristiche e non vengono utilizzati. La directory virtuale `Ucwa` viene utilizzata per Microsoft Lync Mobile (introdotto con Lync Server 2013) in tutti i dispositivi supportati. Il servizio UCWA viene installato durante il processo di distribuzione dei servizi Web di distribuzione di Lync Server 2013 interni.

    <Link token="Internal/XFrame" href="https://webinternal.contoso.net/Autodiscover/XFrame/XFrame.html"/>

    <Link token="External/XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>

    <Link token="XFrame" href="https://webexternal.contoso.com/Autodiscover/XFrame/XFrame.html"/>

`Internal/XFrame`, **External/XFrame** e **XFrame** forniscono l'accesso per le applicazioni server basate su UCWA. XFrame viene installato durante il processo di distribuzione dei servizi Web di distribuzione di Lync Server 2013 interni.

    <Link token="Self" href="https://webexternal.contoso.net/Autodiscover/AutodiscoverService.svc/root/user"/>

Il token `Self` fa riferimento a informazioni specifiche per il client (tipo di risposta utente) che sta effettuando la richiesta. Il client che ha creato questa richiesta era esterno e il riferimento ad Autodiscover è alla parte utente del servizio di individuazione automatica.

## Vedere anche

#### Ulteriori risorse

[Requisiti di sistema per i componenti per l'accesso degli utenti esterni per Lync Server 2013](lync-server-2013-system-requirements-for-external-user-access-components.md)  
[Pianificazione dell'individuazione automatica](lync-server-2013-planning-for-autodiscover.md)

