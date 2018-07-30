---
title: Utilizzo del comando Start per l'acquisizione dei log da parte del servizio di registrazione centralizzato
TOCTitle: Utilizzo del comando Start per l'acquisizione dei log da parte del servizio di registrazione centralizzato
ms:assetid: 0512b9ce-7f5b-48eb-a79e-f3498bacf2de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687958(v=OCS.15)
ms:contentKeyID: 49887430
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo del comando Start per l'acquisizione dei log da parte del servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Per acquisire i log di traccia utilizzando il servizio di registrazione centralizzato si specifica un comando per iniziare la registrazione in uno o più computer e pool. Si specificano poi i parametri che definiscono i computer o i pool, gli scenari da eseguire (ad esempio AlwaysOn, un altro scenario predefinito oppure uno scenario personalizzato) e i componenti di Lync Server (ad esempio S4, SipStack) da tracciare.

Per acquisire le informazioni giuste è necessario assicurarsi di usare lo scenario corretto per la raccolta di informazioni pertinenti al problema. Nel servizio di registrazione centralizzato uno scenario rappresenta la possibilità di attivare la registrazione in base a un insieme di componenti server, livelli di registrazione e flag, una procedura molto più efficiente rispetto a dover definire questi elementi per ogni server. Si definisce e specifica uno scenario da eseguire, e questo viene eseguito in modo coerente in tutti i server e i pool nell'ambito dell'infrastruttura.

Lo scenario predefinito è denominato **AlwaysOn**. Lo scopo di AlwaysOn, come indicato dal nome, è l'esecuzione costante dello scenario. Lo scenario AlwaysOn raccoglie informazioni a livello Info su molti dei più comuni componenti server. Tenere presente che questo livello di registrazione include, in aggiunta ai messaggi di informazioni, i messaggi di tipo Fatal, Error e Warning, ovvero relativi ad avvisi, errori ed errori irreversibili. AlwaysOn raccoglie informazioni prima, durante e dopo il verificarsi di un problema. Questo comportamento è radicalmente diverso rispetto a quello degli strumenti di registrazione precedenti, ad esempio OCSLogger. L'esecuzione di OCSLogger avveniva quando il problema si era già verificato, rendendone più difficoltosa la risoluzione poiché i dati raccolti erano di tipo reattivo e non proattivo. Se AlwaysOn non contiene le informazioni cercate per individuare il componente che causa il problema e indicare le azioni per la risoluzione (evento improbabile, data l'estensione e il livello di dettaglio dei provider in AlwaysOn), indicherà un livello di informazioni ragionevole per determinare le altre operazioni da eseguire, ad esempio creare un nuovo scenario, raccogliere altre informazioni, eseguire una ricerca diversa per raccogliere dettagli più specifici e così via.

servizio di registrazione centralizzato offre due modi per specificare i comandi. Sono disponibili vari argomenti direttamente focalizzati sull'uso di Windows PowerShell attraverso Lync Server Management Shell. La possibilità di utilizzare numerose configurazioni e comandi complessi privilegia l'uso di Windows PowerShell per servizio di registrazione centralizzato. Poiché l'uso di Windows PowerShell attraverso Lync Server Management Shell è praticamente universale per tutte le funzioni in Lync Server, vengono descritti solo i comandi di Windows PowerShell.


> [!NOTE]
> Se si sceglie di usare il set di comandi limitato disponibile dalla riga di comando, è possibile ottenere assistenza con CLSController.exe digitando <CODE>ClsController.exe</CODE>. Per impostazione predefinita, <STRONG>ClsController.exe</STRONG> viene installato nella directory C:\Programmi\Microsoft Lync Server 2013\ClsAgent.



## Per eseguire Start-CsClsLogging con Windows PowerShell usando comandi di base

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Avviare uno scenario di registrazione con il servizio di registrazione centralizzato digitando quanto segue:
    
        Start-CsClsLogging -Scenario <name of scenario>
    
    Ad esempio, per avviare lo scenario **AlwaysOn** digitare:
    
        Start-CsClsLogging -Scenario AlwaysOn
    

    > [!NOTE]
    > Lo scenario AlwaysOn non ha una durata predefinita. Verrà eseguito finché non lo si interrompe esplicitamente con il cmdlet <STRONG>Stop-CsClsLogging</STRONG>. Per informazioni dettagliate, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging">Stop-CsClsLogging</A>. Per tutti gli altri scenari, la durata predefinita è 4 ore.



3.  Premere INVIO per eseguire il comando.
    

    > [!NOTE]
    > Per l'esecuzione dei comandi e la comunicazione dello stato dai computer della distribuzione possono essere necessari da 30 a 60 secondi.

    
    ![Esecuzione di Start-CsClsLogging.](images/JJ687958.c5be7413-8cef-4de7-9712-944d20cc2fa4(OCS.15).jpg "Esecuzione di Start-CsClsLogging.")

4.  Per avviare un altro scenario, usare il cmdlet **Start-CsClsLogging** con il nome dello scenario aggiuntivo da eseguire (ad esempio lo scenario **Authentication**) come segue:
    
        Start-CsClsLogging -Scenario Authentication
    
    > [!IMPORTANT]  
    > È possibile eseguire un totale di due scenari su qualsiasi computer in qualsiasi momento. Se l'ambito del comando è globale, lo o gli scenari verranno eseguiti da tutti i computer della distribuzione. Per avviare un terzo scenario è necessario interrompere la registrazione nel computer, pool, sito o ambito globale in cui si vuole eseguire il nuovo scenario. Se è stato avviato un ambito globale, è possibile interrompere la registrazione per uno o per entrambi gli scenari in uno o più computer e pool. Per informazioni dettagliate sugli scenari in esecuzione, vedere <a href="lync-server-2013-using-stop-for-the-centralized-logging-service.md">Utilizzo del comando Stop per il servizio di registrazione centralizzato</a> e <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging">Stop-CsClsLogging</a>.

## Per eseguire Start-CsClsLogging con Windows PowerShell usando comandi avanzati

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Sono disponibili ulteriori parametri per la gestione dei comandi di registrazione. -Duration consente di regolare la durata di esecuzione dello scenario. È anche possibile definire -Computers, un elenco di nomi di dominio completi (FQDN) di computer separati da una virgola, oppure -Pools, un elenco di FQDN separati da una virgola dei pool nei quali si vuole eseguire la registrazione.
    
    Si supponga di voler avviare una sessione di registrazione per lo scenario *UserReplicator* nel pool "pool01.contoso.net". La durata della sessione di registrazione deve essere di 8 ore. A tale scopo, digitare:
    
        Start-CsClsLogging -Scenario UserReplicator -Duration 8:00 -Pools "pool01.contoso.net"
    
    L'esecuzione corretta dello scenario restituisce un risultato simile al seguente:
    
    ![Esecuzione di Start-CsClsLogging.](images/JJ687958.399f0c2e-c08c-40ab-b6c6-381dddc12fe9(OCS.15).jpg "Esecuzione di Start-CsClsLogging.")
    
    Si noti che in questo esempio gli scenari AlwaysOn e UserReplicator sono entrambi in esecuzione.

## Vedere anche

#### Concetti

[Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md)

