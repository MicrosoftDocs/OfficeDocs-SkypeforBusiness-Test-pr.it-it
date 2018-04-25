---
title: 'Lync Server 2013: Routing della messaggistica unificata di Exchange ospitata'
TOCTitle: Routing della messaggistica unificata di Exchange ospitata
ms:assetid: 6c90dc8b-6aef-4ce8-b483-37c7b5a553c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398512(v=OCS.15)
ms:contentKeyID: 49300892
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Routing della messaggistica unificata di Exchange ospitata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

L'applicazione di routing di Messaggistica unificata di Exchange viene eseguita nel Front End Server per il routing delle chiamate a una distribuzione di messaggistica unificata di Microsoft Exchange Server locale o al servizio Messaggistica unificata di Exchange ospitato.

## Applicazione di routing della messaggistica unificata di Exchange

L'applicazione di routing della messaggistica unificata di Exchange per Lync Server 2013Messaggistica unificata di Exchange utilizza le informazioni tratte dalle impostazioni degli account utente e dai parametri dei criteri di segreteria telefonica ospitata per determinare come eseguire il routing delle chiamate per la messaggistica vocale ospitata, come illustrato nel diagramma seguente.

**Esempio di routing della messaggistica unificata di Exchange con distribuzione mista**

![Distribuzione della messaggistica unificata di Exchange con Lync Server in locale](images/Gg398512.75258286-1f23-487b-bf46-d8538e7d540e(OCS.15).jpg "Distribuzione della messaggistica unificata di Exchange con Lync Server in locale")

È possibile configurare il routing di Messaggistica unificata di Exchange per eseguire il routing delle chiamate a utenti abilitati per Messaggistica unificata di Exchange , a utenti abilitati per il servizio di Messaggistica unificata di Exchange ospitato, o per una combinazione di entrambe.

Si supponga, ad esempio, che la cassetta postale di Roy e il servizio di Messaggistica unificata di Exchange siano ospitati in una distribuzione di Exchange locale.

  - Le informazioni sull'indirizzo proxy dell'account utente di Roy vengono utilizzate dall'applicazione di routing della messaggistica unificata di Exchange per eseguire il routing delle sue chiamate a un server di Messaggistica unificata di Exchange.

La cassetta postale di Alice e il servizio di Messaggistica unificata di Exchange si trovano nel data center di un provider di servizi di Exchange ospitati. Il routing per le sue chiamate di Messaggistica unificata di Exchange viene configurato nel modo seguente:

  - Il valore impostato nell'attributo msExchUCVoiceMailSettings dell'account utente di Alice indica all'applicazione di routing della messaggistica unificata di Exchange di controllare i dettagli relativi al routing in criteri di segreteria telefonica ospitata.
    

    > [!NOTE]
    > Il valore dell'attributo msExchUCVoiceMailSettings può essere impostato dal provider di servizi di Exchange o dall'amministratore di Lync Server 2013. Nell'esempio illustrato nel diagramma precedente il valore (CsHostedVoiceMail=1) è stato impostato dall'amministratore di Lync Server 2013 per abilitare la segreteria telefonica ospitata per Alice. Per informazioni dettagliate su questo attributo, vedere <A href="lync-server-2013-hosted-exchange-user-management.md">Gestione di utenti di Exchange ospitati in Lync Server 2013</A>.



  - I criteri di segreteria telefonica ospitata assegnati all'account utente di Alice offrono informazioni dettagliate sul routing:
    
      - La destinazione corrisponde al provider di servizi di Messaggistica unificata di Exchange (in questo esempio, .ExUm. *\<ExchangeServerOspitato\>* .com).
    
      - Le organizzazioni sono identificate dagli ID tenant, che corrispondono agli FQDN di routing per i messaggi SIP per i tenant di Exchange Server che si trovano in ls.ExUm. *\<ServerExchangeOspitato\>* .com (in questo esempio, corp.contoso.com e corp.litwareinc.com).
        

        > [!NOTE]
        > L'FQDN di Exchange Online è exap.um.outlook.com.

        
        Per informazioni dettagliate, vedere [Criteri di segreteria telefonica ospitata in Lync Server 2013](lync-server-2013-hosted-voice-mail-policies.md).


> [!NOTE]
> Se l'attributo msExchUCVoiceMailSettings e le impostazioni dell'indirizzo proxy di messaggistica unificata sono entrambi presenti in un account utente, l'attributo msExchUCVoiceMailSettings ha la precedenza.


