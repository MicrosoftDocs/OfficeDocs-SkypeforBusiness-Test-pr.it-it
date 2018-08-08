---
title: "Lync Server 2013: FAQ: Provisioning della connettività Lync Server per Skype"
TOCTitle: 'Domande frequenti: provisioning della connettività Lync Server per Skype'
ms:assetid: 4d1b2bfc-780b-4b8c-afd5-11c2e59203b5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn440172(v=OCS.15)
ms:contentKeyID: 59602734
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Domande frequenti: provisioning della connettività Lync Server 2013 per Skype

 

_**Ultima modifica dell'argomento:** 2015-07-22_

**D: Quali funzionalità sono supportate tra Microsoft Lync e Skype?**

**R:** Con l'arrivo di Skype nella famiglia Microsoft nascono nuove possibilità di estendere gli scenari delle comunicazioni unificate a centinaia di milioni di utenti Skype. Questa combinazione consentirà ai clienti Lync di connettersi e collaborare con fornitori, clienti e partner sfruttando la ricca dotazione di funzionalità di Lync e la vasta portata di Skype.

  - Messaggi istantanei e chiamate audio e video: chiamate audio e video e messaggistica istantanea federata tra utenti di Lync e Skype

  - Condivisione delle informazioni sulla presenza: scambio di informazioni sulla presenza tra i contatti federati

  - Amministrazione semplificata: impostazioni e controlli per configurare le comunicazioni federate nel rispetto dei criteri e degli standard dell'organizzazione

**D: Quali sono i criteri di idoneità per connettere una distribuzione di Lync a Skype?**

