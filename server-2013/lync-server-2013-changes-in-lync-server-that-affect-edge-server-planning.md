---
title: "Lync Server 2013: Modifiche in LS che limitano pianificaz. server perimetr."
TOCTitle: Modifiche introdotte in Lync Server 2013 che incidono sulla pianificazione dei server perimetrali
ms:assetid: 66305160-c9b8-4bc4-9f24-8ee8d9a294f7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204965(v=OCS.15)
ms:contentKeyID: 49300809
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifiche introdotte in Lync Server 2013 che incidono sulla pianificazione dei server perimetrali

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Lync Server 2013 introduce nuove funzionalità che estendono le caratteristiche e metodi di comunicazione per gli utenti. Inoltre, Lync Server 2013 introduce modifiche ai servizi esistenti per integrare meglio ed estendere i servizi disponibili nell'organizzazione. Di seguito è disponibile un riepilogo delle modifiche che potrebbero incidere sulla pianificazione e la distribuzione dei servizi Lync Server 2013  server perimetrale.

## Supporto dell'indirizzamento IPv6

Lync Server 2013 supporta l'indirizzamento IPv6 per tutti i servizi del server perimetrale. Se sono stati specificati gli indirizzi IPv6 per le interfacce tramite la configurazione in Windows Server, è possibile utilizzare gli indirizzi IPv6 nella configurazione del server perimetrale tramite la configurazione degli indirizzi IP in Generatore di topologie. Anche il protocollo XMPP (Extensible Messaging and Presence Protocol) supporta IPv6 e non è necessaria alcuna configurazione aggiuntiva. Se IPv6 è configurato nella topologia, XMPP utilizzerà IPv6 quando richiesto.

Un requisito aggiunto per il supporto di IPv6 in Lync Server 2013 prevede la creazione di record DNS (Domain Name System) per i record che devono essere individuati e risolti in un indirizzo IPv6. Il sistema DNS IPv6 utilizza record host definiti **AAAA** e chiamati "quad-A". Gli altri tipi di record sono coerenti con le controparti IPv4.

## Supporto della distribuzione del protocollo XMPP (Extensible Messaging and Presence Protocol)

Nel server perimetrale viene introdotto un proxy XMPP totalmente integrato (distribuito nei server perimetrali) e un gateway XMPP (distribuito nei Front End Server). È possibile distribuire la federazione XMPP come componente facoltativo. Tramite l'aggiunta e la configurazione del proxy XMPP e del gateway XMPP, è possibile consentire agli utenti di Microsoft Lync 2013 di aggiungere contatti da partner XMPP per la messaggistica istantanea e la presenza.


> [!NOTE]
> Attualmente i servizi XMPP nel server perimetrale forniscono solo funzionalità di messaggistica istantanea e presenza tra i client Lync Server e i contatti XMPP. Il protocollo XMPP, inoltre, è ospitato in un solo sito.



> [!IMPORTANT]  
> La funzionalità XMPP di Lync Server 2013 è testata e supportata da Microsoft per la federazione di messaggistica istantanea con Google Talk. Per altri sistemi XMPP, contattare il fornitore di terze parti per verificare l'eventuale supporto della federazione con Lync Server 2013 e per indicazioni per la distribuzione o la risoluzione dei problemi.

## Supporto della distribuzione di certificati di autenticazione audio/video e di autenticazione server-server

I certificati vengono utilizzati per generare token rilasciati ai client e altri consumer del servizio di autenticazione A/V e per l'autenticazione server-server. Il certificato di autenticazione audio/video è di tipo *AudioVideoAuthentication* e il certificato di autenticazione server-server è di tipo *OAuthTokenIssuer* .

Per l'autenticazione audio/video, i token vengono utilizzati per autenticare le richieste di allocazione della porta e vengono memorizzati nella cache per un massimo di 8 ore, ovvero la durata predefinita del token. In condizioni operative normali, questo è un metodo molto affidabile per creare e distribuire il materiale di autenticazione ai consumer del servizio A/V. I certificati, tuttavia, hanno una durata definita e una data e ora di scadenza prestabilite, in base alla data di creazione e ai criteri applicati dall'Autorità di certificazione che ha creato il certificato, solitamente 2 anni per questo tipo di certificato. Alla scadenza del certificato, qualsiasi token creato dal certificato scaduto e memorizzato nella cache dai consumer diventa non valido. Qualsiasi tentativo di utilizzare un token creato con un certificato scaduto risulterebbe in errori di allocazione Media Relay e causerebbe l'interruzione di qualsiasi sessione audio/video corrente. A questo punto, il client dovrebbe acquisire un nuovo token creato da un certificato valido per riprendere le normali funzionalità audio e video.

