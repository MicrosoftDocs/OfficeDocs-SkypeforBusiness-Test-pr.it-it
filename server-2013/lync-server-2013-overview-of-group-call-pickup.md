---
title: Panoramica della risposta alle chiamate di gruppo
TOCTitle: Panoramica della risposta alle chiamate di gruppo
ms:assetid: 3dc0eca8-c773-463c-96bb-9cd6afa2a840
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945623(v=OCS.15)
ms:contentKeyID: 52062134
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica della risposta alle chiamate di gruppo

 

_**Ultima modifica dell'argomento:** 2013-02-12_

La risposta alle chiamate di gruppo, una nuova funzionalità inclusa negli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013, consente agli utenti di utilizzare i telefoni personali per rispondere alle chiamate in arrivo per i colleghi. Con questa nuova caratteristica si ottiene una maggiore disponibilità della linea di un utente grazie alla possibilità di consentire ad altri utenti di rispondere a una chiamata in arrivo componendo un numero per la risposta alle chiamate di gruppo. Con la distribuzione della funzionalità di risposta alle chiamate di gruppo è possibile ridurre in modo significativo il numero di chiamate in arrivo instradate alla segreteria telefonica e ciò risulta particolarmente utile per le chiamate dai clienti esterni all'organizzazione.

La funzionalità di risposta alle chiamate di gruppo è progettata in particolare le business unit in ambienti open space. Le chiamate in arrivo non rappresentano un disturbo perché squilla solo il telefono nella destinazione prevista. Gli altri utenti che sentono lo squillo, tuttavia, possono rispondere alla chiamata componendo semplicemente il numero di gruppo.

In ambienti in cui gli utenti non si trovano in un open space oppure nei quali gli utenti che condividono responsabilità comuni sono dislocati in posizioni geografiche diverse, la funzionalità di intercettazione team rappresenta la soluzione più appropriata. La differenza principale tra la funzionalità di risposta alle chiamate di gruppo e l'intercettazione team consiste nel fatto che con la risposta alle chiamate di gruppo la chiamata in arrivo squilla solo nella destinazione prevista e chiunque può comunque scegliere di rispondere componendo un numero di gruppo. Con la funzionalità di intercettazione team, la chiamata squilla in tutti i telefoni dei membri del team e qualsiasi utente del team può sollevare il telefono per rispondere. Un'altra differenza è il fatto che la funzionalità di risposta alle chiamate di gruppo viene gestita da un amministratore tramite Lync Server. Nel caso dell'intercettazione team, invece, gli utenti finali gestiscono la funzionalità tramite il client Lync. Con la risposta alle chiamate di gruppo, quindi, questo aspetto della gestione delle chiamate può essere centralizzato.

La risposta alle chiamate di gruppo è basata sull'applicazione Parcheggio di chiamata. Quando si distribuisce la funzionalità di risposta alle chiamate di gruppo, è necessario configurare la tabella dei codici orbit del parcheggio di chiamata con intervalli separati dei numeri interni designati come numeri per la risposta alle chiamate di gruppo. Come i codici orbit del parcheggio di chiamata, i numeri per la risposta alle chiamate di gruppo devono essere interni virtuali a cui non sono assegnati utenti o telefoni. Per ogni pool Front End in cui si distribuisce la risposta alle chiamate di gruppo possono esistere uno o più intervalli di numeri di risposta alle chiamate di gruppo. Gli intervalli di numeri di gruppo devono essere globalmente univoci nell'ambito della distribuzione di Lync Server.


> [!NOTE]
> Gli intervalli di numeri designati come numeri per la risposta alle chiamate di gruppo nella tabella dei codici orbit del parcheggio di chiamata non possono essere gestiti o visualizzati tramite il Pannello di controllo di Lync Server. L'unico modo per visualizzare tutti gli intervalli di numeri nella tabella dei codici orbit del parcheggio di chiamata consiste nell'utilizzare Lync Server Management Shell. In modo analogo, l'unico modo per aggiungere, modificare o rimuovere i numeri per la risposta alle chiamate di gruppo consiste nell'utilizzare Lync Server Management Shell.