**R:** La connettività Skype è autorizzata se si dispone di una delle seguenti licenze:

  - Lync Server 2010 o 2013 con licenze CAL (Client Access License) Standard per Lync 2010 o 2013 per gli utenti e/o i dispositivi nell'organizzazione che si connetteranno a Skype. 

  - Lync Online (licenze autonome o nell'ambito di una famiglia di prodotti Office 365). Questo servizio (pic.lync.com) è tuttavia riservato esclusivamente al provisioning di Lync Server e delle distribuzioni di Lync Server e Lync Online ibride. Il provisioning PIC di Lync Online viene eseguito nel Pannello di controllo di Lync Online.

**D: Cosa devono fare gli utenti finali di Lync per connettersi ai contatti Skype?**

**R:** Dopo l'attivazione di un dominio e l'abilitazione delle funzionalità da parte di un amministratore di Lync dell'organizzazione, gli utenti di Lync possono aggiungere contatti Skype ai propri elenchi contatti nel client Lync.

**D: Cosa devono fare gli utenti finali di Skype per connettersi ai contatti di Lync?**

**R:** Tutti gli utenti Skype che intendono connettersi a un utente Lync devono disporre di un account Microsoft associato al proprio ID Skype e accedere usando l'account Microsoft. Questa funzionalità può essere abilitata all'interno del client Skype.

**D: È ancora disponibile la federazione con Windows Live?**

**R:** Nel mese di ottobre 2012 Microsoft ha iniziato ad aiutare gli utenti di Windows Live Messenger (WLM) a passare a Skype, in vista del ritiro di WLM. Lync continuerà a supportare la federazione con WLM finché il programma sarà sul mercato, ma non saranno consentite ulteriori attivazioni di domini Windows Live. Lo spostamento degli utenti di WLM è reso possibile da Skype 6.0 per Mac e Windows, rilasciato il 25 ottobre 2012, che consente di accedere con un account Microsoft, ossia utilizzando le stesse credenziali di WLM. Quando si accede a Skype, l'elenco degli amici di WLM viene trasferito automaticamente. Utilizzando Skype, gli utenti possono sfruttare le funzionalità di comunicazione estese di Skype, tra cui la possibilità di chiamare su numeri di rete fissa e cellulari, la condivisione dello schermo, le chiamate di gruppo e il supporto di un'ampia gamma di dispositivi. Inoltre, i contatti federati di Lync degli utenti di WLM seguiranno la transizione a Skype insieme al resto degli elenchi di amici, e la messaggistica istantanea tra Skype e Lync per questi contatti sarà disponibile immediatamente. Gli utenti di Lync non devono eseguire alcuna operazione, poiché la continuità del servizio è automatica.

**D: È ancora disponibile la federazione con Yahoo\! o AOL?**

**R:** La federazione con Yahoo\! e AOL sta per essere terminata per gli utenti di Lync (e di Office Communications Server). La capacità di Microsoft di fornire questi servizi è sempre stata subordinata al supporto offerto da Yahoo\! e AOL, che sono entrambi in fase di risoluzione del contratto. Sia per Yahoo\! che per AOL il servizio continuerà fino a giugno 2014.

  - Yahoo\!: il servizio continuerà fino a giugno 2014 e gli utenti dovranno sempre disporre di una licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync ("PIC USL"). Dal 1 settembre 2012 questa licenza non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. Gli utenti con licenze acquistate prima di questa data potranno continuare a usufruire della federazione con Yahoo\! fino alla data di chiusura del servizio o alla scadenza del contratto di licenza. Gli utenti con contratti di licenza PIC che si estendono oltre il 30 giugno 2014 riceveranno un credito proporzionato all'importo dei pagamenti relativi al periodo di tempo successivo al 30 giugno 2014.

  - AOL: a partire dal 30 giugno 2014, il servizio di connettività per messaggistica istantanea pubblica ("PIC") di Lync non sarà più disponibile. Per limitare i disagi causati del termine del servizio, Microsoft ha interrotto il provisioning di domini utente aggiuntivi. Fino al 30 giugno 2014 gli utenti possono continuare a supportare le comunicazioni federate con AIM senza variazioni. Oltre quella data (o per gli utenti che desiderano eseguire il provisioning di domini aggiuntivi nel frattempo), sarà disponibile un servizio sostitutivo direttamente da AOL. Per altre informazioni sul nuovo servizio di AOL, vedere <http://aimenterprise.aol.com/pic.php>  (verrà aperta una nuova pagina su AOL.com).  

**D: È possibile provare la connettività Skype prima di acquistare Lync?**

**R:** La connettività Skype non viene offerta in prova. I clienti Lync in possesso delle licenze idonee sono invece invitati a eseguire l'iscrizione al servizio per testarlo.

**D: Quali informazioni sono richieste per il provisioning?**

**R:** Per inviare una richiesta di provisioning con una licenza idonea, è necessario quanto segue:

  - Numero del contratto Microsoft:
    
      - Supporto di contratti multilicenza Microsoft: numero del contratto multilicenza Microsoft
    
      - Microsoft Partner Network: ID partner sede centrale
    
      - Service Provider Licensing Agreement: numero di iscrizione iniziale
    
      - Servizi per volumi elevati: numero di iscrizione al prodotto

  - Nomi di dominio completi (FQDN) per il servizio Access Edge.
    
      - È richiesto l'FQDN per almeno un servizio Access Edge.
    
      - Se nell'organizzazione sono presenti più server che eseguono il servizio Access Edge, specificare i FQDN per ogni servizio Access Edge aggiuntivo. Importante: se si desidera modificare un FQDN specificato in precedenza per il servizio Access Edge, il provisioning per la modifica può richiedere diversi giorni e può causare un'interruzione del servizio. Per evitare questo problema, è consigliabile mantenere l'FQDN del servizio Access Edge specificato in precedenza.

  - Dominio/i SIP (Session Initiation Protocol). Si tratta del suffisso di dominio dell'URI SIP attualmente utilizzato dagli utenti per la messaggistica istantanea. Se l'organizzazione include più domini SIP, specificare il suffisso di dominio per ogni dominio utilizzato per la messaggistica istantanea. Ad esempio, per user1@contoso.com specificare contoso.com come dominio SIP e per user1@example.fabrikam.com specificare example.fabrikam.com come dominio SIP.
    

    > [!NOTE]
    > Specificare solo il suffisso di dominio per il dominio SIP. Non specificare alcun FQDN, incluso l'FQDN per il servizio Access Edge, per il dominio SIP.



  - Informazioni di contatto. Specificare l'indirizzo di posta elettronica per l'amministratore di ogni dominio SIP specificato.

**D: Come si abilita la connettività Lync-Skype in uno scenario di dominio condiviso?**

**R:**In uno scenario di dominio condiviso locale con Lync Online 2013 e Lync Server (in cui utenti sia online che locali usano lo stesso dominio SIP), abilitare la connettività Lync-Skype eseguendo questa procedura nell'ordine indicato:

1.  Configurare la connettività Lync-Skype locale come illustrato nella Guida al provisioning PIC.

2.  Attendere la conferma dell'avvenuto provisioning del dominio da parte di Microsoft.

3.  Dopo avere ottenuto la conferma, usare l'interfaccia di amministrazione di Lync per attivare le "comunicazioni esterne". Per altre informazioni, vedere [http://office.microsoft.com/it-it/support/configure-external-communications-HA102817865.aspx?CTT=5\&origin=HA102817356](http://office.microsoft.com/it-it/support/configure-external-communications-ha102817865.aspx?ctt=5%26origin=ha102817356)

Questo ordine è importante. È infatti necessario configurare la connettività locale prima di abilitare le comunicazioni in Lync Online. Se l'ordine viene invertito, le informazioni immesse per la connettività locale all'indirizzo <https://pic.lync.com> non verranno applicate. Se Lync Online è già stato configurato per le comunicazioni esterne con questo dominio, è necessario disattivarlo, attendere 24 ore e ricominciare, immettendo innanzitutto le informazioni locali all'indirizzo <https://pic.lync.com> e quindi attivando le comunicazioni esterne per Lync Online.

**D: È possibile eseguire il provisioning di più FQDN di servizi Access Edge per la connettività Skype?**

**R:** È possibile eseguire il provisioning di un massimo di dieci FQDN di servizi Access Edge con ogni richiesta di provisioning.

**D: È possibile ottenere l'elenco degli indirizzi di posta elettronica degli account Microsoft trovati per l'organizzazione che richiede il provisioning?**

**R:** No. Questi indirizzi sono considerati informazioni personali e non vengono condivisi.

**D: Come è possibile aggiungere un contatto Windows Live Messenger il cui ID contiene un dominio diverso da quelli supportati da Windows Live?**

**R:** Se si aggiunge un utente Windows Live Messenger il cui account o ID include un dominio non Windows Live, immettere l'indirizzo nel formato seguente: \<nome utente\>(\<nome di dominio\>)@msn.com, dove \<nome di dominio\> è il nome di dominio nell'indirizzo di posta elettronica dell'utente. Ad esempio, per aggiungere ugo@contoso.com, usare il formato seguente: ugo(contoso.com)@msn.com. Per un elenco dei domini supportati da Windows Live, vedere la sezione dedicata ai domini supportati nell'articolo relativo ai problemi noti che si verificano con la messaggistica istantanea pubblica dopo avere installato Live Communications Server Service Pack 1, disponibile all'indirizzo http://support.microsoft.com/?kbid=897567.

**D: Quanto tempo richiede il processo di provisioning?**

**R:** Il provisioning può richiedere fino a 30 giorni.

**D: Come si fa a sapere quando il provisioning è terminato?**

**R:** Al termine del provisioning, Microsoft invierà una notifica tramite posta elettronica.

**D: Come è possibile aggiornare i dettagli della configurazione o di contatto inviati?**

**R:** Al termine del provisioning è possibile aggiornare le proprie informazioni sullo stesso sito Web usato per richiedere il provisioning. Immettere il numero di contratto, quindi fare clic su Aggiorna servizio.