L'autenticazione server-server è gestita da un certificato globale richiesto e applicato in tutti i server della distribuzione. Il certificato è responsabile per l'autenticazione dei server in Lync Server 2013, nonché per l'autenticazione in Exchange 2013 e Microsoft SharePoint Server 2013. Per ulteriori informazioni sul funzionamento dell'autenticazione server-server, vedere [Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md). Una differenza molto importante tra il processo di autenticazione audio/video e il processo di autenticazione server-server è la durata dell'autenticazione, ovvero dei token. Nel caso dell'autenticazione audio/video, la scadenza è dopo 8 ore, mentre la durata dell'autenticazione server-server è di 24 ore. È necessaria una pianificazione corrispondente in base al tipo di certificato.

Una novità di Lync Server 2013 è la possibilità di distribuire un certificato di autenticazione audio/video e di autenticazione server-server, prima della scadenza del certificato corrente. Il nuovo certificato viene così utilizzato per generare i nuovi token o gestire le nuove richieste di autenticazione, mentre quello precedente viene mantenuto per le sessioni e le autenticazioni correnti. Il vantaggio di questa nuova funzionalità è quello di evitare quasi tutti gli errori causati dalla scadenza di token e certificati. Per informazioni dettagliate su questa funzionalità e su come configurarla, vedere [Gestione temporanea dei certificati AV e OAuth utilizzando -Roll in Set-CsCertificate in Lync Server 2013](lync-server-2013-staging-av-and-oauth-certificates-using-roll-in-https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsCertificate)

## Minore dipendenza dall'affinità basata su cookie

Nelle versioni precedenti di Lync Server e Office Communications Server, l'affinità basata su cookie viene utilizzata dai servizi Web per assicurare il mantenimento dello stato di sessione dei servizi Web e dei client. I servizi Web di Lync Server 2013 utilizzano un meccanismo di affinità incorporato che elimina la maggior parte dei requisiti relativi all'affinità basata su cookie.


> [!WARNING]
> Il client Microsoft Lync 2010 Mobile deve comunque utilizzare l'affinità basata su cookie e renderà necessario configurare tale affinità fino al completamento della migrazione di tutti i client al futuro client Microsoft Lync Mobile (data di rilascio non ancora stabilita).



Per informazioni dettagliate sull'affinità basata su cookie per Lync Server 2013, vedere [Componenti necessari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-components-required-for-external-user-access.md).

## Miglioramenti dell'individuazione automatica

La funzionalità di individuazione automatica in Lync Server 2013 consente ai client di individuare le funzionalità aggiuntive rese disponibili per le comunicazioni. L'individuazione automatica è stata introdotta per la prima volta nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011 per la mobilità e Microsoft Lync 2010 Mobile. La funzionalità di individuazione automatica (nota anche con i nomi di record DNS LyncDiscover e LyncDiscoverInternal) consente ai client di individuare e utilizzare i servizi di mobilità (per i client Microsoft Lync 2010 Mobile), Microsoft Lync Web App e Lync Web Scheduler, nonché le comunicazioni con Microsoft Exchange Server w SharePoint Server. Questa funzionalità viene installata durante la normale installazione e distribuzione dell'infrastruttura e dei server Lync Server 2013. Con Generatore di topologie e Distribuzione guidata di Lync Server viene eliminata la maggior parte delle attività di configurazione richiesta nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Servizi per i client mobili

Introdotti nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011, i servizi di mobilità in Lync Server 2013 consentono ai cellulari che eseguono Lync Mobile e i dispositivi tablet che utilizzano dispositivi mobili supportati Apple iOS, Android, Windows Phone o Nokia di eseguire attività come l'invio e la ricezione di messaggi istantanei, la visualizzazione dei contatti e la visualizzazione della presenza. I dispositivi mobili supportano inoltre alcune funzionalità VoIP aziendale, tra cui la possibilità di partecipare a una conferenza mediante clic del mouse, la chiamata tramite ufficio, il numero unico, la segreteria telefonica e la notifica di chiamate senza risposta.


> [!NOTE]
> I servizi di mobilità utilizzano il proxy inverso e i servizi pubblicati distribuiti nel Front End Server. Non sono necessarie modifiche per i server perimetrali. Come minimo è necessaria la configurazione SIP/TCP/5061 in uscita dal server che esegue il servizio Access Edge di Lync Server.



## Il ruolo Director è facoltativo

Il ruolo del server Server Director nella topologia di Lync Server 2013 non è cambiato e viene ancora utilizzato per l'hosting dei servizi Web, la preautenticazione delle richieste utente in arrivo e l'indirizzamento degli utenti esterni al pool principale. Con la modifica del Server Director da ruolo consigliato a ruolo facoltativo, Microsoft non intende sminuire il valore del Server Director. Lo scopo è quello di ridurre il numero di server e altri requisiti hardware (ad esempio, i servizi di bilanciamento del carico hardware per il Server Director) senza limitare caratteristiche e funzionalità. Dato che i Front End Server possono svolgere le stesse funzioni del Server Director senza effetti negativi sui servizi forniti, è possibile distribuire server Director se lo si preferisce. È possibile escludere in tutta sicurezza il ruolo Server Director confidando sul fatto che i Front End Server offriranno gli stessi servizi in sostituzione di un Server Director.