Dopo aver configurato i numeri per la risposta alle chiamate di gruppo è necessario assegnare gli utenti a un gruppo per la risposta alle chiamate di gruppo. Altri utenti potranno rispondere a qualsiasi chiamata indirizzata a un utente assegnato al gruppo. All'arrivo di una chiamata per un utente assegnato a un gruppo di risposta alle chiamate di gruppo, qualsiasi altro utente che nota la chiamata può rispondere componendo manualmente il numero per la risposta alle chiamate di gruppo. L'utente che risponde non deve necessariamente essere un membro del gruppo. Quando un altro utente risponde a una chiamata, al numero chiamato in origine viene inviata una notifica.


> [!NOTE]
> Un utente può essere un membro di un solo gruppo per la risposta alle chiamate di gruppo.




> [!NOTE]
> Sebbene qualsiasi utente nella distribuzione di Lync Server possa rispondere a una chiamata indirizzata a un membro del gruppo di risposta alle chiamate, la persona che risponde deve conoscere il numero per la risposta alle chiamate di gruppo corretto da comporre.



Se un utente compone il numero per la risposta alle chiamate di gruppo per rispondere a una chiamata quando stanno squillando più telefoni nel gruppo, l'utente risponde alla chiamata che ha squillato più a lungo.

Le impostazioni di squillo simultaneo funzioneranno per gli utenti che utilizzano la risposta alle chiamate di gruppo. Ciò significa che una chiamata indirizzata a un utente assegnato alla risposta alle chiamate di gruppo squillerà per tutte le destinazioni configurate e un altro utente potrà rispondere alla chiamata. L'eccezione per questa regola è rappresentata dal caso in cui l'utente configura lo squillo simultaneo per la chiamata di tutti i membri del team.

Non è possibile utilizzare la risposta alle chiamate di gruppo per rispondere ai tipi di chiamate seguenti:

  - Chiamate a una linea privata

  - Chiamate da un contatto assegnato alla relazione di privacy Amici e parenti
    
    > [!tip]  
    > Un utente membro di un gruppo per la risposta alle chiamate di gruppo può impedire il recupero di determinate chiamate tramite la risposta alle chiamate di gruppo contrassegnando il contatto come contatto personale nel client Lync. Per contrassegnare un contatto come personale, impostare la relazione di privacy per il contatto su Amici e parenti. Qualsiasi chiamata in arrivo da contatti con relazione di privacy Amici e parenti non potrà essere recuperata tramite la funzionalità di risposta alle chiamate di gruppo.

  - Parte video delle chiamate audio/video
    

    > [!NOTE]
    > Se un utente risponde a una chiamata audio/video, riceverà solo la parte audio. La persona chiamante o la persona che risponde alla chiamata può effettuare l'escalation della chiamata per aggiungere la parte video.



  - Chiamate con squillo simultaneo instradate ai membri di intercettazione team

  - Chiamate instradate a un delegato

  - Chiamate instradate a un Response Group

I tipi di utenti seguenti non possono partecipare alla risposta alle chiamate di gruppo, ovvero non devono essere inclusi nel gruppo e non possono rispondere a chiamate destinate a utenti che hanno abilitato la risposta alle chiamate di gruppo.

  - Gli utenti ospitati online in una distribuzione ibrida

  - Gli utenti non ospitati in un pool di Lync Server 2013 con gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013 in una distribuzione in locale

Se nessuno risponde a una chiamata per un membro del gruppo per la risposta alle chiamate di gruppo, la chiamata viene instradata in base a quando specificato nelle impostazioni client, ovvero viene indirizzata alla segreteria telefonica o inoltrata a una diversa destinazione.

